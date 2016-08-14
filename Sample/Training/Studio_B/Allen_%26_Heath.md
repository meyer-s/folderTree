The Studio B Allen & Heath is the primary mixing board. Its wiring, and therefore signal flow, is documented below. 

The board is a GL2800 with 22 mono channels and powered by a RPS11. The manual is attached towards the bottom of the page; in particular, fader controls start on page 16, and the routing table below is best understood by looking at page 7.

The ICE-16 interface is also made by Allen & Heath, and receives the 16 direct-outs from the channels with mics. Because of the ASIO spec, the FastTrack and ICE cannot be used simultaneously. To switch in Repear, open Preferences with Ctrl-P, and go to Devices on the left. Select ASIO, and then select the desired interface. When switching to the ICE, you'll want to set the "last" to 16.

Aux Outputs
-----------

||
|**\#**|**Direct Dest.**|**Normaled Dest.**|**Type**|
|1|DEE SNAKE 19|-|MONO|
|2|DEE SNAKE 20|-|MONO|
|3|P2 19|LW 12002 L|MONO|
|4|P2 20|LW 12002 R|MONO|
|5|P2 21|SPX9000|MONO|
|6|P2 22|SPACESTATION|MONO|
|7|P2 23|DUAL1|MONO|
|8|P2 24|DUAL2|MONO|
|9-10|DEE SNAKE 17+18|-|STEREO|

 

Signal Flow Diagrams
--------------------

-   [Recording Diagram](https://docs.google.com/a/wmfo.org/drawings/d/1bxb7D8bJwV_rtJ89UhXMAMmxQz1uh7WE16bpH7ruKg0/edit "https://docs.google.com/a/wmfo.org/drawings/d/1bxb7D8bJwV_rtJ89UhXMAMmxQz1uh7WE16bpH7ruKg0/edit")
-   [Playback Diagram](https://docs.google.com/a/wmfo.org/drawings/d/10JwPqQPqzOd74Dkx0uNSCMqzbUqjKEMzD4O-wkuWVOM/edit "https://docs.google.com/a/wmfo.org/drawings/d/10JwPqQPqzOd74Dkx0uNSCMqzbUqjKEMzD4O-wkuWVOM/edit")

Fader Inputs
------------

These tables are done "upside-down", from the perspective of someone leaning over the top of the board.

||
| |**1**|**2**|**3**|**4**|**5**|**6**|**7**|**8**|
|**MIC IN**|DEE 1|DEE 2|DEE 3|DEE 4|DEE 5|DEE 6|DEE 7|DEE 8|
|**LINE IN**|-|-|-|-|-|-|-|-|
|**INSERT**|INS1 1|INS1 2|INS1 3|INS1 4|INS1 5|INS1 6|INS1 7|INS1 8|
|**DIRCT OUT**|ICE 1|ICE 2|ICE 3|ICE 4|ICE 5|ICE 6|ICE 7|ICE 8|

 

 

**9**

**10**

**11**

**12**

**13**

**14**

**ST15**

**ST16**

**MIC IN**

DEE 9

DEE 10

DEE 11

DEE 12

DEE 13

DEE 14

-

-

**LINE IN**

P2 5

P2 6

P2 7

P2 8

P2 9

P2 10

P1 17 (L)
 P1 18 (R)

P1 19 (L)
 P1 20 (R)

**INSERT**

INS1 9

INS1 10

INS1 11

INS1 12

INS1 13

INS1 14

**DIRCT OUT**

ICE 9

ICE 10

ICE 11

ICE 12

ICE 13

ICE 14

-

-

 

||
| |**17**|**18**|**19**|**20**|**21**|**22**|**23**|**24**|
|**MIC IN**|DEE 15|DEE 16|-|-|-|-|-|B MIC|
|**LINE IN**|P1 9|P1 10|P1 11|P1 12|P1 13|P1 14|P1 15|P1 16|
|**INSERT**|INS2 1|INS2 2|INS2 3|INS2 4|-|-|-|-|
|**DIRCT OUT**|ICE 15|ICE 16|-|-|-|-|-|-|

 

Basically: The Dee snake inputs go to 1-14 and 17+18 becasue 15 and 16 are stereo channels. You toggle between the mic in and line in using a switch near the top of the fader; on 1-8 where no line is connected it activates a pad instead. 9-14's line in are normalled to the CD, CDR, and Aux in, and 17-24 are normalled to the FastTrack. Most faders have inserts available, where the audio is routed to an effects processor and then returns to the fader. The 16 mics are routed to the 16 channels on the ICE.

Master I/O
----------

### First Layer

||
|**Stereo In**|**1**|**2**|**3**|**4**|
|**L/M**|P2 1|P2 3|P1 21|P1 23|
|**R**|P2 2|P2 4|P1 22|P1 24|

 

||
|**MTX**|**1**|**2**|**3**|**4**|
|**IN**|-|-|-|-|
|**OUT**|P2 13|P2 14|P1 15|P1 16|

 

**2TRK**

**IN**

**OUT**

**L**

SBRS1
 DEST

-

**R**

-

Lamps: not connected

### Second Layer

**INSERT**

**MONITOR OUT**

**1**

**2**

**3**

**4**

**5**

**6**

**7**

**8**

**L**

**R**

**M**

**L**

**R**

INS1 15

INS1 16

INS1 17

INS1 18

INS1 19

INS1 20

INS1 21

INS1 22

INS1 23

INS1 24

-

NEARFIELD LVL

### Third Layer

TRS aux outs, ascending left to right. Refer to table above for destinations.

TB/GEN OUT: not connected
 OUT M: not connected

### Fourth Layer

**GROUP**

**MAIN**

**1**

**2**

**3**

**4**

**5**

**6**

**7**

**8**

**L**

**R**

P1 1

P1 2

P1 3

P1 4

P1 5

P1 6

P17

P1 8

SBRS1 SOURCE

 

The L/R main outputs are what go to the Studio A board. You can hear what the DJ in there hears on the Std B/Dee fader by pressing the rightmost of the eight horizontal buttons on SBRS1 near the top of the upper rack and plugging in headphones (note that this changes 2TRK). Change it back to the leftmost button (airfeed rereceive) when you are done.

1.  1. [Aux Outputs](#Aux_Outputs)
2.  2. [Signal Flow Diagrams](#Signal_Flow_Diagrams)
3.  3. [Fader Inputs](#Fader_Inputs)
4.  4. [Master I/O](#Master_I.2FO)
    1.  4.1. [First Layer](#First_Layer)
    2.  4.2. [Second Layer](#Second_Layer)
    3.  4.3. [Third Layer](#Third_Layer)
    4.  4.4. [Fourth Layer](#Fourth_Layer)


[Page Attachments](https://wiki-files.wmfo.org/Training/Studio_B/Allen_%26_Heath)

![Allen&Heath.JPG](https://wiki-files.wmfo.org/Training/Studio_B/Allen_%26_Heath/Allen&Heath.JPG)
