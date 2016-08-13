This page covers the Arduino control panel. The purpose of this panel:

1.  View which studio is on air
2.  (Switch to and) Activate the Duke's Rivendell for an emergency override
3.  Switch between studios
4.  Power the transmitter on or off
5.  Troubleshoot basic issues

 

A couple of procedures:

1.  Reboot the Element in Studio A by sending the OFF command to the PDU in A and then sending the ON command after a cool down delay. If boot is not successfull, offer to execute reboot commands.
2.  Power up/down studios

 

Design:

1.  4 buttons and keypad driven with one Analog Input and one Interrupt Pin each, thus 4 pins required for input
2.  SendOnlySoftwareSerial library used to write to display
3.  4 outputs drive lights on buttons

*
