Studio C PowerStation Main 1 Audio Node
---------------------------------------

**Credential Level:** Operations
 **[IP Address](https://wiki.wmfo.org/index.php?title=Operations/Diagrams_%26_Tables/IP_Address_Space "IP Address Space"):** 192.168.3.152 (Assigned by SCPSM1 at 192.168.3.150)

See [Axia Normal Tables](/Operations/Diagrams_%26_Tables/Axia_Normal_Tables "Operations/Diagrams_%26_Tables/Axia_Normal_Tables") page and [Diagrams & Tables](https://wiki.wmfo.org/index.php?title=Operations/Diagrams_%26_Tables "Diagrams & Tables") page for keys and abbreviation information.

### Sources:

||
|**Port**|**Name**|[**Channel**](https://wiki.wmfo.org/index.php?title=Operations/Diagrams_%26_Tables/LW_Address_Space "LW Address Space")|**Shareable**|**Mode**|**Gain**|**Ph/AES**|**Direct Wire**|**Direct Device**|**Terminal Device**|
|M1|SC - MIC 1|13520|N|LS|64.0|D|-|-|SC - MIC 1|
|M2|SC - MIC 2|13521|N|LS|64.0|D|-|-|SC - MIC 2|
|A1|SC - RTR1 - Out|13522|N|LS|0.0|-|-|-|SC - RTR1 - O|
|A2|SC - Tape - Out|13523|N|SS|0.0|-|-|-|SC - TAPE1 - O|
|A3|SC - Aux1|13524|N|SS|0.0|-|1|SCSHP 1|AUX1 PLATE|
|A4|SC - Aux2|13525|N|SS|0.0|-|2|SCSHP 2|AUX2 PLATE|
|D1|SC - CDR1 - Out|13526|N|SS|-9.0|A|-|-|SC - CDR1 - O|
|D2|SC - CD1|13527|N|SS|-9.0|A|7|SCSHP 7|SC - CD1 MJ|

### Destinations:

||
|**Port**|**Name**|[**Channel**](https://wiki.wmfo.org/index.php?title=Operations/Diagrams_%26_Tables/LW_Address_Space "LW Address Space")|**Type**|**Load**|**Gain**|**Direct Wire**|**Direct Device**|**Terminal Device**|
|A1|SC - RTR1 - In|13500|FS|hi-Z|0.0|-|-|SC - RTR1 - I|
|A2|SC - Tape - In|13500|FS|hi-Z|0.0|-|-|SC - TAPE1 - I|
|A3|SC - Rec Out 1|13500|FS|hi-Z|0.0|3|SCSHP 3|RO 1 PLATE|
|A4|SC - Rec Out 2|13500|FS|hi-Z|0.0|4|SCHSP 4|RO 2 PLATE|
|A5|SC - DJ Phns|13511|FS|hi-Z|0.0|5|SCSHP 5|DJ HP AMP|
|A6|SC - GstPhns|13514|FS|hi-Z|-12.0|6|SCSHP 6|GST HP AMP|
|D1|SC - CDR1 - In|13500|FS|-|0.0|-|-|SC - CDR1 - I|
|D2|-|0|FS|-|0.0|8|SCSHP 8|-|

1.  1. [Studio C PowerStation Main 1 Audio Node](#Studio_C_PowerStation_Main_1_Audio_Node)
    1.  1.1. [Sources:](#Sources:)
    2.  1.2. [Destinations:](#Destinations:)


