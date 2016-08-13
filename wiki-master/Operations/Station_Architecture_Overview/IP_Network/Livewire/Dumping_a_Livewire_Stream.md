Sometimes you may wish to play out an Axia Livewire stream using a Linux computer on the Livewire network.

First, make sure you have SoX ([Sound eXchange](http://sox.sourceforge.net/ "http://sox.sourceforge.net/")).

Then, get [rtptools](http://www.cs.columbia.edu/irt/software/rtptools/ "http://www.cs.columbia.edu/irt/software/rtptools/") and run the following command to play out a livewire stream:

rtpdump -F payload 239.192.0.33/5004 | /usr/bin/play -c 2 -r 48000 -b 24 -e signed-integer  -B -t raw -

Basically meaning: dump the audio payload from livewire channel 33 (multicast ip: 239.192.0.33, port 5004) and pipe it to SoX.

Format is:

2 Channels
 48000Hz Sample Rate
 24 bit
 Signed Integer
 Big Endian

If you need to dump to a file use the actual SoX command. This /usr/bin/play is an alias for SoX to play out of the soundcard.

Also, this will probably only work on Standard Livewire streams, as Livestreams use a propriety Axia protocol instead of pure RTP.

*
