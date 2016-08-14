This page will detail routing and equipment information from the WMFO equipment in Ballou. Signal chain will read roughly down the page, with some exceptions.

# PDU

This device is a network accessible power distributor, which runs off of a dedicated fibox line and will soon run out of the UPS. This allows you to remotely power cycle many devices in the tower for troubleshooting purposes. Obviously the prime candidate here is the Omnia which has shown some flakiness. You shouldn't need to use it, but it's here as a hard kill switch. Outlets are labeled in software.

1.  Omnia MPX Generator
2.  Inovonics 531 Mod Meter
3.  Cisco SG500X-24 switch
4.  unused
5.  unused
6.  unused
7.  unused
8.  Mozart Transmitter

# Router Selector

Currently also sends the output of the Inovonics Model 531 modulation meter back down as RF-TOW-MON livewire source. This will give garbage audio if the transmitter powers down, and can serve as a substitute for the Belar if need arises.

Allows you to listen to various sources over headphones which is good.

# Omnia FM (transmitter-omnia.wmfo.local)

Input: Livewire EAS Output

Output: AES audio (primary) and Livewire (secondary)

Also has other I/O and failover support.

Basically just slams our normalized audio up to maximum volume and adds compression.

# Webstream Omnia (webstream-omnia.wmfo.local)

Input: LW EAS Out

Output: Livewire (primary)

Slams the audio upwards in prep for webstream codecs

#### Functionality:

1.  This terminates the livewire network (listens to the EAS output)
2.  applies configurable multi-band compression
3.  Applies 75 uS pre-emphasis (US FM Standard EQ thing)
4.  Outputs AES audio (turned down a few dB from max to lower modulation)

#### MPX Signal Lesson:

MPX stands for multiplex and includes

-   FM L+R sum 0-15 khz
-   19k Pilot Tone (tells stereo decoders "yes this is a stereo FM broadcast")
-   FM L-R difference signal (Double Sideband Supressed Carrier)
-   (not yet, but someday) RDS at 57 kHz (3x harmonic of 19k pilot tone)

which is modulated onto the 91.5 mHz carrier in the Heterodyne Modulator. This signal should be thought of as a sound based signal even though the stereo is encoded at frequencies higher than humans can hear. The amplitude of this signal translates into carrier deviation inside the modulator where carier deviation is proportional to amplitude of MPX signal. Calibration is key.

### Inovonics RDS Encoder

We have an IP enabled Inovonics RDS encoder. It is configured over IP Telnet (and a Windows utility installed on Smooth).

1.  Data pushed to spinitron by user or Rivendell
2.  Spinitron pushes data to wmfo-http
3.  Script generates a string
4.  String pushed to RDS encoder over UDP
5.  RDS encoder receives MPX output from Mozart
6.  RDS encoder generates 57 KHz RDS output
7.  RDS input to Mozart
8.  Mozart adds RDS to transmitted signal

### DB Broadcast Mozart 100 Transmitter

Gets AES signal from Omnia. Generates stereo signal. Adds RDS either from internal RDS encoder or external. Provides control interface, monitoring, email alerts.

Outputs Modulated and amplified FM signal at 91.5 MHz and \~53 watts.

Watt Meter should confirm this. It should be calibrated with the VRC2500 to read 100% at 54 watts. There's a little fluctuation in output wattage especially right after you turn it on and this is probably acceptable. It's not like the FCC is going to come barging in the door unless we're up 10% above our specified level or more. Best not to tempt fate though.

Terminates this into our antenna which is a 50 ohm load. VSWR is the ratio of forward to reflected power. 1:1 is happy, 1:infinity is death. Should kick itself off if the VSWR gets too high (would be caused by antenna being destroyed).

### Rereceive/Modulation Meter

This is a DaySequerra M4FM mod monitor. We also have an Inovonics Model 531 FM modulation monitor ([manual](http://www.inovonicsbroadcast.com/wp-content/uploads/catablog/downloads/531Manual.pdf "http://www.inovonicsbroadcast.com/wp-content/uploads/catablog/downloads/531Manual.pdf")) back in studio A. The DaySequerra shows up on RF-TOW-MON channel. Can also give you a real time modulation indication.

To calibrate modulation:

1. Establish modulation baseline - since we have an RDS encoder at 6% of our modulation, we're allowed additional modulation over 100% (usually 103%).
2. Due to an issue with the limiter in the Mozart (i.e. it doesn't appear to do anything), we back off the AES output to reduce the effective modulation. This has proved pretty reliable - the control is on the transmitter-omnia remote control java applet.
3.  Switch to pilot tone measurement and adjust the 19 kHz pilot tone injection level until it reads about 9% on that meter. If you had to increase this measurement, best check that the overall increase in modulation hasn't significantly altered the readings.
4.  Switch back to regular modulation metering and make sure everything still looks good.

# Notes on Modulation Measurements with the Inovonics 531:

The manual specifies the integration time of the modulation calculator is by default set to 100 microseconds, and can be adjusted with an internal modulator up to 1 millisecond. Increasing the integration time has the effect of lowering the overall modulation reading for given content by averaging more readings together. The manual (also an excellent resource on calibrating FM transmitters) says that 1 ms is generally safe most all of the time. The safest bet here is to use a separate antenna to compare our off-air signal with that of local commercial stations and set our modulation to tend to be a little lower than theirs.
