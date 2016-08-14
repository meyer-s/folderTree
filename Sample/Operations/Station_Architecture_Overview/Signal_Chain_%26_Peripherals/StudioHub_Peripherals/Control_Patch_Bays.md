# Control Patch Bays

There are 3 patch bays in Control, 1 Shielded CAT 5 (top) and 2 Unshielded CAT 6.

The wires are routed around the station via the attic. Each port should be labeled (SA, SB, SC, Annex, MD, GM) and an 'H' indicates a shielded cable.

Shielded are used for Audio in StudioHub AES or Analog format -- some may carry +/- 15V power as well. Unshielded CAT6 carry data and 802.1af PoE. Do not mix and match cables at all costs (putting 15V into a device not expecting it results in sparks and fire).

There are several special-purpose wires:

1. Hall monitors etc are carried to their respective amplifiers (Lounge, outside hall, etc). Each are labeled appropriately and fed through the built-in power supply.
2. GPIO for on-air lights is carried over so-marked cables and connects to the GPIO-controlled PDU in Control.
