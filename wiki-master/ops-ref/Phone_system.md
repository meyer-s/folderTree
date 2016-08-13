# Instructions to DJs

[Watch the video](https://www.youtube.com/watch?v=VA58rh5cP2U&index=1&t=8m55s&list=PLP5F7bT61v2tx_MKfE0UVFV1dXid4YE5M)

To **answer the phone**, press the phone button (Set). Then hold talkback, press preview, then release both buttons. Then talk to the caller off-air.

To **put the caller on air** (after the phone was answered with Set), put the phone fader on and up.

To **hang up**, press the phone button again and the light should go out.

To **dial out from the board**, press the phone button, dial on the board’s keypad on the right, and then press the Enter button by the arrow keys.

Please note that there are some issues with having phone lines on Studio C and Studio A at the same time. Studio C and Studio A cannot both answer the same phone line. In addition, we are limited to four simultaneous phone channels on the boards, so if phone line 1 is on Studio C, we can't put one of the four phone lines on Studio A.

# Operations Docs

WMFO has a VoIP system to handle its phone needs. This provides us with a great flexibility (and no need to configure the system through TTS).

There are two main entry points:

1. VoIP.ms SIP gateway with 4 active FXS ports for 4 POTS lines
2. Tufts 7-3800 POTS line

POTS lines <=> conata1 <=> connx1 which bridges to the Livewire network

# Desktop Director

We have a desktop director which is a specialized (Telos Provided) ISDN phone that connects directly to the phone system through one of the four ports on the rear of the Nx12. It is able to view, answer, and manipulate all the lines from within the Nx12 system. You can select "Hold" using the labeled button on the phone and it will display the same status on the Element. The manual provides extra information.

# Element Side

The phone system requires Euro-style faders with four buttons above ON/OFF. We have 4 of these faders on the Studio A board and 2 on the Studio C board. On each they are on the right side. Phones can only be assigned to these faders.

Instead of fader numbers, the phone line faders display a status symbol. A dot means the line is not ringing. A square means the phone is on but not connected. A pulsing square means the line is ringing. A downward arrow means the line is connected. An x means the line is in use, most likely that the line is on the other board or answered on the desktop director.

The system itself is the Telos Nx6, installed November 2012 in the far side of the Control rack. See Telos documentation for more details.

# Wiring

Four POTS lines enter the Nx12 from the Patton ATA. Lines 1 & 2 are split for flashers; the 3800 phone from Tufts is split for flashers as well.

Both VoIP Line 1 and 3800 run to Studio B for its phone.

# VoIP Configuration

Terminology:

- VoIP - voice over IP, the way in which phones are transferred around an internet
- SIP - Session Initiation Protocol, the protocol that handles setting up calls
- RTSP - realtime transfer streaming protocol, the protocol that transfers actual audio in the call
- POTS - Plain Old Telephone System (1890s style phones with RJ11 jacks)
- DTMF - dual tone multi frequency, the modern signaling used to dial over POTS phones
- DID - direct inward dial number, the actual phone number which people use to dial us
- PSTN - public switched telephone network
- PBX - private branch exchange
- Trunk - a virtual pipe over which calls are transferred - as opposed to a phone line, trunks are for general calls and don't have channels reserved for a single number. Each call comes over tagged with a phone number using SIP and then the call is routed based upon that information.
- IVR - interactive voice receptionist ("Press 1 for Jim, Press 2...")
- Hunt group - series of phone lines where busy lines cause failover to next available line - first caller gets line 1, second gets line 2, etc
- ATA - analog telephone adpater, converts a VoIP line to a POTS line.

VoIP.ms is our gateway to the PSTN. VoIP.ms provides a handy configuration portal where one configures which DIDs map to which endpoints. We use an IVR (interactive voice receptionist) to direct callers into our system. 

1. Caller dials DID (855) 915-WMFO 
2. PSTN routes caller to VoIP.ms
3. VoIP.ms sees DID sent to IVR, IVR handles call (can route to mailboxes for PD or ops)
4. CONATA1 sip account
5. CONATA1 directs callers into a hunt group
6. Callers are routed to CONATA1 phone lines 1-4
7. callers enter the Nx12 phone system, received by element or desktop director

# CONATA1

This is the magic box that connects to VoIP.ms, handles the transfer of signaling and audio, and provides POTS lines for the Nx12. The device has a fairly arcane configuration system, though it provides a web interface to do handle it.

1. You first configure the IP and Default Route for the device (along with QoS)
2. You configure a SIP Gateway GW_SIP that binds an IP Interface to a Location Service (?) and a SIP Interface
3. A SIP interface IF_SIP handles the registration and incoming call routing to DJ-Phone Hunt Group
4. A Hunt Group routes the call to the FXS Interfaces
5. The FXS interface configures parameters about the FXS port to POTS lines
6. The FXS port refers to the physical port and configures physical paramters

On the outbound the path goes FXS Port => FXS Interface => Routing Table => SIP Interface/Gateway back outwards. 
