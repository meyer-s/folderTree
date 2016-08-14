**NOTE: This page contains code requires SpinPapi Credentials. Contact Spinitron.com to obtain these and insert them into the attached "get-spinpapi-data.php" file.**

It grabs the metadata from the Spinitron API (SpinPapi) and puts it up on the SHOUTcast servers.

**README contents are below.**

This program uses a tempfile located at /tmp/SHOUTcast-Updater/tempfile.txt.  The location is hard-coded into update-once.sh.

Basically, how this works is that you run shoutcast-stream-updater.sh, and it updates all three SHOUTcast streams every 15 seconds until it's killed (CTL-C, etc).

shoutcast-stream-updater runs update-once.sh every 15 seconds.

update-once.sh queries Spinitron for data about the currently playing song with get-spinpapi-data.sh. It then checks to see if a new song is playing, and if so, formats the song data and posts it to the SHOUTcast streams.

spinpapi.inc.php is the SpinPapi Client Library.

 

Automatic Startup
-----------------

Started by watchdog.sh on ThinWhiteDuke.

1.  1. [Automatic Startup](#Automatic_Startup)

[Page Attachments](https://wiki-files.wmfo.org/Operations/Station_Architecture_Overview/Code/SHOUTcast_Metadata_Updater)
