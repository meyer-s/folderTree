Studio A Shielded Patch Panel
-----------------------------

This is a Studio Hub+ Hub16 Patch Panel ([manual](https://wiki.wmfo.org/@api/deki/files/422/=HUB16-DC.pdf "/@api/deki/files/422/=HUB16-DC.pdf")) installed in the back of the Studio A in cabinet rack.
 It utilizes a Studio Hub+ External Universal Power Supply (PS-EXTU) for +/- 15VDC, Power Grounding, and Shield Grounding.

#### Jumper Key

JU1 - +15VDC Connect (per channel)
 JU2 - -15VDC Connect (per channel)
 JU3 - Shield to Common Chassis Connect (per channel)
 JU4 - Shield to Common Shield Bus/Power Supply Shield Connect (per channel)
 JU33 - Chassis to Shield Bus Connect (per 8 block)
 JU34 - Common Power Ground Bus Connect (per channel)

X - Jumper Connected

#### JU33 Status

Block 1 (left) - Connected
 Block 2 (right) - Connected

### Routing Table

Channel| RJ-45 Device | Patch Device | Notes
--- | --- | --- | ---
1 | - | CONSHP1 | to control, disconnected
2 | - | CONSHP2 | 
3 | - | CONSHP3 | 
4 | SA-Comp-In | SAA1-O6 | SA Skype Input on Computer, uses SH Line Converter with adjustments to match level, configured as To send from the SA-Comp-D source to get mix-minus 
5 | SA-CD3 | SAD1-I3 | CD3 needs S/PDIF to AES converter
6 | SA-COMP-D | SAD1-I4 | S/PDIF optical converter in cabinet
7 | SA-DJ-HP Amp | SAA1-O1 | That box on the far side that has a bunch of headphone jacks in it
8 | SA-Guest-HPs | SAA1-O2 | Bounces around to the different amps
9 | SA-Mic1 | SAA1-I1 | Mic amps in cabinet
10 | SA-Mic2 | SAA1-I2 | 
11 | SA-Mic3 | SAA1-I3 | 
12 | SA-Mic4 | SAA1-I4 | 
13 | SA-Aux1 | SAA1-I5 | RCA SH converters
14 | SA-Aux2 | SAA1-I6 | 
15 | SA-TT1 | SAA1-I7 | RCA SH => TT amp in cabinet
16 | SA-Rec-Out | SAA1-O4 | RCA SH

## SA Modular Jack

There are 6 ports of terminated CAT6 in Studio A. All six are patched to CONS1. 

Jack | Device
--- | ---
1 | SAA1 (Analog node)
2 | SAEGP1 (Element controller)
3 | Adele
4 | SAPDU (Remote controlled PDU)
5 | SAD1 (Digital xNode)
6 | -

[Page Attachments](https://wiki-files.wmfo.org/Operations/Station_Architecture_Overview/Signal_Chain_%26_Peripherals/StudioHub_Peripherals/SASHP)
