Studio B Analog Node 1
----------------------

**Credential Level:** Engineer
 **[IP Address](https://wiki.wmfo.org/index.php?title=Operations/Diagrams_%26_Tables/IP_Address_Space "IP Address Space"):** 192.168.2.100

See [Axia Normal Tables](/Operations/Diagrams_%26_Tables/Axia_Normal_Tables "Operations/Diagrams_%26_Tables/Axia_Normal_Tables") page and [Diagrams & Tables](https://wiki.wmfo.org/index.php?title=Operations/Diagrams_%26_Tables "Diagrams & Tables") page for keys and abbreviation information.

Note: P2 means "Patch 2" but refers to the bottommost of the [patch bays](https://wiki.wmfo.org/Training/Studio_B/Patch_Bays "Patch Bays"). The top two are insert bays.

Note: This table is arranged slightly differently than the others to display the normaled sources and destinations on the patch bays. "Normaled" means that the signal flows to the sources or from the destinations when no patch cables are inserted. On these tables only, tick marks for "Direct Device" indicate that the name of the source gives the relevant information.

### Sources:

||
|**Port**|**Name**|[**Channel**](https://wiki.wmfo.org/index.php?title=Operations/Diagrams_%26_Tables/LW_Address_Space "LW Address Space")|**Shareable**|**Mode**|**Gain**|**Direct Device**|**Normaled Source**|
|1|SB - P2 - 13/14|12000|N|LS|0.0|-|SB - A&H MTX1/MTX2|
|2|SB - P2 - 15/16|12001|N|LS|0.0|-|SB - A&H MTX3/MTX4|
|3|SB - P2 - 17/18|12002|N|LS|0.0|-|None|
|4|SB - P2 - 19/20|12003|N|LS|0.0|-|SB - A&H Aux 3/4|
|5|SB - CD1|12004|N|SS|0.0|SB - CD1 - MJ|-|
|6|SB - AuxIn|12005|N|LS|0.0|SH JACK|-|
|7|SB - TT1|12006|N|SS|0.0|SB - TT AMP|-|
|8|SB - R2R1 - Out|12007|N|LS|0.0|SB - RTR1|-|

### Destinations:

||
|**Port**|**Name**|[**Channel**](https://wiki.wmfo.org/index.php?title=Operations/Diagrams_%26_Tables/LW_Address_Space "LW Address Space")|**Type**|**Load**|**Gain**|**Channel Source**|**Direct Device**|**Normaled Destination**|
|1|SB - P2 - 1/2|10500|FS|hi-Z|-12.0|SA - PGM1|-|SB - A&H ST1|
|2|SB - P2 - 3/4|10501|FS|hi-Z|-12.0|SA - PGM2|-|SB - A&H ST2|
|3|SB - P2 - 5/6|12004|FS|hi-Z|0.0|SB - CD1|-|SB - A&H CH9/CH10|
|4|SB - P2 - 7/8|12101|FS|hi-Z|0.0|SB - CDR1|-|SB - A&H CH11/CH12|
|5|SB - P2 - 9/10|12005|FS|hi-Z|0.0|SB - AuxIn|-|SB - A&H CH12/CH14|
|6|SB - P2 - 11/12|12200|FS|hi-Z|0.0|A&H OUT|SH LEVEL|SB - REC OUT|
|7|StudioDee - Mon|12000|FS|hi-Z|0.0|MTX1&2 (norm)|CROWN D-75|-|
|8|SB - R2R1 - In|12200|FS|hi-Z|0.0|A&H OUT|SB - RTR1|-|

Note: the Studio B nearfields are fed directly from the Allen & Heath.

1.  1. [Studio B Analog Node 1](#Studio_B_Analog_Node_1)
    1.  1.1. [Sources:](#Sources:)
    2.  1.2. [Destinations:](#Destinations:)


