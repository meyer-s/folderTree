***Now maintained on Github: ***[https://github.com/WMFO/Automation-Scheduler](https://github.com/WMFO/Automation-Scheduler "https://github.com/WMFO/Automation-Scheduler")

Overview
--------

The automatic log generation for Rivendell is done on TinMachine. Due to the scheduling algorithm for Rivendell being O(n\^2), we use our own custom scheduler. Rivendell allows you to generate a schedule (placing PSAs and such) and placing music from an outside music scheduler into place-holder spots. This is what we do basically. Rivendell schedules placeholders for all the actual music but places specific PSAs and IDs in the schedule. Then, the music from WMFO's custom scheduler is "merged" in. See the Rivendell documenation for more info on using custom schedulers.

Relevant Files
--------------

On TinMachine:

-   /opt/wmfo/scheduler/scheduler (also see source files in the same directory)
-   /opt/wmfo/scheduler/logs (directory to hold output from custom scheduler to be imported into Rivendell)
-   /opt/wmfo/scheduler/logs/generate\_log.sh

Automatic Run
-------------

root's cronab on TinMachine

"0 15 \* \* \* /opt/wmfo/scheduler/logs/generate\_log.sh"

 This script calls the WMFO scheduler to generate 24 hours of random song selections and places the result in the logs directory. Then the rdlogmanager Rivendell utility is called and the Rivendell log is created. Logs are generated two days in advance.

Misc
----

The custom scheduler requires mysql++ to compile.

You'll notice some setting of the DISPLAY variable in generate\_logs.sh. rdlogmanager requires this for automatic log generation. This requirement was dropped in the next version of Rivendell.

1.  1. [Overview](#Overview)
2.  2. [Relevant Files](#Relevant_Files)
3.  3. [Automatic Run](#Automatic_Run)
4.  4. [Misc](#Misc)

