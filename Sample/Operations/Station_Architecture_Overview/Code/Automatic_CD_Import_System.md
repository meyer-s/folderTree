The Importer system will, when revised, be hosted on Github. The READMEs there will contain the practical deployment information. This page serves as a design document and arcitectural overview. Its subpages are largely historical.

Contents
--------

-   [Filename Sanitizer](https://wiki.wmfo.org/Operations/Station_Architecture_Overview/Code/Automatic_CD_Import_System/Filename_Sanitizer "Operations/Station_Architecture_Overview/Code/Automatic_CD_Import_System/Filename_Sanitizer")
-   [LyricsFlagger](https://wiki.wmfo.org/Operations/Station_Architecture_Overview/Code/Automatic_CD_Import_System/LyricsChecker "Operations/Station_Architecture_Overview/Code/Automatic_CD_Import_System/LyricsChecker")
-   [Profanity-Detecting Regex](https://wiki.wmfo.org/Operations/Station_Architecture_Overview/Code/Automatic_CD_Import_System/Profanity-Detecting_Regex "Operations/Station_Architecture_Overview/Code/Automatic_CD_Import_System/Profanity-Detecting_Regex")

Design Document
---------------

The music import system is composed of three distinct programs. In order, they are: the File Sanitizer (no longer the file*name* sanitizer), the Importer, and the Lyrics Flagger. All three run daily on Duke, probably by cron job.

Where appropriate, the programs use PID files in /var/run and only run if the file is not found or it contains a process ID that is not in use. Lock files for each individual music file are not necessary. All programs have logs in /var/log/import. The unix mail utility needs to be configured so these programs can report errors, with specifics described below.

The File Sanitizer takes the raw wav files from the ripper and ensures they meet several criteria. These may include having entirely ASCII names, having the right metadata format in the name, and being valid wav binaries. An advanced test would be using signal analysis to weed out lossy formats that have been converted to wav. The sanitzer moves files that pass all the tests (possibly after correcting a fault) to a directory that cannot be written to from Floodland (either by permissions or a separate mount). It moves files that fail any test to another directory. Optionally, it may send out an email when the directory contains a certain number of files. It also moves directories containing only log files left by the ripper to /var/log/import/7601XDP. It removes empty directories in the ripper directory.

The Importer takes the files from the sanitized directory and puts them in to Rivendell. Ben's current implementation needs only minor refinements. Specifically, it needs to use a PID file rather than a lock file per above, and pull only from the sanitized directory. It should also write basic status logs (N number of tracks imported each session, etc). These could be sent to the MD each week, to help keep us aware of the chain working correctly and help us catch issues before the DJs do.

The Lyrics Flagger, version 3, places new music into a scheduler code or group (or both) that classifies it as clean, explicit, or unclassifiable if no lyrics could be found. Automation should pull only from the clean category. It may be possible to patch Rivendell to show explicit music in red when searching. The flagger should fail gracefully: it should detect when the API is unavailable or gives unusually short lyrics listings, and not change the classification of the music (not even to unclassifiable). The flagger should alert the ops list if it fails. An advanced feature is to distinguish between instrumental tracks and tracks who lyrics could not be found. Tentatively, it will use the EchoNest API but should ideally have multiple APIs to fall back on and collate information among them.

The Sanitzer and Importer will be in one git repo, and the lyrics flagger in another. This is because they will be coupled by the sanitized folder, and the Flagger can be used more widely.

Duke root's crontab
-------------------

will be posted here when the project is done.

1.  1. [Contents](#Contents)
2.  2. [Design Document](#Design_Document)
3.  3. [Duke root's crontab](#Duke_root's_crontab)

