*ToDo: The content form the attached document needs to be updated and transfered to this page.*

 

### Fixing archives not streaming

On a more recent level, there has been a reccuring (3 times) issue with archives not playing due to the web server not keeping the proper time. Steps to fix:

1.  ssh into the Dreamhost server (see hosting credentials). Compare the server's clock (run the `date `command) to a known source like [time.gov](http://time.gov "http://time.gov") and see if they are off by more than 30 seconds.
2.  If yes, log into the Dreamhost panel and file a support ticket asking them to reset the NTP daemon. You can see previous support tickets if you like.
3.  If the Dreamhost server is on time, it's a new bug on Spinitron's side. Follow up with them.
4.  If Spinitron, Dreamhost, and the federal governement agree on the time, it's a different bug entirely.

1.  1. [Fixing archives not streaming](#Fixing_archives_not_streaming)

[Page Attachments](https://wiki-files.wmfo.org/Operations/Historical/Archive_%26_Streaming_%28old%29)
