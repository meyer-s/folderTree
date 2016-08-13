Before you begin, have this page and the Internal Credntials page open. You will be taking this very wiki offline and not be able to access them.

We've seen Rivendell freeze up during the backup run, most likely due to overtaxing Super's read/write ability, so play something else.

Backing up
----------

1.  Log into Smooth using the Windows credentials, and then into the VM Server Home Page / VMware Infrastructure Web Access using the same credentials. Ignore warnings about certificates.
2.  Take a VM snapshot (click the VM on the left, then under commands on the right).
3.  Shut down the guest OS and power down the VM.
4.  On *Super*, run the Synctoy VirtualMachines2 job to back everything up to the other server.
5.  Power up the wiki VM. The Guest OS should come up automatically (be patient).

 

Updating Software
-----------------

1.  Back up the wiki as described above.
2.  Launch either the VM terminal or SSH into the machine using the [MindTouch\_wikiWMFO credentials](https://wiki.wmfo.org/Operations/Credentials/Internal_Credentials "Internal Credentials").
3.  Follow the directions here for upgrading a VM install:  [Upgrading the wiki](http://developer.mindtouch.com/en/docs/MindTouch_Administration_Guide/Upgrading_MindTouch/Upgrading_MindTouch_VMware_Appliance "http://developer.mindtouch.com/en/docs/MindTouch_Administration_Guide/Upgrading_MindTouch/Upgrading_MindTouch_VMware_Appliance")
    1.  You may need to update some of the system packages using apt-get. Often, you need the *backports* version of a repo to satisfy dependencies. Try *apt-get -t lenny-backports \<command\>* if you have issues.
    2.  Mono 2.10 has been installed from source using the instructions [here](http://developer.mindtouch.com/en/docs/mindtouch_setup/010Installation/020Installing_on_Debian/Installing%2F%2FUpgrading_Mono_on_Debian "http://developer.mindtouch.com/en/docs/mindtouch_setup/010Installation/020Installing_on_Debian/Installing%2F%2FUpgrading_Mono_on_Debian"). If you need to update it, you might also have to build it from source.
    3.  However, when it comes to actually run *updateWIki.sh*, you'll want to become root (run *su*) first.

4.  Test to ensure everything is working (except openID).
5.  If it works, go to step 7.
6.  If it's broken, revert the VM snapshot so everything works again and see if you can find a solution offline. Then repeat from step 2.
7.  Restart the VM.
8.  Test everything again.
9.  If it works (and make sure it does as this step will be irreversible), make a new backup.
10. If it's broken, revert the VM snapshot so everything works again and see if you can find a solution offline. Then repeat from step 2.

1.  1. [Backing up](#Backing_up)
2.  2. [Updating Software](#Updating_Software)

