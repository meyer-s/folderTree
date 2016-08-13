# Doing Remote Broadcasting

Remote broadcasting is a powerful tool for a variety of station uses, primarily events which focus on location and publicity for the station.

There are multiple methods for handling these events:

- Simple phone remotes using a cell phone or landline connection. Quality will be lame.
- VoLTE remotes where someone ties their iPhone into the board and we use a separate iPhone for the broadcast. Has the benefit of being easy to carry, plus VoLTE should be quite reliable as VZW controls the whole network. Procuring an Apogee Duet interface would be beneficial.
- Skype remotes using the Skype application. Again, using an audio interface will be of great benefit.
- Use the Zephyr / IP units. The system consists of two devices: stationary unit is mounted in Bay B, between Control and Studio A and the mobile unit resides in the Annex when not in use. The units can "call" each other over the internet, and send audio in each direction. They are equipped with a variety of codecs for remote use and transmit in stereo in both directions.
- ipDTL which offers a laptop + Google Chrome web browser solution as well as ISDN interoperability. Could be easily deployed in Studio C etc.

Log
---

Log uses and test calls of the Zephyrs here and report any problems. This allows us to make sure test calls happen often enough.

|Date|Event|Notes|
|:---|:----|:----|
|11/6/12|Election Night @ Campus Center|Wired connection held high bitrate for hours.|
|3/30/13|Ops meeting| |
|June 2016| Nick was able to remote broadcast from his bedroom in Newbury MA| WiFi from within NAT without port forwarding over a Comcast connection. Set up with RemoteRivMix from CONSE1 which is a mix of both Rivendell from the main server output and the remote source. Backfeed was just the RD-All from rivendell and used VNC to control rdairplay|


# Physical Setup

If you just want to have up to 4 people talking with mics headphones, you don't need any other equipment. The Zephyr supports 4 XLR inputs and 4 monitors (headphones with 1/4" jacks; one on the front, three on the back). The knobs on the top row control the input volume, while buttons toggle sending that input to XLR output A or B, i.e. speakers. You'll probably want every active mic on A and B. There is no way to control the volume going to the speakers, nor what input (it gets all 4 plus Livewire receive). Each monitor has its own volume and the option of whether to listen to send, receive, both, or neither. Again, you'll probably want both, which will let you talk to someone in the studio. While simpler, this setup is the one you're less likely to use.

If you want more control, bring the mobile Allen and Heath (a ZED 14 that lives in the big hard Gator case in tech 2) and optionally the Rane headphone splitter (1RU unit in tech 2) although the Zephyr's monitors should be plenty. Run the A&H main out to Zephyr inputs 2 and 3 (1 does not work properly). On the Zephyr, Stereo mode maps A to L and B to R; assign inputs 1 and 2 to match the wiring from the A&H and make sure their gain knobs are turned up.

Normally you'd put all your mics on the A&H but if you ever want to put them directly into the Zephyr, there's a setting to turn up their gain. Set it back to pro audio when you're done, otherwise it will sound horrible from having so much gain.

In either setup, bring the longest ethernet cable you can find (it typically lives on top of the mobile Zephyr in Storage). Bring plenty of XLRs (1 per mic or speaker; 2 to connect A&H out to Zephyr; spares); power cables (1 per Zephyr, speaker, or A&H); headphones mics stands and holders (1 per person). Bring the swag box, which has a roll of gaffer's tape to tie down cables and put up the banner. Make sure in advance you'll have a table, or bring one. Bring a laptop and charger to log Spinitron from. Even if you're just talking for more than a few minutes, log something and set the format as "Live". You still need to log and you still need to do station IDs, but the PD may waive the PSA requirement.

## Set up Internet

