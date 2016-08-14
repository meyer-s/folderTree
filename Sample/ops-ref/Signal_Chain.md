A high level overview of the signal chain is depicted in [this google drawing](https://docs.google.com/drawings/d/1ZioPk_CP5EZg8U6Jix9IY1ol_1xH6u0A_kD7RZt3h1g/edit?usp=sharing "https://docs.google.com/drawings/d/1ZioPk_CP5EZg8U6Jix9IY1ol_1xH6u0A_kD7RZt3h1g/edit?usp=sharing").

Common Signal Chain
-------------------

1.  Audio starts out as:
    1.  Inputs to a Node from microphones, computers, CD players, etc. or
    2.  Audio played through the ASI card directly off of Duke

2.  Those sources are mixed together by StudioEngine (Studio A) or the PowerStation (Studio C), producing a Program source (Program 1 on each board).
3.  That program feed passes through the EAS, which replays emergency alerts received from other stations in the area. The EAS output goes to either the webstream or the transmitter.

### Transmitter

1.  The transmitter-omnia with the FM image provides processing of the audio data. It compresses the everything to increase signal volume and compensate for DJ incompetence. This device outputs AES audio directly to the transmitter.
2.  The transmitter takes the AES data and converts it to a composite signal.
    1.  The transmitter outputs the multiplex signal to the Inovonics RDS encoder. The RDS encoder gets RDS data from a script on wmfo-http's push.wmfo.org which receives Spinitron Push data and formats it for the RDS 64 character Radio Text string. It generates the RDS subcarrier which is returned to the Transmitter to the Aux input port.

3.  The transmitter feeds a Coaxial output which is connected to the antenna on the roof.
4.  The feed is monitored by the Modulation Monitors in the Tower and in Studio A.

### Webstream

1.  The control Omnia compresses the audio data and feeds it back to the Livewire network.
2.  The stream is captured via the wmfo-webstream AoIP license and encoded for webstream distribution on Shoutcast. (See the webstream doc for more info)


