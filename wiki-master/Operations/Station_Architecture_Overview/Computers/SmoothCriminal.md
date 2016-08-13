Services
--------

Smoothcriminal is the last Windows host following the untimely death of Supertramp.

### IIS7

As of 7/14, most services are hosted on the Linode or elsewhere. What remains is a legacy FTP fileshare and the "Default Website" which hosts data.txt, a huge file of all the telemetry data since the dawn of time (aka 2009).

### Lynx 5

This is the legacy program by Burk which interfaces with the IP Telemetry unit in the tower to download telemetry readings every day. It is started by a Windows service in the background so that it may download and then killed. A service then dumps the database file into a text file and pushes it to the data.txt web file.

###  EAS Configuration

This has a windows program necessary to configure the EAS box.

### Fileshares

It currently houses the secondary RAID and exposes some shares.

1.  1. [Services](#Services)
    1.  1.1. [IIS7](#IIS7)
    2.  1.2. [Lynx 5](#Lynx_5)
    3.  1.3. [ EAS Configuration](#EAS_Configuration)
    4.  1.4. [Fileshares](#Fileshares)


