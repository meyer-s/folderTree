# Webstream Architecture

WMFO serves its webstream through a shoutcast server. The signal chain is as follows:

1. EAS Output from COND1 is sent to webstream-omnia in the tower
2. The webstream omnia runs AGC and multiband compression to increase the loudness of the track up from a normal of -12 dB to full scale (or rather, whatever the DJ decides to send). This is necessary because the codecs that compress the audio down to a low bitrate tend to destroy quiet signals and with limited dynamic range and quality it's important to use more of it.
3. The output of the webstream-omnia is sent to the input of wmfo-webstream.orgs.tufts.edu. The webstream host uses a 4 channel license of Axia's AoIP Windows Driver to pull audio off the network.
4. The Shoutcast Server runs as a Windows Service. It can be accessed through webstream.wmfo.org and using the admin login (password is configured in the Windows configuration file c:\Users\wmfo-admin\Documents\SHOUTcast\sc_serv.ini). It's configured to bind to a few extra ports for legacy compatibility with the old streaming setup which used three separate servers on port 8000 8002 8004 for each quality. Eventually we can remove those (once the iOS app is retired).

The three streams are:

1. /mobile @ 56kbps HE-AACv2, recommended for data-sensitive applications with quite good quality
2. /highq @ 256kbps AAC, recommended for enjoying the fidelities
3. / @ 256kbps MP3, recommended for clients that can't handle the AAC

You can query the stream listeners at https://www.shoutcast.com/Search?query=wmfo

## Notes

- AoIP driver is not technically supposed to run on top of KVM's virtualized network hardware and internal bridge, but appears to be working fine. The jitter occasionally exceeds the recommended value but we have not heard of any issues with dropouts and noise (it would sound like a popping if we were losing packets or whatever). Should we wish to change this, a physical NIC installed in a spare PCIe slot in Tupac would be a suitable alternative to running an entirely separate box in the tower.
- There are some issues with clients playing nice with streams. Safari on iOS, OSX etc supports Shoutcast V2 quite well, though Chrome is less happy. Many clients only play stream #1 (HE-AACv2) regardless of what you specify (for example, TuneIn displays only our HE-AACv2 stream for all streams even though I sent them the separate URLs). iTunes works well. VLC works well. There are sometimes issues with getting the stream to send based upon query URL. You can either specify with an ?sid=3 variable in the URL. Sometimes, you can use the http://webstream.wmfo.org/; to force sending the stream but this again appears to only send stream ID 1. Some fiddling is necessary. The best streaming solutions are for either iTunes or VLC on Desktop.

# Archives

Archives are recorded by SoX on Windows. I had trouble running it as a service so it's still running as a console application. Basically:

1. SoX records the audio data from the default audio card.
2. It converts it to a simple PCM Signed 16 bit format, which is literally (Low Byte L) (High Byte L) (Low Byte R) (High Byte R) or some such formwat. It has no headers or anything so when converting it back you must specify 2 channels, 48000 sample rate, 16 bit signed to SoX or else the output will be mangled.
3. SoX dumps this to a custom program called the hour_mator.exe which simply takes in data and writes it to the network share in (approximately) hour increments.

At this point, this Windows computer's role is done for recording.

## Notes

- I encountered problems with getting the batch file to run as a service. I will look more into this.
- If we decide we don't like windows, this service could be easily removed to the Rivendell host with the caveat that the Rivendell host may have more downtime and result in more lost archive time.
- We had a Samba crash due to a bug in samba on Ringo that resulted in a soft lockup. Rivendell and the archives both died. This bug should have been fixed by the update I ran (as it was a known bug). We probably want to do some hardening against errors such as these and maybe configure a failover to local storage.

## Serving the Archives

The archives are served from wmfo-http.orgs.tufts.edu host in Ballou. The page that serves archives is http://new-archive.wmfo.org/serve.php. It mounts the archive recordings share and then transcodes them on-the-fly per request. https://github.com/WMFO/archive-server is the github repo for them. These requests come from either:

1. Apps that implement archive support
2. wmfo.org /popout_archive.php player or whatever page that is
3. download.wmfo.org

All these apps implement (on their own) restrictions for downloading old shows (a two week time limit chosen to represent "fair use").

The approximate process is:

1. Request comes in with date, transcode type, and length parameters
2. Presence of MP3s triggers serving legacy format imported from old archive. It concatenates the MP3 streams.
3. Checks for .s16 files for date and length, serves 404 if not found
4. Checks for .done file in cache directory. If present, serve cache file.
5. If not present, check for partial file. If present, serve partial file (8). In this case, it sends the file size header in this case because it knows the size already.
6. If partial file not present, start transcode (handled by the separate transcode bash script using SoX).
7. Transcode handled by a separate process, which forks and continues in background.
8. Server serves partial file. It will continue to serve parts of the file until it reaches both the EOF marker AND the .done file has appeared. Stopping before both conditions would serve an incomplete file.
9. Exit

There are several edge cases to be handled:

1. If the transcode is complete (.done file present), sanity_check function takes a look at MP3 file size ratio with the original file. If it's over a ratio threshold (tested experimentally because I hate math), it assumes the transcode was interrupted prematurely and deletes both files, starting the transcode again.
2. If the transcode is in progress (cache but no .done file) but the file hasn't been modified very recently, we assume that some sort of error caused the transcode to fail or be interrupted. We discard the cache file and retranscode.
3. Wait until we confirm that the transcode file exists before entering the serve_incomplete function.

This has performed pretty well. There are several possible improvements:

1. Send estimated file size when we serve partial. Some programs don't like having no idea how big the file will be.
2. Allow serving a subpart of the file (sometimes players can implement lazy loading etc.)
3. Start transcode after every spinitron show concludes - SoX transcodes don't work particularly well with the lazy loading system we have built. Some filetypes embed the file length in the file header (I believe FLAC included) so SoX will fseek back to the beginning and add that at the conclusion of the transcode. The only other option would be to explicitly force the user to wait for transcode to complete, which is probably worse.
