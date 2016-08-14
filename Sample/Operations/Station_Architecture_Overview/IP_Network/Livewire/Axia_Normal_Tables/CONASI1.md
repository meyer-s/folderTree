Control Audio Science Inc. 6585 PCI Sound Card
----------------------------------------------

Think of it as a node that resides inside Duke. It's mostly invisible to the OS. Manufacturer info [here](http://www.audioscience.com/internet/products/cobranet/asi6585.htm "http://www.audioscience.com/internet/products/cobranet/asi6585.htm"). Provides [Rivendell](https://wiki.wmfo.org/Operations/Rivendell#ASI_SoundCard "Rivendell") out and webstream in.

**Credential Level:** Operations
 **[IP Address](https://wiki.wmfo.org/index.php?title=Operations/Diagrams_%26_Tables/IP_Address_Space "IP Address Space"):** 192.168.0.130

See [Axia Normal Tables](/Operations/Diagrams_%26_Tables/Axia_Normal_Tables "Operations/Diagrams_%26_Tables/Axia_Normal_Tables") page and [Diagrams & Tables](https://wiki.wmfo.org/index.php?title=Operations/Diagrams_%26_Tables "Diagrams & Tables") page for keys and abbreviation information.

### Sources:

||
|**Port**|**Name**|[**Channel**](https://wiki.wmfo.org/index.php?title=Operations/Diagrams_%26_Tables/LW_Address_Space "LW Address Space")|**Shareable**|**Mode**|**Gain**|**Direct Wire**|**Direct Device**|**Terminal Device**|
|1|SA-RD Main|10300|N|SS|6.0|-|-|Adele RD|
|2|SA-RD Aux|10301|N|SS|0.0|-|-|Adele RD|
|3|SA-RD Preview|10302|N|SS|0.0|-|-|Adele RD|
|4|SC-RD Main|10303|N|SS|0.0|-|-|Coulton RD|
|5|SC-RD Aux|10304|N|SS|0.0|-|-|Coulton RD|
|6|SC-RD Preview|10305|N|SS|0.0|-|-|Coulton RD|
|7|TINMACH-RD All|10306|N|SS|0.0|-|-|TinMachine RD|
|8|DUKE-RD All|10307|N|SS|3.0|-|-|Duke Rivendell|

### Destinations:

||
|**Port**|**Name**|[**Channel**](https://wiki.wmfo.org/index.php?title=Operations/Diagrams_%26_Tables/LW_Address_Space "LW Address Space")|**Type**|**Load**|**Gain**|**Direct Wire**|**Direct Device**|**Terminal Device**|
|1|Webstream|10420|FS|hi-Z|0.0|-|-|Webstream|
|2|-|0|FS|hi-Z|0.0|-|-|-|
|3|-|0|FS|hi-Z|0.0|-|-|-|
|4|-|0|FS|hi-Z|0.0|-|-|-|
|5|-|0|FS|hi-Z|0.0|-|-|-|
|6|-|0|FS|hi-Z|0.0|-|-|-|
|7|-|0|FS|hi-Z|0.0|-|-|-|
|8|-|0|FS|hi-Z|0.0|-|-|-|

### GPIO:

||
|**Port**|**Name**|[**Channel**](https://wiki.wmfo.org/index.php?title=Operations/Diagrams_%26_Tables/LW_Address_Space "LW Address Space")|Notes|
|1|SA\_CR\_GPIO|10308|Preview: 3|
|2|SC\_CR\_GPIO|10309|Preview: 8|
|3|SA\_RD|10300|RD off pulse: 15|
|4|SC\_RD|10303|RD off pulse: 20|
|5|-|0| |
|6|-|0| |
|7|-|0| |
|8|-|0| |

 

The GPIO channels carry information for the Rivendell audition to enable the Element external preview, and for the mics to turn on the [on-air lights](https://wiki.wmfo.org/index.php?title=Operations/Diagrams_%26_Tables/GPIO_Spec/On_Air_Lights "On Air Lights"). They are used as the CR GPIO channel in every source profile in that room, as well as on the physical GPIO port that drives the lights. The second pair of channels make GPO about the Rivendell fader, added automatically by the board, available to Rivendell as GPI.

1.  1. [Control Audio Science Inc. 6585 PCI Sound Card](#Control_Audio_Science_Inc..C2.A06585_PCI_Sound_Card)
    1.  1.1. [Sources:](#Sources:)
    2.  1.2. [Destinations:](#Destinations:)
    3.  1.3. [GPIO:](#GPIO:)


