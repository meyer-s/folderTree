Control Room Analog Node 1
--------------------------

**Credential Level:** Operations
 [**IP Address**](https://wiki.wmfo.org/index.php?title=Operations/Diagrams_%26_Tables/IP_Address_Space "IP Address Space")**:** 192.168.0.100

See [Axia Normal Tables](https://wiki.wmfo.org/index.php?title=Operations/Diagrams_%26_Tables/Axia_Normal_Tables "Axia Normal Tables") page and [Diagrams & Tables](https://wiki.wmfo.org/index.php?title=Operations/Diagrams_%26_Tables "Diagrams & Tables") page for keys and abbreviation information.

### Sources:


|**Port**|**Name**|[**Channel**](https://wiki.wmfo.org/index.php?title=Operations/Diagrams_%26_Tables/LW_Address_Space "LW Address Space")|**Shareable**|**Mode**|**Gain**|**Direct Wire**|**Direct Device**|**Terminal Device**|
--- | --- | --- | --- | --- | --- | --- | --- | ---
|1|-|10000|N|D|0.0|-|-|-|
|2|-|10001|N|D|0.0|-|-|-|
|3|AphexCompOut|10002|N|LS|0.0|-|-|Apex - O|
|4|AirMon 1 - Belar|10003|N|LS|0.0|79|BB - Belar - O|Rereceive|
|5|-|10004|N|D|0.0|-|-|-|
|6|-|10005|N|D|0.0|-|-|-|
|7|SA - Comp - A|10006|N|SS|0.0|-|CONSHP 5|SA - Comp - A MJ|
|8|SA - Tape|10007|N|SS|0.0|-|CONSHP 8|SA - TAPE1 - O|

### Destinations:

|**Port**|**Name**|[**Channel**](https://wiki.wmfo.org/index.php?title=Operations/Diagrams_%26_Tables/LW_Address_Space "LW Address Space")|**Type**|**Load**|**Gain**|**Direct Wire**|**Direct Device**|**Terminal Device**|
--- | --- | --- | --- | --- | --- | --- | --- | ---
|1|-|0|FS|hi-Z|0.0|-|-|-|
|2|-|0|FS|hi-Z|0.0|-|-|-|
|3|AphexCompIn|10107|FS|hi-Z|0.0|-|-|Apex - I|
|4|Backup Tow Feed|10107|FS|hi-Z|0.0|-|CON - LD|Transmitter (planned)|
|5|-|0|FS|hi-Z|0.0|-|-|-|
|6|Mons Lounge VLib|10003|FS|hi-Z|-12.0|-|CONCUBE2 I1|SHAMP - LNG+VLIB|
|7|Mons Halls|10003|FS|hi-Z|-12.0|-|CONCUBE1 I1|SHAMP - HALLS|
|8|Mons Stairs|10003|FS|hi-Z|-12.0|-|CONCUBE1 I2| SHAMP - STAIRS|

1.  1. [Control Room Analog Node 1](#Control_Room_Analog_Node_1)
    1.  1.1. [Sources:](#Sources:)
    2.  1.2. [Destinations:](#Destinations:)


