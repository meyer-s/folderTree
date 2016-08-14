***Now on Github: [https://github.com/WMFO/Watchdog](https://github.com/WMFO/Watchdog "https://github.com/WMFO/Watchdog")***

**The rest of this page is historical.**

### TODO: Update Info to watchdog2

We are now using Watchdog2. The original script no longer works. This page needs to be updated to reflect the new version of the script.

### Overview

The watchdog process is started at reboot by cron on ThinWhiteDuke. (root's crontab) Every 3 seconds it checks for the existence of processes relating to:

-   Shoutcast Server
-   Listenbotv2
-   Mounting of /var/snd and /var/import
-   Rivendell Daemons

 

If there is a process or mountpoint missing, it attempts to start the missing elements. Because it is always checking for the correct functioning of the server, it is not necessary to start services relating to the above elements as watchdog will start them itself. It is not recommended to attempt to start them at start up, as this may spawn duplicate processes.

 

Relevant Files

On ThinWhiteDuke:

-   /opt/wmfo/watchdog/watchdog2.sh
-   /opt/wmfo/watchdog/start-listenbot.sh
-   Various startup scripts for wmfo services.

 

Automatic Startup

In root's crontab on ThinWhiteDuke.

"@reboot /opt/wmfo/watchdog/watchdog2.sh /var/log/watchdog2.log"

 

Misc.

The reason that \`export PATH=blahblahblah\` line is present in the watchdog script is because when scripts are run from cron, the regular user environment is not set. By exporting the PATH variable (not just setting it), the correct path is set for all the scripts called by watchdog.sh. In fact, if watchdog has been started by cron (i.e. automatically and not by some developer) then all the scripts it calls to start various services will fail if that line is not included.

1.  1. [TODO: Update Info to watchdog2](#TODO:_Update_Info_to_watchdog2)
2.  2. [Overview](#Overview)

