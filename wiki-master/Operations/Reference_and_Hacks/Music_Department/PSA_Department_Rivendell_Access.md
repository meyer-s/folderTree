Overview
--------

The WMFO PSA department has access to the Rivendell system in order to conduct their duties of importing new PSAs into the Rivendell digitial library and placing relevant PSAs on the sound panels of Rivendell.

 

PSA Drive Space
---------------

The PSA department has a personal spot on the Supertramp/Smoothcriminal data shares. It is used for transferring files from the MD computer to a place where a Rivendell program can access them.

 

PSA Accounts
------------

PSA has user accounts on the MD computer, TinMachine (Studio A computer) and its own Rivendell user account. The PSA account on the MD computer (actually a domain account) mounts the PSA share and allows PSA department members to upload new PSAs on to the share. It also has shortcuts to an NX Client (NX is NoMachine, the remote graphical access used to remotely access TinMachine by the PSA department) that will open TinMachine.

 

The TinMachine user account is accessed remotely by the PSA department, either through the MD computer or via their own personal computers. Once logged in, they can import their PSAs using rdlibrary. The can also edit the soundpanels on TinMachine. The PSA Rivendell account grants them the permissions to do this.

 

WatchPup
--------

WatchPup is a script on TinMachine that monitors if someone has logged out of the PSA Linux account. If so, it sets the Rivendell user to the regular default user. In the future it should be expanded for automatic mounting of the /var/PSA directory (which is the mount point for the PSA share on Super/Smooth) and the /var/backup directory. (Although TinMachine does not currently backup anything to it.) These shares are mounted automatically on reboot; it's very rare if ever that they become unmounted (and a reboot will fix it).

1.  1. [Overview](#Overview)
2.  2. [PSA Drive Space](#PSA_Drive_Space)
3.  3. [PSA Accounts](#PSA_Accounts)
4.  4. [WatchPup](#WatchPup)

