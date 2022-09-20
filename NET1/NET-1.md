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

Possibly some further fragmentation of the Data-Packets from L3 is nessecary 
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

## Standardization Organizations
### IETF
Internet Engineering Task Force
### IEEE
Institute of Electrical and Electronics Engineers
### ISO
International Standards Organization
## IPv4 Address Calculation
Subnetmask devides an IP-Address in Network and host part.
Beginning from the left all Bits that define the network part must be 1 all trailing bits will be 0.
**Broadcast:** The last address in the nework
**Gateway:** Usually the first or last address before Broadcast
### Slash Annotation
Subnetmasks can also be displayed in Slash annotation. 

192.168.0.1/24 == IP: 192.168.0.1 SNM: 255.255.255.0

192.168.0.1/16 == IP: 192.168.0.1 SNM: 255.255.0.0


Example:

| First Octet | Second Octet | Third Octet | Fourth Octet |
| - | - | - | - |
| 255 | 255 | 255 | 0 |
| 11111111 | 1111 1111| 1111 1111| 0000 0000 |

### Classes
| Class | Binary Value Range | Decimal Value Range | SNM |
| - | - | - | - |
| A | 0xxx xxxx | 1 - 126 | 255.0.0.0 |
| B | 10xx xxxx | 128 - 191| 255.255.0.0 |
| C | 110x xxxx | 192 - 223 | 255.255.255.0 |
| D | 1110 xxxx | 224 - 240 | ---------------|
| E | 1111 xxxx | 240 - 255 | ---------------|

127.0.0.0/8 Loopback-Address / Local Host

A-C Unicast
# Abbreviations
**BC:** Broadcast

**NW:** Network

**SN:** Subnet

**SNM:** Subnetmask

**VLSN:** Variable Length Subnetting

# UP FOR NEXT WEEK: CHAPTER 2 of NetAcad !!!