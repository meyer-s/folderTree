Ringo is the primary file server for WMFO.

Architecture
------------

It's currently running the 14.04 LTS of Ubuntu.

The main RAID is installed on top of 8x6TB WD Red drives. These are all grouped under a single RAIDZ share using the ZFS filesystem.

Services
--------

Ringo exposes several shares over Samba:

-   Rivendell: mounted only on Duke
-   tobeImported: mounted on Floodland for ripping and Duke for import
-   Backup: mounted on Duke and Devolution for backups

 

Ringo has an IPMI interface for out of band reboots and an external NIC. 

1.  1. [Architecture](#Architecture)
2.  2. [Services](#Services)

