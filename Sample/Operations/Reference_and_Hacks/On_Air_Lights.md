This is the GPIO specification for the On Air Light control lines.

Up to 4 independent light circuits can be driven from a single Cat6 line. Each circuit uses its own D-sub 15 connector.

Control PDU
-----------

The grid is driven by an 8 port serial/contact closure Power Distrabution Unit (PDU), theDataprobe Serial iBootBar sBB-N15 ([manual](http://dataprobe.com/support/manuals/pwr/sbb_v1.0x.pdf "http://dataprobe.com/support/manuals/pwr/sbb_v1.0x.pdf")). The PDU detects GPIO contact closure from the studios and powers on or off outlets that are connected to the on-air lights.

The PDU is configured via serial console with Baud: 115200, Data: 8, Stop: 1, Parity: 0.  Access to this device requries credentials found on the [Internal Credentials Page](https://wiki.wmfo.org/Operations/Credentials/Internal_Credentials "Internal Credentials").

### Configuration

The following table is the current configuration of the device and intended purpose of each port. Currently only outlets 1, 5, and 6 are connected to lights, although all control wiring has been done.

||
|**Outlet \#**|**Name**|**Mode**|**Purpose**|
|1|SA\_Ext|Closed|SA External Light|
|2|SB\_Int|Closed|SB Internal Light|
|3|SC\_Int|Closed|SC Internal Light|
|4|Outlet4|Open|Distro - Always On|
|5|SB/SDee\_Ext|Closed|SB & SDee External Lights|
|6|SC\_Ext|Closed|SC External Light|
|7|Outlet7|Open|Distro - Always On|
|8|Outlet8|Open|Distro - Always On|

### Changing Config

To change the mode of the outlet call: `set outlet <outlet #> control.on <open/closed>`
 Open means the outlet is on when the contact is open, and Closed means the outlet is on when the contact is closed.

The current mode of an outlet can be checked by: `get outlet <outlet #> control.on`

The current status of all outlets can be checked by: `get outlets`

Studio A Driven (connected to SAEGP1)
-------------------------------------

### D-sub Mapping

The D-subs are where the GPIO control signals leave the LiveWire network.

||
|**D-sub \#**|**Lights Controlled**|**Axia GPIO Profile**|
|1|SA External|Control Room Monitor|
|2|SB Internal|Line Input|
|3|SC Internal|Line Input|

### Pin Mapping

**Wire Color**

**Axia Side (D-sub 15)**

**PDU Side (bare wire)**

**Pin \#**

**Description**

**Pin \#**

**Description**

White Green

D1-7

CR ON AIR Lamp

1L

Outlet 1 Contact

Green

D1-8

Source Common

1R

GND

White Orange

D2-1

 ON Lamp

2L

Outlet 2 Contact

Orange

D2-7

Source Common

2R

GND

White Blue

D3-1

ON Lamp

3L

Outlet 3 Contact

Blue

D3-7

Source Common

3R

GND

White Brown

NC

-

NC

-

Brown

NC

-

NC

-

Studio B Driven
---------------

The lights driven by Studio B (B/Dee Externals) are controlled by a physical switch mounted above the board. This switch is driven by a 3 conductor line spliced off of an 8 conductor Cat6 line.

### Pin Mapping

**Wire Color**

**Studio B Side (bare wire)**

**PDU Side (bare wire)**

**Pin \#**

**Description**

**Pin \#**

**Description**

White Green

2 (black wire)

Switch ON 2

5L

Outlet 5 Contact

Green

NC

-

NC

-

White Orange

NC

-

NC

-

Orange

NC

-

NC

-

White Blue

NC

-

NC

-

Blue

NC

-

NC

-

White Brown

(red wire)

LED +

-

SC +5V Supply

Brown

3,4 (bare/silver wire)

Switch Common 1,2

-

SC GND Source

 

Note1: The LED - (negative) line is connected to Switch ON 1.
 Note2: The ground for the Outlet 5 contact is provided by the Studio C PowerStations; this could be reworked using 4 conductor line and making use of the two isolated switch lines provided by the mechanical switch.

Studio C Driven (connected to SCPSA1)
-------------------------------------

### D-sub Mapping

||
|**D-sub \#**|**Lights Controlled**|**Axia GPIO Profile**|
|1|SC External & 5V Supply|Control Room Monitor|

### Pin Mapping

**Wire Color**

**Axia Side (D-sub 15)**

**PDU Side (bare wire)**

**Pin \#**

**Description**

**Pin \#**

**Description**

White Green

D1-1

CR ON AIR Lamp

6L

Outlet 6 Contact

Green

D1-7

Source Common

6R

GND

White Orange

NC

-

NC

-

Orange

NC

-

NC

-

White Blue

NC

-

NC

-

Blue

NC

-

NC

-

White Brown

D1-9

+5V

-

SB Lamp Supply

Brown

D1-8

GND Source

-

SB Lamp GND

1.  1. [Control PDU](#Control_PDU)
    1.  1.1. [Configuration](#Configuration)
    2.  1.2. [Changing Config](#Changing_Config)

2.  2. [Studio A Driven (connected to SAEGP1)](#Studio_A_Driven_(connected_to_SAEGP1))
    1.  2.1. [D-sub Mapping](#D-sub_Mapping)
    2.  2.2. [Pin Mapping](#Pin_Mapping)

3.  3. [Studio B Driven](#Studio_B_Driven)
    1.  3.1. [Pin Mapping](#Pin_Mapping_2)

4.  4. [Studio C Driven (connected to SCPSA1)](#Studio_C_Driven_(connected_to_SCPSA1))
    1.  4.1. [D-sub Mapping](#D-sub_Mapping_2)
    2.  4.2. [Pin Mapping](#Pin_Mapping_3)


