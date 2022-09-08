# Networking Technologies
**Test:** 20.12.2022

**Material:** [Cisco Networking Academy Course](hhttps://lms.netacad.com/course/view.php?id=1494354) 

Certification for 200€

# Protocols

# Network Models
The Connection happens only on layer 1
## OSI
### L7 Application
**Data Unit:** Data
HTTP, FTP, SMTP...
### L6 Presentation
**Data Unit:** Data
ASCII, EBCIDIC, JPEG... essentially data encodings
### L5 Session
**Data Unit:** Data
SIP, H.323, H.235 (Voice over IP)
### L4 Transport
**Data Unit:** Segment
TCP, UDP
### L3 Network
**Data Unit:** Packet
**Hardware:** Router
IP, ICMP (Routing)
### L2 Data Link
**Data Unit:** Frame
**Hardware:** LAN Switch
Not only has a Header but also a Trailer
Ethernet, WiFi
### L1 Physical
**Data Unit:** Bits
**Hardware:** LAN Hubs
RJ45, Ethernet, WiFi

## TCP/IP
### L4 Application
### L3 Transport
### L2 Internet
### L1 Network Access

## Data Encapsulation
### Segmentation
Deviding Data into Parts (L4 OSI).
Each Segment is encapsulated with an Header
### Headers
Layer removes its own headers and hands information over to higher layers (Decapsulation)