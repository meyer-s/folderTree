Overview
--------

WMFO is required to record telemetry readings from its transmitter. The unit used to do this is the VRC2500. It was manufactured by Gentner, which was bought out by Burk. Burk still supports the unit. The unit is capable of configuration via a dial-up modem and/or a direct serial connection. The unit also has a "Voice" unit, which is capable of answering phone calls, and providing basic menu functionality to touch-tone phones. Full details can be found in the [VRC2500 menu](http://www.burk.com/Support/Vrc2500.aspx "http://www.burk.com/Support/Vrc2500.aspx") supplied by Burk.

Historical Telemetry Readings
-----------------------------

In the past, no automated telemetry readings were taken by the VRC2500. DJs were forced to call the VRC2500 and use the voice prompts to receive telemetry readings, which they then recorded into a book. Unfortunately, DJs were unreliable and were even caught with full evidence of copying over older readings to new times.

Old Modem Telemetry System
--------------------------

The VRC2500 is currently programmed to record telemetry readings every hour. Every day, the Lynx software, the software provided by Burk to manage and configure the VRC2500, dials in using a dial-up modem connected to Supertramp and downloads these recorded samples. The VRC2500 can hold about a week's worth of telemetry readings before it begins to overwrite its buffer. The Lynx software records these values into an Access database file. A WMFO program (contact Ben Yu for technical support) reads in these values via OBDC, and then outputs them to a text file, which is published on Smoothcriminal's webserver. 

Current Telemetry System (IP)
-----------------------------

The VRC2500 unit is attached to an IP Unit from Burke which allows it to maintain connectivity over a Fiber Box to download readings. The Lynx software has also been moved to Smoothcriminal following the untimely death of Windows on Supertramp.

Online access
-------------

The Linux Server, ThinWhiteDuke, contains an apache website where the chief operator can digitally record a signature, signifying that he or she has ascertained telemetry has been recorded correctly in the previous week. The telemetry readings themselves are accessed [on Smoothcriminal](http://wmfo-smooth.orgs.tufts.edu/data.txt "http://wmfo-smooth.orgs.tufts.edu/data.txt").

Calibration
-----------

The VRC2500 unit takes it readings from GPIO with the other rack-mounted units in the tower. Calibrations must be performed when the VRC2500's memory is wiped and/or when the equipment in the transmitter line changes. Details on the calibration procedure can be found in the Lynx 5 manual from Burk.

Miscellaneous
-------------

The Lynx software is set to startup automatically on Supertramp. Unfortunately, when not launched in a Desktop session, the Lynx software tends to freeze. It works much more reliably when invoked in a Desktop environment which is then locked. As of now, it is SOP for the CO to kill the background Lynx and start a Lynx session in a Desktop logon on Supertramp. Once started, it is only necessary to keep the LynxLogger window minimized in the system tray.

Troubleshooting
---------------

If when firing up the Lynx 5 software, it doesn't see the modem, try disconnecting the modem for 5 minutes (power off then pull serial cable). Then (while unplugged), run program "services.msc" and restart the telephony service. Then plug the modem back into the computer, turn power on, select COMM1 from device manager and "Scan for hardware changes."

You should see the modem magically appear in the modems category.

1.  1. [Overview](#Overview)
2.  2. [Historical Telemetry Readings](#Historical_Telemetry_Readings)
3.  3. [Old Modem Telemetry System](#Old_Modem_Telemetry_System)
4.  4. [Current Telemetry System (IP)](#Current_Telemetry_System_(IP))
5.  5. [Online access](#Online_access)
6.  6. [Calibration](#Calibration)
7.  7. [Miscellaneous](#Miscellaneous)
8.  8. [Troubleshooting](#Troubleshooting)

