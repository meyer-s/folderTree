This page is a listing of all lines running to the patch bays in the control room.  The numbering scheme is as follows (not all lines have been run, space has been left for expansion):

1 -  8 : Studio A Shielded Cat5e

 9 - 16 : Studio A Cat6
 
 17 - 24 : Studio B Shielded Cat5e
 
 25 - 32 : Studio B Cat6
 
 33 - 40 : Studio C Shielded Cat5e
 
 41 - 48 : Studio C Cat6
 
 49 - 52 : Annex Shielded Cat5e
 
 53 - 56 : Annex Cat6
 
 57 - 60 : MD Shielded Cat5e
 
 61 - 64 : MD Cat6
 
 65 - 68 : GM Shielded Cat5e
 
 69 - 72 : GM Cat6
 
 73 - 76 : Air Monitor Shielded Cat5e
 
 77 - 80 : Bay B Shielded Cat5e
 
 81 - 84 : Bay B Cat6

All wires rows in the table below correspond to a wire that has been run from Control to its destination, even if not connected to.

Control Room Wire Routing Table
-------------------------------

Legend: SHP - StudioHub+/Shielded Patch, P1 - Cat6 Patch 1 (24 port), P2 - Cat6 Patch 2 (16 port), END - RJ45 Male Connector, I - Input, O - Output, NC - Not Connected, POW - Line is connected to +/- 15VDC or +/- 5VDC power (decouple before servicing), CUBE - Line goes though a PS-CUBE in Control and is at +/- 15VDC (decouple before servicing), NUM - Non-Control end wire number needs to be updated.


|**Wire Number**|**Control Terminus**|**Destination Terminus**|**Control Device**|**Destination Device**|**Note**|
--- | --- | --- | --- | --- | ---
|1|SHP 1|SASHP 1|COND1-I1|SA-CD1|POW|
|2|SHP 2|SASHP 2|COND1-I2|SA-CD2|POW|
|3|SHP 3|SASHP 3|COND1-I3|SA-CD3|POW|
|4|SHP 4|SASHP 4|COND1-I4|TINMACHINE-D-O|POW|
|5|SHP 5|SASHP 5|CONA1-I7|TINMACHINE-A-O|POW|
|6|SHP 6|SASHP 6|NC|NC|POW|
|7|SHP 7|SA-END|COND1-O1|SA-CDR1-I| |
|8|SHP 8|SA-END|CONA1-I8|SA-TAPE1-O| |
|9|P1 1|SA 1|CONS1|SAA1| |
|10|P1 2|SA 2|CONS1|SAEGP1| |
|11|P1 3|SA 3|CONS1|TINMACHINE-NIC2| |
|12|P1 4|SA 4|NC|NC| |
|13|P1 5|NC|NC|NC| |
|14|P1 6|NC|NC|NC| |
|15|P1 7|SA split Dsub-15|On Air Light Driver|SAEGP1-GPIO6-8| |
|16|P1 8|SA split Dsub-15|NC (old phone)|SAEGP1-GPIO1,2|POW|
|17|SHP 9|SH-SB 1|NC|NC| |
|18|SHP 10|SH-SB 2|NC|NC| |
|19|SHP 11|SH-SB 3|NC|NC|NUM|
|20|SHP 12|SH-SB 4|NC|NC|NUM|
|21|SHP 13|SH-SB 5|NC|NC| |
|22|SHP 14|SH-SB 6|NC|NC| |
|25|P1 9|SB 1|CONS1|DEVOLUTION| |
|26|P1 10|SB 2|On Air Light Driver|SB Air Light Switch| |
|27|P1 11|SB 3|CONS2|SBA1|NUM|
|28|P1 12|SB 4|CONS2|SBRS1|NUM|
|29|P1 13|SB 5|NC|NC| |
|30|P1 14|SB 6|NC|NC| |
|33|SHP 17|SC-SH 1|COND1-I5|COULTON-D-O|CUBE|
|34|SHP 18|SC-SH 2|NC|NC| |
|35|SHP 19|SC-SH 3|NC|NC| |
|36|SHP 20|SC-SH 4|NC|NC| |
|41|P1 17|SC 1|CONS1|SCPSM switch| |
|42|P1 18|SC 2|NC|NC| |
|43|P1 19|SC 3|NC|NC| |
|44|P1 20|SC 4|On Air Light Driver|SCPSA1-GPIO4| |
|53|P2 1|AN 1|CONS1|SMOOTH-NIC1|NUM|
|54|P2 2|AN 2|SUPER-NIC2|SMOOTH-NIC4|NUM|
|61|P2 5|MD 1|CONS2|PRINTER|NUM|
|62|P2 6|MD 2|CONS1|FLOODLAND-NIC1|NUM|
|69|P2 9|GM 1|CONS1|NC|NUM|
|70|P2 10|GM 2|NC|NC|NUM|
|73|SHP 21|END|CONA1-O8|AMSW|CUBE|
|74|SHP 22|END|CONA1-O7|AMFH|CUBE|
|75|SHP 23|END|CONA1-O6|AMLG|CUBE|
|77|END|END|COND1-I8|BB-EAS-I| |
|78|END|END|COND1-O8|BB-EAS-O| |
|79|END|END|CONA1-O4|BB-Belar-O| |
|81|END|END|CONS1|BB-EAS| |
|82|END|END|CONS1|BB-ZEYPHR| |

