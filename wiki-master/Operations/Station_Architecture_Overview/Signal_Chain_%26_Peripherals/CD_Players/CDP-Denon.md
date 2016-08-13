This is the GPIO specification for the Denon DN-C635 & C620 CD Players.

Axia GPIO Profile: Line Input

#### Pin Mapping

**Wire Color**

**Axia Side (D-sub 15)**

**Device Side (D-sub 25)**

**Pin \#**

**Description**

**Pin \#**

**Description**

White Green

7

Source Common

23

Command Common

Green

4

START Pulse

2

PLAY Command

White Orange

NC

-

NC

-

Orange

5

STOP Pulse

3

PAUSE Command

White Blue

NC

-

NC

-

Blue

15

READY Command

16

CUE Tally

White Brown

10

Input Common

22

Tally Power Supply

Brown

NC

Deprecated<sup>1</sup>

NC or 24<sup>1</sup>

EOM Tally (Deprecated<sup>1</sup>)

 

Note 1: Previously WMFO had used the CD player EOM signal to trigger a count-down timer via a second Axia GPIO port. This secondary GPIO port used the Axia "Studio Monitor" GPIO profile on which pin 14 is the countdown timer trigger.  As of the Studio A overhaul in January 2011, we no longer use the EOM signal, nor a second GPIO port, and this wire has been disconnected on the Axia side.  As of July 2012, the CD GPIO cables in Studio A still have this pin wired on the device side. The brown wire on these cables should thus be ignored and must be disconnected on the Axia side to prevent it from interfering with the main CD player GPIO profile.

1.  1. [Pin Mapping](#Pin_Mapping)

