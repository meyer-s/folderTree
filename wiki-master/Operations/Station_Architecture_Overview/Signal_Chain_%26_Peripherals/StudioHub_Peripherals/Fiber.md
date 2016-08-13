This page documets the fiber connections from Control in Curtis to the 4th floor HVAC closet in Ballou ("the tower") where the transmitter is located. The run is estimated at between 1.0km and 1.5km.

The term "fiber box" may refer to either the beige "wall box," which holds the 6 ST connections on the fiber trunk, or a "[fibox](http://www.netsys-direct.com/product_p/nm-102kit.htm "http://www.netsys-direct.com/product_p/nm-102kit.htm")", a converter between a single strand of fiber and ethernet, made by netsys. All fiber lines require a fibox, an SFP in a switch, or a NIC in a computer, as these hold the laser and reciever. 

The fiber lines are critical infrastructure as they connect the studio to the transmitter (by way of the Omnia and backup router selector), as well as ethernet [telemetry](https://wiki.wmfo.org/Operations/Regulatory/Telemetry "Telemetry"), a PDU, and the primary servers. The primary connection is between two Cisco SG500X switches.

### Curtis Connections

|Strand (Curtis Number)|Interface|Device|
|:---------------------|:--------|:-----|
|1,2|Cisco SFP |Cisco SG500X-24 port|
|3|Fibox 1|PDU|
|4|Fibox 2|Router Selector|
|5+6|N/C|Backup link (connection in prog)|

### Saturation tests

Saturation tests can be done using `iperf -s|-c IP `run on Elvis (for CONS1) and Ringo for TOWS1 

### Fiber resources

-   [Single Mode vs. Multi-Mode: What’s the Difference?](http://www.imakenews.com/drs/e_article001146955.cfm "http://www.imakenews.com/drs/e_article001146955.cfm")
-   [Fiber Polarity Simplified](http://www.ampnetconnect.com/documents/WHITEPAPER_Fiber_Polarity_Simplified_090813.pdf "http://www.ampnetconnect.com/documents/WHITEPAPER_Fiber_Polarity_Simplified_090813.pdf")
-   [Fiber Connectors](http://www.fiberoptics4sale.com/Merchant2/fiber-optic-connectors.php "http://www.fiberoptics4sale.com/Merchant2/fiber-optic-connectors.php") - see duplex LC, ST, SC
-   [SFP transciever](http://en.wikipedia.org/wiki/Small_form-factor_pluggable_transceiver "http://en.wikipedia.org/wiki/Small_form-factor_pluggable_transceiver") - between switch and LC connector, the part with the lasers

1.  1. [Strands](#Strands)
2.  2. [Curtis Connections](#Curtis_Connections)
3.  3. [Saturation tests](#Saturation_tests)
4.  4. [Fiber resources](#Fiber_resources)

