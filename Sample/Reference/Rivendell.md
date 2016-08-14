WMFO runs Rivendell as its primary radio automation and playout softeware. This page briefly lists resources maintained by the Rivendell community, and then explains WMFO's technical setup in some detail. Many custom scripts interact with Rivendell in some way, with this page providing an "ecosystem" level view; full information can be found on Github. Finally, this page provides instructions for installing and updating Rivendell.

General References
------------------

In general, Rivendell documentation can be incomplete and out of date. While you should do the background reading, direct specific questions to the ops list and then the Rivendell mailing list.

-   [Rivendell Website](http://www.rivendellaudio.org/ "http://www.rivendellaudio.org/") - General Information, Links, and Downloads
-   [Rivendell Wiki](http://rivendell.tryphon.org/wiki/Main_Page "http://rivendell.tryphon.org/wiki/Main_Page") - Dynamic Community Generated Documentation
-   [Rivendell Mailing Lists](http://lists.rivendellaudio.org/mailman/listinfo/ "http://lists.rivendellaudio.org/mailman/listinfo/") - Active Rivendell User and Development Discussion, greate place to get help just be polite
-   [Rivendell Operations Guide](http://rivendell.tryphon.org/wiki/Rivendell_Operations_Guide "http://rivendell.tryphon.org/wiki/Rivendell_Operations_Guide") - Link goes to wiki which will have the latest version

 

Installing and packages (see in-house documentation below first):

-   [Rivendell 2 + Ubuntu Tutorial](http://www.thevoiceasia.com/rivendell/Rivendell_2_on_Ubuntu_1104.pdf "http://www.thevoiceasia.com/rivendell/Rivendell_2_on_Ubuntu_1104.pdf") - HowTo Guide for Rivendell 2 + Ubuntu ([Static PDF Copy](https://wiki.wmfo.org/@api/deki/files/377/=Rivendell_2_on_Ubuntu_1104.pdf "https://wiki.wmfo.org/@api/deki/files/377/=Rivendell_2_on_Ubuntu_1104.pdf") Attached Below)
-   [Rivendell + Ubuntu Packages](http://projects.tryphon.eu/blog/2011/10/18/rivendell-2-beta-debian-ubuntu-packages/?utm_source=rivendell-prog&utm_medium=email&utm_campaign=rivendell-2.0.2-1-preview "http://projects.tryphon.eu/blog/2011/10/18/rivendell-2-beta-debian-ubuntu-packages/?utm_source=rivendell-prog&utm_medium=email&utm_campaign=rivendell-2.0.2-1-preview") - Beta Version Packages Maintined as of 10/21/11
-   [AukonDK: Rivendell install guide](http://blog.aukondk.com/2014/02/rivendell-install-guide.html "http://blog.aukondk.com/2014/02/rivendell-install-guide.html") - Install packages on Xubuntu, 2/12/14

WMFO Setup
----------

An overview of WMFO's Rivendell system setup. This is a technical guide to Rivendell, not a user's guide.

### Architecture

WMFO uses Rivendell in a distributed architecture setup with multible servers and one or more clients.

#### Servers

-   ***ThinWhiteDuke*** - Our primary Linux server, also our primary Rivendell server. Resides in Control. It can be used for playback under the separate user account *duke-rivendell* but this requires bypassing Studio A (presumably nonfunctional) in the LiveWire config. More importantly, it hosts the following components of the Rivendell System:
    -   mysql database (containing song metadata)
    -   Import and Autoimport systems
    -   ASI soundcard (see below)
    -   Primary Audio Engine
-   ***Supertramp & Smoothcriminal*** -  Host the [Data Stores](https://wiki.wmfo.org/Operations/Station_Architecture_Overview/Computers/Data_Store "Data Store") that provide the file storage backend for the Rivendell system. These file stores are mounted to ThinWhiteDuke via [Samba](http://www.samba.org "http://www.samba.org"). Also provide backup store locations for mysql database, etc. Supertramp resides in Control, while Smoothcriminal resides in the annex.
-   A long term project is to create a third fileserver to reside in Ballou next to the transmitter ("the tower server"). It would keep an offsite backup of the library, and be able to play automation if silence is detected from Curtis. (Ballou has a backup generator.)

#### Clients

-   ***Studio A (TinMachine)*** - Primary Studio RDAirPlay client system. Plays audio to Livewire network via the RD engine on ThinWhiteDuke using the ASI Soundcard.
-   ***Studio C (Coulton)*** - Secondary Studio RDAirPlay client system. Also plays audio to Livewire network via the RD engine on ThinWhiteDuke using the ASI Soundcard.
-   ***MD Office (Floodland)*** - Primary RD import and ripping station. Imported files are kept the in the data stores.

#### ASI SoundCard

WMFO uses the [AudioScience](http://www.audioscience.com/ "http://www.audioscience.com/") HPI [Livewire Soundcard](http://www.audioscience.com/internet/products/livewire/asi6585_asi6685.htm "http://www.audioscience.com/internet/products/livewire/asi6585_asi6685.htm") [CONASI1](https://wiki.wmfo.org/Operations/Station_Architecture_Overview/IP_Network/Livewire/Axia_Normal_Tables/CONASI1 "CONASI1") for audio playback into the Livewire network. It is a PCI card located inside ThinWhiteDuke; the LiveWire network treats it much like a node and the OS largely ignores it (e.g. it does not appear on `ifconfig`). All audio orginates from this card; the audio capabilties of the DJ computers are irrelevant. This is an alternative "adapter" to JACK; you can safely ignore references to that. The soundcard requires a special driver, information on which can be found below. For Rivendell you will be concerned with the card's Livewire sources. (One destination is used for the webstream.)

Each computer that has Rivendell installed on it is known as a host. (This is in contrast to machines that host file shares and through mounting become invisible.) Hosts are configured using rdadmin-\>manage hosts. This is where the clients are told the database resides on ThinWhiteDuke and not locally. The RDAirplay button for each host brings up a screen where each Rivendell audio out can be routed. The port is equal to the ASI source number minus 1, so port 0 is source 1. Typically we put the main and soundpanel out on one source, both auxes on another, and the preview on a third. ThinWhiteDuke's audio is all a single source. The card/adapter number is always 0 (we have only one adapter) and it can be viewed in RDAdmin (a good troubleshooting tip, make sure it's there).

Prior to getting the card, Rivendell out was done from Tinmachine's  S/PDIF and the webbrowser was done via analog. We've since switched the webbrowser over to digital but the analog out is still connected. If the card ever fails, you can return to this system as a backup.

##### Virtual GPIO

The soundcard also provides eight channels of GPIO. 

Virtual GPIO is used for two purposes: first, GPIO signals travel from Rivendell to the Element to trigger the Rivendell Monitoring on rdairplay's button press. In this manner, pressing Play on the rdairplay search box triggers the headphones to switch to the respective RD Preview. There are four Macro carts (two for SA and two for SC) that trigger the GPIO, which is sent to the board over the first two channels on the Tower ASI card.

The third and fourth channel correspond to the RD Main channels on the TOWASI1 card for each of SA and SC. They are responsible for shutting off automation if the user presses the off button on the RD Main channel. The automation_OFF.sh script in /opt/wmfo/macro_sh registers the GPI and maps it to the Automation OFF cart. It selects the GPIO switcher based upon a text version of the hostname (and it's case sensitive, so be careful changing the hostname). When the board, which has the RD Main source, has that particular channel shut off, the 5th pin of the GPO from the board registers a pulse. This pulse is used to shut off automation.

You can telnet into the card at port 93 to gain access to the GPIO interface. Commands: ADD GPI and ADD GPO which display the status of each pin whenever they change. A capital letter means it just changed; lowercase means it's been like that. The pins are active low, so hhLhh means pin 3 just became active. You can also do LOGIN and the GPI 2 xxLH to set channel 2 pin 3 to low and pin 4 to high while leaving the others alone. This can (and is) scripted using Rivendell, so `rmlsend GO\ 3\ O\ 8\ 1\ 0\!` will send to matrix 3 an Output on port 8, setting to active, indefinitely. Matrix 3 is the ASI card as configured for Carlos (rdadmin-\>ManageHosts-\>Switchers GPIO). The O is an output of Rivendell and an input of the ASI card. Source 8 is pin 3 on channel 2 (5 pins to a channel). 1 means active so low. 0 means indefinte; you can supply a time in miliseconds.

We use another two channels to turn off automation when the board fader is turned off. The state of automation is recorded by the presence of absence of /var/lock/automation\_is\_on.lock and a blank log is only loaded if the file is present. If the file is not present, this means someone turned off the fader (or clicked the button) when automation was off. Because they could have manually cued songs, we do not overwrite them with a blank log.

### Configuration

#### Processes

These are simply shell commands. Use the `-X` option when ssh'ing in, or better yet use a remote desktop client.

`rdlogin` - Log in as admin to access certain actions in other processes. Credentials documented on the appropriate page. **Remember to log out afterwards**.

`rdlibrary` - modify individual carts and cuts (tracks).

`rdadmin` - modify system-wide configurations, make backups, etc. Password required on startup.

`rdairplay` - DJ interface

`rdlogmanager` - Manage log configuration

`rdlogedit` - View logs (automation schedules)

`caed, ripcd, rdcatchd` - Rivendell [daemons](http://rivendell.tryphon.org/wiki/Rivendell_daemons "http://rivendell.tryphon.org/wiki/Rivendell_daemons")

#### Network Share Mounts

Mounting file shares allows files physically hosted on Supertramp (and backed up on Smoothcriminal) to be logically part of ThinWhiteDuke's file system. Mounts are configured in the rather complicated `/etc/fstab`. The mounts are:

`/var/snd` - (think *sound*) Holds the song data for the entire library. Very large: `ls` and tab completion take several seconds. Name mandated by Rivendell.

`/var/import` - Holds files that have been ripped but not yet imported into Rivendell. Mounted on Floodland as well; most songs go in to `/var/import/automatic/7601XDP`.

`/var/backup` - Holds nightly backups of mysql song metadata, as well website data, under `mysql`.

`/var/PSA` - TinMachine only. Not really part of Rivendell, but since we're on the topic, this is where imported [PSAs](https://wiki.wmfo.org/Operations/Reference_and_Hacks/Music_Department/PSA_Department_Rivendell_Access "PSA Department Rivendell Access") go. 

### Scripts

#### Watchdog

[Watchdog](https://github.com/WMFO/Watchdog "https://github.com/WMFO/Watchdog") is a script that runs on ThinWhiteDuke that ensures the network shares are mounted exactly once and that the daemons are running. It also makes sure the webstream (shoutcast) is running and the NICs are up. It is started on reboot by cron. Watchdog should always be running.

Watchpup is a far simpler script that runs on Tinmachine. All it does is make sure the Rivendell PSA account is properly logged out after a certain amount of time. It is not yet on Github.

#### Import

Ripping is done on Floodland in accordance to Music Department standards. The current import script is run by cron regularly, taking all .wav files in the directory ripped to and putting them in Rivendell. Metadata transfer is done by a specific filename pattern. One project is to revise the importer to make it more robust and its logging more accessible.

Just prior to import, the [Import Logger](https://github.com/WMFO/ImportLogger "https://github.com/WMFO/ImportLogger") records the number of files and CDs newer than 24 hours, as well as the disk space used an available. Currently nothing is done with this information, but it is available for reference and visualization as the data stores become full.

There is interest in creating a script, the File Sanitizer, that verifies tracks prior to import. It could check for non-ASCII characters, malformed filenames, and maybe even inferior quality audio passed off as lossless.

The Lyrics Scraper is run on every song after it is imported, those which has a scheduling code of NULL. If it can find the lyrics it matches a regular expression against them to declare the song SAFE or EXPLICIT, and otherwise as UNKNOWN. This effort may one day be helped by the [Song Flagger](https://github.com/WMFO/Song-Flagger "https://github.com/WMFO/Song-Flagger") (currently incomplete) that allows DJs to reclassify the currently playing song, and system where volunteers can find the lyrics on the web manually. This family of software uses the Notes field to keep track of what (e.g. scraper of a certain version) last tagged the cart.

#### Spinitron and Automation

Songs are logged to Spinitron by [Rivendell-Spinitron Update](https://github.com/WMFO/Rivendell-Spinitron-Update "https://github.com/WMFO/Rivendell-Spinitron-Update"), a C program. It is configured on Tinmachine and Duke only. Eventually it will be modified to only log songs if enabled, at which point it can be deployed to Coulton. Songs will be logged to the last opened playlist if automation is off, and to a Rick Deckard playlist if it is on. This distinction is associated with the "pm" bit in Spinitron's logging API, and is otherwise taken care of by Spinitron. Sometimes songs logged manually are tagged as "Rivendell" by autocomplete, but only Rivendell songs have their cart bumber in the Spinitron Notes field.

The [Automation Scheduler](https://github.com/WMFO/Automation-Scheduler "https://github.com/WMFO/Automation-Scheduler") selects songs randomly from the pool declared SAFE. Its output is the cart number of a clean song every 2 minutes in a file dated two days in the future. Rivendell log processes merge PSAs, promos, and IDs at certain points every hour. IDs are set to play at :00 and will cut off the current song at :03. Clicking "automation on" loads the failsafe log, overwritten by the day's log (which will exist provided the scheduler was run). The scheduler runs on TinMachine but connects to ThinWhiteDuke.

### How To...

#### Start and/or Stop Rivendell

The DJ interface, `rdairplay`, should be in the GUI Launcher and should never be closed.

If you ever get the error message "multiple instances not allowed" when starting a user-facing Rivendell process, first check that it is not running in another desktop. If not, run `ps -A | grep rdprocess` for the process in question to find its PID. Then run `sudo pkill rdprocess` and restart the process. If this is `rdariplay` on TInmachine, sudo will not be required, and you can even direct the DJ to do it over the phone.

If there's no running process, take down the daemons on the terminals and then on duke. Ensure they are not running and kill them by hand in the right order if necessary. Restart Tinmachine. Bring the daemons up on Duke and then tinmachine - hopefully it works now.

#### Import a Track Manually

Barring equipment failure, you should rely on the automatic nightly import system for general music. This procedure is what you'll use for PSAs.

Copy the audio files to a Rivendell computer on which you have GUI access, either at the terminal or a remote desktop client. ssh X forwarding will work but is not reccomended. Log in as an admin or psa using `rdlogin`, then open `rdlibrary`. Click "Add" in the bottom left corner and fill out the info accordingly - all you should have to change is the name and group. Right of the cart field, click "Import/Export" and select the file. Don't bother with metadata import because you're about to fill that out manually on the cart info page. (You create the cart and the import the cut. Carts can have multiple cuts but WMFO does not use this feature.) Be sure to add the "SAFE" scheduler code.

Optionally, open `rdairplay`, click Setup, click a slot on the SoundPanel (right side with the buttons) and add the PSA with a name and color. This requires a restart of `rdairplay` on the Tinmachine terminal to take effect there.

Be sure to log out with `rdlogin` when you're done.

#### View library remotely

Go to [rivendell.wmfo.org](http://rivendell.wmfo.org/ "http://rivendell.wmfo.org/"). The code is on [GitHub](https://github.com/WMFO/Rivendell-Metadata "https://github.com/WMFO/Rivendell-Metadata").

#### Add/Remove/Verify SMB Mounts

One sanity check for the mounts is to run `df` on ThinWhiteDuke, which should include:

`\\\\<SuperIP>\\Rivendell-Super    17577991160 xxxxxxxxxxx yyyyyyyyyy  zz% /var/snd \\\\``<SuperIP>``\\tobeImported-Super 17577991160 ``xxxxxxxxxxx yyyyyyyyyy  zz%`` /var/import \\\\``<SuperIP>``\\Backup-Super       17577991160 ``xxxxxxxxxxx yyyyyyyyyy  zz%`` /var/backup`

Where x is the amount used, y is the amount available, and z is the use percentage. They should be identical across mounts. The 17 number is the capacity of the array.

Watchdog ensures the mounts are mounted exactly once.

#### Recompile the ASI driver

**DKMS has been set up (see next section) and you shouldn't have to do this manually anymore. But in case you do...**

Every time ThinWhiteDuke's kernel is updated, the driver for the ASI soundcard needs to be recompiled. (We have tried and failed to set up DKMS.) When Duke is updated, you'll need to find a DJ willing to do without archives, Rivendell, and webstream. Close `rdairplay` clients, and take down the daemons on all Rivendell machines using

`sudo /etc/init.d/rivendell stop`

Then run the typical

`sudo apt-get update` then `upgrade` then `dist-upgrade`

on ThinWhiteDuke. Power cycle. Now that you're on the new kernel,

`cd ~/Downloads/hpklinux-4.10.15`

`make clean`

`./configure CFLAGS=-DHPI_BUILD_INCLUDE_DEPRECATED` (the flags are probably not necessary, but...)

`make`

(Make sure there is no errors in the build.)

`sudo make install`

(Restart ThinWhitDuke one more time.)

 

It may take a minute or two for the webstream to come up. Once it is, run

`./etc/init.d/rivendell start`

on all all Rivendell machines. If possible test in C before declaring it good in A.

 

If things don't go smoothly, you can debug with

`sudo asihpi``test`

#### Building the ASI driver using DKMS

 

DKMS has been set up for the ASI driver on Duke. 

Source code goes in  /usr/src/asihpi-4.10.15/

Make directives and kernel location are specified in the dkms.conf in this folder. Current settings:

 

> PACKAGE\_NAME="asihpi"

> PACKAGE\_VERSION="4.10.15"

> SOURCE\_DIR\_NAME="asihpi-\${PACKAGE\_VERSION}"

> CLEAN="make clean"

> MAKE[0]="sh ./configure CFLAGS=-DHPI\_BUILD\_INCLUDE\_DEPRECATED && make"

> BUILT\_MODULE\_NAME[0]="asihpi"

> BUILT\_MODULE\_LOCATION[0]="./drv/"

> DEST\_MODULE\_LOCATION[0]="/kernel/extra/asihpi"

> AUTOINSTALL="yes"

 

To build the module:  sudo dkms build -m asihpi -v 4.10.15

To install the module: sudo dkms install -m asihpi -v 4.10.15

 

Modify the mySQL database

If possible, avoid direct modifications to the database. Use `rdlibrary` instead.

However, scripts and occaisonal batch changes need to operate at the sql level. After logging in (see [credentials](https://wiki.wmfo.org/Operations/Credentials/Internal_Credentials#mysql_credentials "Internal Credentials")) the following commands may be useful:

`use Rivendell;`

*Run this before anything else*

 `describe CART;`

*See fields of the CART table*
  

`select TITLE, ALBUM from CART where ARTIST = "The Doors";`

*See all songs by The Doors*

 `select distinct SCHED_CODES, COUNT(*) from CART group by SCHED_CODES;`

*S**ee a list of scheduler codes and how many carts have each on**e*
  

`select distinct USER_DEFINED, COUNT(*) from CART group by USER_DEFINED ORDER BY COUNT(*);`

*S**ee a list of genres and how many carts are in each, in order*
  

`update Rivendell.CART set SCHED_CODES = "SAFE       ." where SCHED_CODES = "CLEAN      .";`

C*hange songs marked CLEAN to SAFE*
  

`` UPDATE `Rivendell`.`CART` SET `ARTIST` = CONCAT ("The ", REPLACE (`ARTIST`, ", The", "")) WHERE `ARTIST` LIKE "%, The"; ``

`` UPDATE `Rivendell`.`CART` SET `ARTIST` = REPLACE (`ARTIST`, ", the", "") WHERE `ARTIST` LIKE "%, the"; ``

*Used together, change artists like "Doors, The" and "Doors, the" to "The Doors"*
  

`exit`

*Guess.*

A note of scheduler codes: Each *must* be 11 characters long followed by a period. Create new ones in `rdadmin` first. Rivendell permits multiple scheduler codes per cart but WMFO schema does not.

#### Remove Duplicates

First create the group DUPLICATES in `rdadmin`, if it does not already exist. Then log into mysql as root. At the mysql prompt,

`use Rivendell;`

`call duplicates();`

`exit`

 

The procedure will take a few minutes. Log in to `rdadmin` and delete the DUPLICATES group, which will delete everything in it (tha'ts good). This will take several minutes. Recreate the group.

Duplicate cart removal is not automated and should be done every 6 months or so. The script detects exact duplicates (title, album, artist, length) and yes, it keeps one copy.

#### Run donations PSAs in automation

Configure the logs using `rdlogmanager`. There should be a clock set up for donations, which you need to place into the schedule. Using `rdlogedit`, you can view the upcoming logs and make sure that the donations PSAs start on the right days. It may be necessary to delete and rebuild the logs for days during or after the drive.

#### Backup/restore the mySQL Database

Backups are done nightly automatically by a ThinWhiteDuke cron job calling `/opt/wmfo/mysql_backup/backup.sh`. This script is readable only by root as it contains sensitive credentials, but essentially it creates one backup of all mySQL database and one of just the Rivendell database. These `.bz2` files named with the date and placed in `/opt/wmfo/mysql_backup/backups/`. Then they are copied to `/var/backup/mysql`, which is part of the large data store on Supertramp and Smoothcriminal.

The master mySQL database is located on ThinWhiteDuke, and therefore you should use the local backups (provided ThinWhiteDuke is functioning). Unzip the backups using `bunzip2`. Depending on the situation, you may need to modify a *copy* of the sql file by hand. (If you are restoring a mySQL database other than Rivendell, this is a must! Do not overwrite the Rivendell database to fix the training or DJ info website!) Then have mysql read the unzipped backup from standard in.

You will then need to detect which music data files are no longer referenced by the mysql database, delete them, and re-rip CDs from the backup date used. You should probably disable autoimport until you have the system stabilized.

If ThinWhiteDuke fails, all Rivendell data is backed up to the file servers, but you'll need to rearchitect the system on the fly and change a number of settings in RDAdmin and conf files referencing ThinWhiteDuke's IP.

Build Rivendell from Source
---------------------------

Not every release of Rivendell need be installed. Unless there is a new feature or bug fix desired, or a new machine added, it's quite fine to update Rivendell infrequently. Updates are released every few months on no set schedule.

Although this guide is intended to be as bullet-proof as possible with explicit shell commands, stay alert and don't dismiss anything unexpected.

##### Rebase wmfo-patches

We maintain [a fork](https://github.com/WMFO/rivendell "https://github.com/WMFO/rivendell") of Rivendell with our patches applied on top. You'll need to update the fork to have the patches sit on Rivendell's latest version.

This section assumes no familiarity with git. Those in the know can figure out what's going on.

`git clone https://github.com/WMFO/rivendell.git`

`cd rivendell`

`git pull origin master`

`git remote add upstream https://github.com/ElvishArtisan/rivendell.git`

`git pull upstream master`

`git push origin master # optional but nice to keep our master up to date`

`git checkout wmfo-patches`

`git rebase master # or release number or commit`

`# resolve any conflicts...`

`git push -f origin wmfo-patches`

Now our fork is ready for download and use.

#### For New Installs

**MAKE SURE YOU HAVE THE CORRECT VERSION OF RIVENDELL**

**IF THE VERSION OF RIVENDELL BEING INSTALLED DIFFERS FROM THE VERSION ON DUKE, ALL WILL GO TO HELL**

This apt-get command downloads and installs all dependencies. It is based on [what's available](http://rivendell.tryphon.org/wiki/Compiling_Rivendell_from_Source "http://rivendell.tryphon.org/wiki/Compiling_Rivendell_from_Source") at the Rivendell wiki with packages added from experience. If you do have to go hunting for a new package, get it from Ubuntu's package servers (google "ubuntu" and the package name and look for ubuntu URLs), get the -dev version if one exists, and make a note of it here.

First, follow [these instructions](http://debian.tryphon.eu/ "http://debian.tryphon.eu/") to add lines to `/etc/apt/sources.list` which allow you to access Tryphon's copy of QT3, Rivendell's windowing system.

\# This is the source for rivendell files from tryphon
 \# [http://projects.tryphon.eu/blog/2012...heezy-and-sid/](http://projects.tryphon.eu/blog/2012/10/12/qt3-backport-for-debian-wheezy-and-sid/ "http://projects.tryphon.eu/blog/2012/10/12/qt3-backport-for-debian-wheezy-and-sid/")
 deb [http://debian.tryphon.eu](http://debian.tryphon.eu "http://debian.tryphon.eu") trusty main contrib
 deb-src [http://debian.tryphon.eu](http://debian.tryphon.eu "http://debian.tryphon.eu") trusty main contrib

Execute:

wget -q -O - [http://debian.tryphon.eu/release.asc](http://debian.tryphon.eu/release.asc "http://debian.tryphon.eu/release.asc") | sudo apt-key add -

Then run apt-get update, then:

`` sudo apt-get install build-essential autoconf automake libtool libqt3-* qt3-dev* qt3-qtconfig libid3-dev libflac-dev linux-headers-`uname -r` libogg-dev libvorbis-dev libasound2-dev libsamplerate0-dev libjack-dev libmad0-dev libmp3lame-dev libflac-dev libflac++-dev libcurl4-openssl-dev libmadlib-dev libsndfile1-dev  libcdparanoia-dev libpam0g-dev mysql-server `` qt3-\* libsoundtouch-dev

 E: Unable to locate package twolame-dev
 E: Unable to locate package pam-dev

 

You will be prompted to set a password for mysql, set the password to the root password of that computer.

 

Next run the following commands to create the `src/qt-bin` directory.

 

`mkdir -p ~/src/qt-bin`

`cd ~/src/qt-bin`

`ln -s /usr/bin/designer-qt3 designer`

`ln -s /usr/bin/lrelease-qt3 lrelease`

`ln -s /usr/bin/lupdate-qt3 lupdate`

`ln -s /usr/bin/moc-qt3 moc`

`ln -s /usr/bin/qmake-qt3 qmake`

`ln -s /usr/bin/qtconfig-qt3 qtconfig`

`ln -s /usr/bin/uic-qt3 uic`

 

Create the Rivendell user and group:

 

sudo adduser --system --group rivendell

 

Copy an existing /etc/rd.conf and install it. Make sure you don't connect a newer Rivendell version to a different database schema!

Alternatively, you can copy a config file from rivendell/conf/rd.conf-sample and change the host to point to the computer hosting rivendell.

 

**After the install**, create a new host in rdadmin by cloning an old one and setting the IP.

##### For All Installs (Including Upgrades)

Download our clone of of Rivendell and run the autogen script:

 

`cd ~/src`

`git clone https://github.com/WMFO/rivendell.git`

`cd rivendell`

`./autogen.sh`

Make sure you have the correct version of Rivendell: check rivendell/PACKAGE\_VERSION

If git complains that the directory already exists, move it somewhere (you want to be able to reinstall the old version if necessary). The new clone should be on the correct branch, `wmfo-patches`, by the default set on GitHub. From here on, if something goes wrong run `make clean` and start over.

Now run the configure script:

 

`./configure --with-Qt-bin-dir=/home/wmfo-admin/src/qt-bin`

 

Ensure the path points to the real qt-bin, and do not use a relative path. If you're missing packages, this is where you'll find out about them. If you have problems with Qt, make sure the path is correct. On ThinWhiteDuke, ensure that AudioScience HPI is Yes in the config summary.

 

For new installs, you'll need to edit the configuration file in `/etc/rd.conf` to specifiy ThinWhiteDuke's IP as the Hostname (provided that's the case). If the conf file does not exist, copy it from `rivendell-2.5.1/conf/rd.conf-sample`. However you may wish to wait until Duke is upgraded if the new install is a newer version.

Now compile Rivendell. Avoid taxing both of Duke's cores (it runs the webstream) and just run `make`. For every other machine, you'll want to do it in parallel. See how many processors you have:

`cat /proc/cpuinfo | grep -c processor`

And assuming it says 4, run

`make -j4`

And wait 10-20 minutes. You should get this far on every Rivendell machine before installation. 

##### Installing Rivendell

Installing Rivendell needs to happen **simultaneously** across all machines. Bad things can happen if two different versions interact because they expect different metadata mysql database schemas.

Inform the DJ that Rivendell will be unavailable for around 20 minutes.

On ThinWhiteDuke, kill watchdog (it restarts the daemons):

`sudo pkill watchdog2.sh`

Close all Rivendell programs, then kill the daemons on all machines (except new installs):

`sudo /etc/init.d/rivendell stop`

And on ThinWhiteDuke, take down mysql as well:

`sudo /etc/init.d/mysql stop`

Then on each machine, in the Rivendell directory, run

`sudo make install`

to install Rivendell. Once done, on ThinWhiteDuke run these commands:

`sudo cp /usr/local/libexec/* /srv/www/htdocs/rd-bin`

`sudo /etc/init.d/apache2 restart`

`sudo /etc/init.d/mysql start`

`rdadmin`

This copies the web services to Apache, restarts apache, starts mysql, and brings up `rdadmin`. Log in and click okay to any dialogue box asking to update the schema. Quit once you see the main menu (it may be a few minutes of apparent inactivity).

Bring up the daemons on the other machines using 

`sudo /etc/init.d/rivendell start`

(Last time opening rdadmin on ThinWhiteDuke took care of this but if not do this first.)

You can confirm the daemons are or are not running at any time using

`ps -e |grep caed`

Restart watchdog on ThinWhiteDuke using 

`sudo nohup /opt/wmfo/watchdog/watchdog2.sh /var/log/watchdog2.log &`

Confirm that playback and Spinitron logging work. If Spinitron logging does not work, try recompiling and installing from source in the `~/scripts` directory.

If you get scary segfaults when clicking around in `rdairplay` or other processes, try rebooting.

Be on the lookout for hiccups with the automation scheduler for the next few days. You can view logs for upcoming days using `rdlogedit`.

Best practice is to send an email to the staff list telling them to be on the lookout for any strange behaviour.

### Restart Rivendell Remotely

If the rivendell fader on the board in studio A is on and up, but for instance the computer has crashed, you can execute a reboot (either over SSH or via the SA PDU hard plug pulling) and once the computer has booted:

    rmlsend EX\ 999998\!

as wmfo-dj (so you'll have to run:

    su wmfo-dj

and enter the password if logged in remotely as wmfo-admin.

1.  1. [General References](#General_References)
2.  2. [WMFO Setup](#WMFO_Setup)
    1.  2.1. [Architecture](#Architecture)
        1.  2.1.1. [Servers](#Servers)
        2.  2.1.2. [Clients](#Clients)
        3.  2.1.3. [ASI SoundCard](#ASI_SoundCard)
            1.  2.1.3.1. [Virtual GPIO](#Virtual_GPIO)

    2.  2.2. [Configuration](#Configuration)
        1.  2.2.1. [Processes](#Processes)
        2.  2.2.2. [Network Share Mounts](#Network_Share_Mounts)

    3.  2.3. [Scripts](#Scripts)
        1.  2.3.1. [Watchdog](#Watchdog)
        2.  2.3.2. [Import](#Import)
        3.  2.3.3. [Spinitron and Automation](#Spinitron_and_Automation)

    4.  2.4. [How To...](#How_To...)
        1.  2.4.1. [Start and/or Stop Rivendell](#Start_and.2For_Stop_Rivendell)
        2.  2.4.2. [Import a Track Manually](#Import_a_Track_Manually)
        3.  2.4.3. [View library remotely](#View_library_remotely)
        4.  2.4.4. [Add/Remove/Verify SMB Mounts](#Add.2FRemove.2FVerify_SMB_Mounts)
        5.  2.4.5. [Recompile the ASI driver](#Recompile_the_ASI_driver)
        6.  2.4.6. [Building the ASI driver using DKMS](#Building_the_ASI_driver_using_DKMS)
        7.  2.4.7. [Remove Duplicates](#Remove_Duplicates)
        8.  2.4.8. [Run donations PSAs in automation](#Run_donations_PSAs_in_automation)
        9.  2.4.9. [Backup/restore the mySQL Database](#Backup.2Frestore_the_mySQL_Database)

3.  3. [Build Rivendell from Source](#Build_Rivendell_from_Source)
    1.  1.  1.  3.1.1.1. [Rebase wmfo-patches](#Rebase_wmfo-patches)

        2.  3.1.2. [For New Installs](#For_New_Installs)
            1.  3.1.2.1. [For All Installs (Including Upgrades)](#For_All_Installs_(Including_Upgrades))
            2.  3.1.2.2. [Installing Rivendell](#Installing_Rivendell)

    2.  3.2. [Restart Rivendell Remotely](#Restart_Rivendell_Remotely)


[Page Attachments](https://wiki-files.wmfo.org/Operations/Station_Architecture_Overview/Rivendell)