The mobile unit needs internet connectivity, which can happen in one of three ways: the built-in ethernet jack, the USB WiFi dongle taped to the unit, and a cellular data dongle (boxed in Storage, used a few times in 2011, [Clear](http://www.clear.com/ "http://www.clear.com/") data plan required). Both the ethernet and WiFi dongle should connect to the Tufts network DHCP automatically (the Link and Z/IP indicators onscreen should be green). From there, press the CONN button of the right of the front panel and call the most recent number, which should be the stationary unit. Make sure it has the `tscp:` prefix. In practice, try to use the Ethernet cable (we have a pretty long one).

# Setting up livewire audio etc.

There are several methods for getting audio to the Zephyr, and the method you choose is dependent on which application you're working.

## Board Backfeed for Studio Staffed Remotes

There is an apparent bug in the Zephyr that prevents you from selecting a typical "To" source.

Note about backfeeds: When you configure a Codec on the Studio A Element, it allows you to configure a backfeed source and you can select "default" (the new software has a more intuitive interface than the old version running on the powerstation). When the source is on the board, a "To" backfeed will be generated on the livewire channel "From" which the source is coming. The source will automatically be a mix-minus without any configuration and the talkback will function as expected.

Instead of selecting the "To:" source directly (because it doesn't show up) you will have to create a VMix on the StudioEngine. One is already set up for this purpose called Zephyr-Backfeed or something -- just set the Zephyr to receive it. (Basically each of the VMix channels acts as a tiny virtual mixer. You can combine sources and adjust volumes and there is a configurable transition/fade time when you alter volumes. A simple application could cURL this interface and mix things remotely. In this case we just use one channel and essentially duplicate the source.)

## More advanced setups

Mix together the 1) Zephyr Output and 2) the RD-All from Rivendell server and send that to the EAS Output. This way you can vnc to Rivendell either over RDP or using SSH port forwarding and control Rivendell remotely. Then you could send just the RD-All back to the Zephyr, or you could create a mix of the preview and main outputs (you'd have to separate them first). There's a RemoteRivMix set up to duplicate the Zephyr and the Rivendell Server RD-All output. 

Proper use would require some method of fading: easier would be to manually adjust the VMix or use a simple program to do it. More effective would be a GPIO triggered switch of levels so that the main feed would cut out when preview was engaged.

# Studio Usage

With just the backfeed sent (via the hacky VMix) we can use the talkback button to communicate with the codec just like phones. Simply press and hold the talkback to send Mic 1 to the codec backfeed.

In the station, add the Codec to the element channel (the talkshow profile has it by default). Put up the Zephyr fader like any other.

# Codec choices

If you'll be doing any interactivity it's best to choose an advanced low delay Codec like AAC-ELD. The Zephyr has some simple defaults (quality vs latency). The manual gives some good detail about codec choice. If you're running the mobile unit over Tufts wired connection, you can crank minimum and maximum bitrates upwards and experiment with different codecs. If the talent doesn't need really fast communication back and fourth you could increase the quality and switch to a standard AAC or even uncompressed codec. If you stick to playing music through Rivendell over VNC you can definitely get away with a simpler codec for speach.

# Test Calls

As long as the Studio unit remains connected the WMFO group should remain registered. If you run into problems you can follow instructions in the manual to recreate the WMFO group. In general so long as the group stays available the mobile unit should automatically reregister upon connection. Make a test call between the units *a few days before a remote broadcast event*. (This way there is time to troubleshoot if something goes wrong, and so everyone knows who the system works.)

Call the Telos test line from the stationary unit, the mobile unit over WiFi, and the mobile unit over ethernet. 

# Overview of Z/IP Protocol

The Zephyr uses a proprietary protocol to negotiate called ZepherIP or Z/IP. It uses a Telos server to keep registrations curent and help traverse NAT. Though this isn't required in our circumstance, Telos recommends using this protocol because it's supposedly more tolerant to varying network conditions than an RTP-Push or SIP setup.

We've periodically had problems getting connection after the new Tufts networking shenanigans where they put up a PRC-style firewall. Here are some steps to help here:

- Ensure your firewall settings are correct at the Studio side. The Zephyrs should be able to connect from within a firewall if the Studio unit has an open firewall (see note below)
- Talk to TTS about a firewall exception. You may have to specifically get one for whatever location you're broadcasting from.
- Use a 4G LTE Modem, either wifi tether or a cradlepoint 4G modem with a prepaid Verizon data plan (or an ops staff iPhone in wifi tether mode)
- Try to use SIP and RTP push (may requrie you to enable the intelligent SIP functionality in the Ubiquiti router; can use the spare router in Control so we don't have to mess with the VoIP

Troubleshooting
---------------

If you have trouble connecting (which should only happen if the studio unit shuts off for > 6 months, start from scratch and do the following.

If the stationary unit displays a green "Link" indicator but a red "Z/IP" indicator, do a factory reset (Settings -\> Reboot -\> Reset to Defaults). Follow along in the manual's quickstart guide (google for the latest version). Best practice is to unplug the ethernet cable first in case the IP it chooses conflicts with one we use. Go to Network-\>Ethernet config. Barring massive changes to LAN [IP table](https://wiki.wmfo.org/index.php?title=Operations/Diagrams_%26_Tables/IP_Address_Space "IP Address Space") after this writing, the IP is 192.168.0.140, the netmask is 255.255.0.0, the gateway is 192.168.9.10, and the DNS is 192.168.9.10 (or use 8.8.8.8 - Google). Disable DHCP. Activate the settings. Plug in the ethernet cable. The Link and Z/IP indicators should now be green, and you should be able to call the Telos test server. If not (and Link is green), contact the ops list or Telos support.

Set up the group, which you may need to recreate, using the credentials for the Z/IP server. You can use the browser web interface to change the unit password and the listen port to 9636. Change the Livewire Source to 10400 and the destination to whatever backfeed audio you've selected.

The stationary unit is CONZP1 and the mobile unit is MOBZP1.

At one point we had the Zephyr MACs registered as "assests", which would last for 7 years and be independent of an individual. Neat trick if you can manage it. Otherwise [manually register](http://portal.net.tufts.edu) the MAC addresses yourself. Once that's done, plug in the cable or dongle to the mobile unit, do the network config (enable DHCP), and select that source as the "streaming source". Same deal as above: The Link and Z/IP indicators should now be green, and you should be able to call the Telos test server. If not (and Link is green), try doing a factory reset. If there's still an issue, contact the ops list or Telos support.

Once you have two units that can each call the Telos test server, you should be able to call one from another using the groups you set up. It's sufficient for now to look at each unit and see that they both think they're connected.

There are a bunch of audio settings that may need attention. Consult the engineers or ops list. Then do the test call procedure as above. And then you can say that it works.

Addendum: The stationary unit has only a LAN IP and requires port forwarding. The Ballou router should be set up to forward to the appropriate port. Your shouldn't need to modify these.

# Note from Telos on Z/IP Ports

Note: This is technically for the newer ZepherIP One but most of the facilities are quite similar. The Z/IP One would have a second interface for WAN (which would be helpful should we ever choose to upgrade).

"There is an option in the Setup / Zip Server front panel screen or the Streaming screen of the web interface called "Listen Port" that is set to 0 (automatic) by default. If you set a port number here that you forward, you should be able to route through your router. For example: Rather than leaving the Listen Port set to "0", assign a listen port such as, for example, 21440, and set the router to forward UDP packets to this port. If there are several Z/IP ONE's behind the same firewall, be sure they use different listen ports.

A benefit to setting a static listen port and creating a port forward to it, connection are usually made instantly instead of taking 10 seconds for port negotiation. This is true for most but not all routers.

Both server assisted and direct TSCP connections with the Z/IP ONE are using the "Listen Port", as it relates to flexibility in setup for using the ZIP Server, or for directly-placed TSCP (protocol) calls from one Z/IP ONE to another.

Other ports are de facto industry standard ports, such as port 5060 for SIP calls. Your Z/IP ONE may be behind a NAT router, many of which can do port translation as well as IP address translation.

It is important to note that TSCP connections use the ACT algorithm while other types of connections (such as RTP Push) do not and therefore require excellent connectivity or a connection with QOS to avoid dropouts.

From the manual:

Listen Port

– Enter a value in this field if you need to set a particular port on your Ethernet router to allow Z/IP communications through. The default is ‘0,’ which instructs the Z/IP to use a random port for listening. This random port is shared with the Z/IP Directory Server, which maintains a list of which ports are used by which Zephyr/IPs. This is most useful when setting up port forwarding through a restrictive NAT. If the Z/IP ONE reports a symmetrical NAT, contact your IT administrator for advice on what setting to use here and to set up a port forward.

RTP Push Receive Port

– Change the RTP receive port from the default of UDP 9150, or make blank disable. The three fields following this, G.722 reply at (port+1), Rcv codec reply at (port+2) and User codec reply at (port+3) are for configuring an automatic reply to an incoming RTP stream. For a full explanation of how these settings are used, see Section 9.3, Real-time Transport Protocol.

HTTP/Web Server Port

Allows you to change the Z/IP ONE’s management web interface. Entering a 0 in this field uses the standard, TCP port 80. Since the standard port (and the unofficial, but relatively common management ports of 8800 and 8080) are well known, a Z/IP ONE on the public internet should have its web server set to a unique, non-standard port.

This can also be used to allow management of multiple Z/IP ONEs that are behind a router that supports port forwarding, but not port translation."

