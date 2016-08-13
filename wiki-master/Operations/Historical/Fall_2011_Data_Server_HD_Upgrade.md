This is a report of the process used to upgrade our two data servers (SMOOTHCRIMINAL & SUPERTRAMP) from \~10TB RAID5 to \~20TB RAID6 in October of 2011.

#### Initial Status:

As of 9/28 capacity of mirror is at 7.70TB used out of 9.54TB total (in base2 bytes, not base10 bytes).

Super's array:

-   8 - 1.5TB 5400 3.5" Seagate Drives
-   1 - Areca ARC-1220 8 channel RAID controller
-   1 - Areca ARC-6120-3 controller backup battery

Smooth's array:

-   8 - 1.5TB 5400 3.5" Seagate Drives
-   1 - Highpoint RocketRAID 2320

#### Final Status:

As of \<\<end date\>\> capacity of mirror is at \<\<end consumed\>\> used out of 16.3TB total (in base2 bytes, not base10 bytes)

Super's array:

-   8 - 3TB 5400 3.5" Hitachi Drives
-   1 - Areca ARC-1220 8 channel RAID controller
-   1 - Areca ARC-6120-3 controller backup battery

Smooth's array:

-   8 - 3TB 5400 3.5" Hitachi Drives
-   1 - Areca ARC-1220 8 channel RAID controller
-   1 - Areca ARC-6120-3 controller backup battery

#### Upgrade Process:

1.  ~~Stop all ripping to tobeImported~~
2.  ~~Wait for auto import to finish the backlog and confirm autoimport complete.~~
3.  ~~Review remaining files~~ and fix import so all files are properly imported
4.  ~~Install temp local storage in MD computer (FLOODLAND)~~
5.  ~~Resume ripping to temp storage~~
6.  ~~Complete mirror/backup from Super to Smooth using existing SyncToy jobs~~
7.  ~~Turn off automatic running of sync toy (scheduled script job)~~
8.  ~~On Super: check for and backup to Smooth any files on data disk that are needed but not included in SyncToy jobs~~
9.  ~~Backup webcontent (wiki, mySQLs, etc) from Smooth to Super~~
10. ~~On Smooth: check for and backup to Super any files on data disk that are needed but not included in SyncToy jobs~~
11. ~~Create a VM snapshot image of the wiki and backup to Super (from within VMware Server)~~
12. ~~Move wiki VM to Smooth system disk (if not already there)~~
13. ~~Disable data share write access on Super (not required, but may be wise if not too much trouble. Also, you need to confirm that doing this won't break the Rivendell auto log generation or any other logging (EAS, telemetry, etc)...)~~
14. Upgrade Smooth (annex server)
    1.  ~~Confirm Super array is stable (all 8 drives good), and stabilize if need be.~~
    2.  ~~Take Smooth off line~~
    3.  ~~Remove & **Label** old drives with corresponding controller port~~
    4.  ~~Replace RAID Card with new ARC-1220 & battery~~
    5.  ~~Boot and confirm ARC-1220 operation~~
    6.  ~~Check for ARC-1220 Firmware updates and install if necessary (Note: needed to install v1.49 (latest) for 3TB support)~~
    7.  ~~Shutdown~~
    8.  ~~Install 8 new 3TB 5400 3.5" Hitachi drives and label with new controller port numbers~~
    9.  ~~Boot and confirm drive installs~~
    10. ~~Build new RAID 6 array from Areca mgmt software (76 hour job)~~
    11. ~~Format partition w/ GPT table and NTFS, 4096 sector size (quick format)~~
    12. ~~Clone Super data to new Smooth array using SyncToy (run job in test mode first to insure no deletes!)~~
    13. ~~Switch Rivendell to Smooth array~~
    14. ~~Switch Rivendell database backups, etc to Smooth Array or Local storage~~
    15. ~~Switch auto logging (EAS, Telemetry, etc) to SmoothArray or Local storage~~
    16. ~~Let cook for 7 days and monitor for errors~~
        1.  drive powersaving settings cause spinup lag issues for Rivendell -\> disable all powersaving on card
        2.  there were issues converting the scripts for Rivendell mounting -\> scripts have been reworked

15. Upgrade Super (control server) (started 10/31)
    1.  ~~Take Super off line~~
    2.  ~~Remove & **Label** old drives with corresponding controller port~~
    3.  ~~Install 8 new 3TB 5400 3.5" Hitachi drives and label with new controller port numbers~~
    4.  ~~Install latest (v1.49 all 4 files using webserver) ARC-1220 Firmware update~~
    5.  ~~Build new RAID 6 array from Areca mgmt software (took 9 hrs!?)~~
    6.  Format partition w/ GPT table and NTFS, 4096 sector size (slow format for insurance)
    7.  Clone Smooth data to Super
    8.  Switch Rivendell back to Super
    9.  Switch Rivendell database backups, etc to Super Array or Local storage
    10. Switch auto logging (EAS, Telemetry, etc) to Super Array or Local storage
    11. Let cook for 7 days

16. Review and confirm or add Super \<-\> Smooth autobackup operations for the following data
    -   See [Data Store](https://wiki.wmfo.org/Operations/Systems/Servers/Data_Store "Data Store") info

17. Run Phil's [filename sanitizer](https://wiki.wmfo.org/Operations/Code/FilenameSanitizer "Filename Sanitizer") on tobeImported\\automatic\\old
18. Set up autoimport system (documentation?) and run on tobeImported\\automatic\\old music files
19. Copy MD temp storage to tobeimported
20. Switch Ripping back to Super
21. Resume full, normal auto import
22. Turn on automatic running of sync toy (scheduled script job, possibly already completed as part of 16)
23. Resume normal operations
24. Document the crap out of the above backup systems, Rivendell setup, and Super/Smooth Rivendell switching process for future generations

 

In the event of a catastrophic failure (2 or more drives down) of the other sever during the process: Halt operation and re-install old drives until other sever is stabilized (using the new drives to fill out the array as necessary).

1.  1. [Initial Status:](#Initial_Status:)
2.  2. [Final Status:](#Final_Status:)
3.  3. [Upgrade Process:](#Upgrade_Process:)

