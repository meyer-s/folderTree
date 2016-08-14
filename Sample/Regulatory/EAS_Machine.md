Overview
--------

WMFO uses a SAGE Digital ENDEC as its EAS Encoder/Decoder. The unit is located Bay B, the equipment rack between Studio A and Control. The EAS unit is connected to a rack mounted radio-monitor unit. This unit is just two radio tuners that supply audio to the EAS machine. They are tuned to the [EAS Primary Stations](http://www.mass.gov/eopss/home-sec-emerg-resp/emergency-info/threat-level/emergency-alert-system-eas-for-massachusetts.html "http://www.mass.gov/eopss/home-sec-emerg-resp/emergency-info/threat-level/emergency-alert-system-eas-for-massachusetts.html") for the State of Massachusetts: 104.1 FM and 1030 AM. These are the two stations WMFO is required to monitor in order to relay EAS alerts. Each has an associated antenna.

Configuration
-------------

The EAS has inputs and outputs on the Control side. The output is the same as the input, unless there's an alert, in which case the alert is output instread. The EAS is therefore part of signal chain. Consult the Livewire tables to be sure, but it is typically downstream of SA Pgm1 and upstream of the Aphex webstream compressor and tower router selector. "Bypassing Studio A" means routing a different source into the EAS-IN destination.

The EAS machine can be configured from the physical front panel of the machine. The only relevant options from the front panel are the ability to set the unit's IP address (as it has a NIC card and is presently on WMFO's internal LAN) and the ability to run an EAS test at will.

Most configuration is done through the web browser interface. A configuration file can be downloaded from the unit. Once downloaded on to a Windows PC, the SAGE provided software (installed on Supertramp) can be used to modify the settings, before uploading to the unit. The unit reboots (takes around two minutes) when settings are updated. It likely ceases to function during this time - consider temporarily routing around it in Livewire.

Required Tests
--------------

WMFO is required to send out weekly tests of the EAS encoder. Luckily, the SAGE Digital ENDEC has an option to randomly generate test dates every week. That option is currently used.

We receive monthly tests from the EAS Primary Stations. The EAS does will discard duplicate alerts, and it's a tossup which station it hears from first. As of December 2012, the audio quality of the alerts is acceptable. The EAS stores tests temporarily. Some radio stations use this feature to insert the test into programming, but WMFO does not, so tests play a few minutes after they are received. An actual emergency alert would be played immediately.

Logging Configuration
---------------------

WMFO is required to log certain EAS events. The SAGE Digital ENDEC will log events in its internal memory. This log can be viewed through the web interface. The EAS machine can also be configured to send logs via email or by ftp. WMFO uses both of these options.

The EAS is configured to ftp to Smoothcriminal and place log files there. It uses a special WMFO\\EAS account on the domain to do this. The root of the ftp is on Smooth's C drive, called "EAS." This is copied over to the data store and synced between the servers.

The EAS is also configured to send emails to [ops@wmfo.org](mailto:ops@wmfo.org "mailto:ops@wmfo.org") and [co@wmfo.org](mailto:co@wmfo.org "mailto:co@wmfo.org"). It uses the credentials of the donotreply account to send these emails. The password in the configuration of the SAGE Digitial ENDEC must be updated whenever the password for [donotreply@wmfo.org](mailto:donotreply@wmfo.org "mailto:donotreply@wmfo.org") is updated.

The webpage http://\<EAS Address here\>/mailerr willl show any errors (since the last reboot) the EAS machine has with logging via email or ftp. It is useful for debugging.

Miscellaneous
-------------

During the first national test of the National Emergency EAS code, it was found that the EAS input gain was too high. This is a problem with the EAS circuitry. At gains too high, the EAS output will cross-talk into the input, causing a messages mixed with a delayed version of itself to be played out over the airwaves. SAGE has leveling guidelines for this issue, and it has been implemented at WMFO.

1.  1. [Overview](#Overview)
2.  2. [Configuration](#Configuration)
3.  3. [Required Tests](#Required_Tests)
4.  4. [Logging Configuration](#Logging_Configuration)
5.  5. [Miscellaneous](#Miscellaneous)

