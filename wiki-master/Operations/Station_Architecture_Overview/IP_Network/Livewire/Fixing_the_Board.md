This is your crazed 3AM guide to getting WMFO back on the air after an unexpected power outage or freezeup of the Studio A board.

1.  Bypass the board. Change COND1 (192.168.0.110) Destination 8 to 10300 (SA-RD-Main) or 13500 (SC-Pgm1). Send out audio on that source.
2.  Visit 192.168.1.20 and login. Go to the outlet control page and execute a "reboot immediate" operation which will unplug power for 30 seconds.
3.  Attempt to communicate with the board after about 2 mintues on 192.168.1.160. If you get a webpage, you can continue. Otherwise, try shutting off the board for an extended period (10 minute maybe). We think it may be a thermal problem.
4.  If the rightmost 4 faders aren't on, lift up the back of the board and disconnect the ethernet line running to them (it is located on the far right if you're looking at the back). If they say `INACTIVE`, hold `*` and `2` until they say `CAPTURE`, then hit the return key on the board.
5.  Remember if you put the phones on Studio C's board that they can only be on one board at a time. You'll have to remove them before they'll work properly in Studio A.
6.  Once you are confident the board is up (do the phone faders show dots?), restore COND1 destination 8 to 10500 (CONSE1-Pgm1). Lock up and go home.
7.  If you can't get the board up but are good to go in Studio C, lock the door to A and leave a note on it, and consult the ops list.
8.  If board failure is preventing us from broadcasting, and you have no other contacts or ideas, call Axia 24 hour support at (800) 552-8227.

 

Do not power cycle the Furman because this takes down the analog node too, and one time the board did not like not having it. The Element power supply and Studio Enginer should be power cycled as a pair, but if you can get to the Element web page you may be able to reboot it gently. The rightmost 4 faders are a diferent style module than the others (in order to answer the phones) and for some reason they don't come up as cleanly as the others. Also, it appears that the Studio C board is more likely to come up cleanly after a power outage (it's newer and the hardware is in one place) so you can generally stick the DJ in there while you work. You can even do the changeover (step 1) [remotely](https://wiki.wmfo.org/Operations/Credentials/Remote_Access "Remote Access").

*
