The OmniaONE is a livewire capable multiband compressor with some added "magic" by Omnia. For the sake of our installation, it functions to ensure our webstream is very LOUD before being smashed into MP3 compression through shoutcast etc.

The Omnia is configurable by a web interface at its IP address of 192.168.0.142. It is currently loaded with the "Multicast" firmware for use in webstream and online compression. Other firmware images (FM) are available.

There is a preset called WMFO which is basically an MP3 128kbps with some tweaking and the final limiter turned up to increase volume. It's important to have a higher final limiter stage to increase volume, as the MP3 compression (especially the 128k and 64k) really destroys the fidelity, and the effect is worse with quieter signals.

The output volume is also set to 0 dBFS to maximize the audio. The entire Axia system is 24 bit, so it's not necessary to have full scale audio. However, the MP3 stream is only 16 bits, which means the importance of loud audio is increased.

It's currently not set terribly loud, and most DJs seem to prefer feeding audio through the system at -36 dBFS instead of -12 as the system expects, and in that case the compressor functions solely as a volume increase because it doesn't it any gain reduction.

### Problems

The Omnia was put into service in late 11/13 and it was noted by mid-December that the built in Java metering system had stopped displaying levels. A reboot on 12/24/13 fixed the issue, but it interrupts audio flow. If this continues, support should be contacted.

The web interface stopped responding in mid-January (but Telnet was unaffected) during which Telos support was contacted. They blamed Java, somehow. A reboot solved the problem.

By early February, the level meters on the front had stopped working and were displaying a static arbitrary level. The Java interface had likewise ceased to function. A reboot on the night of 2/13/14 solved the issue. Telos is being contacted.

6/30/14: For some reason it has become vastly more stable with age. No explanation.

1.  1. [Problems](#Problems)

