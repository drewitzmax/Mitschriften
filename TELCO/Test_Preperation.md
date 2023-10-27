# Test Preparation
## Glossar
DSL = Digital Subscriber Line

MPLS = Multi Protocol Label Switching

PHP = Penultimate Hop Popping

## What systems are involved in a xDSL Network?
* DSLAM (DSL Access Multiplexer)
* band/low-pass filter
* xDSL Modem
* twisted pai telephone cable

## Whatfactors affect transmission rate in DSL?
* Gauge of twisted-pair line
* electrical interference
* Distance
* line quality / noise
* dsl technology ADSL VDSL G.fast
* Congestion
* Crosstalk

## MPLS Lables
### Where are MPLS lables positioned
Between layer 2 and 3. It is above the layer 2 frame and incapsulated by the IP packet. Allows for label based forwarding without touching IP.
### BoS (Bottom of Stack) field
* 0 if there are more fields inside
* 1 if it is the last field


## Which MPLS Router performs PHP function
The router before the egress router. Removing MPLS Label and routing to the egress router based on IP header.
Used to reduce load on the egress router by splitting up processing load to multiple devices.

## Advantages of Optical Transmission
* Transmission Speed
* High Bandwidth (Density)
* Long Distances
* No Electomagnetic Interference
* Low Signal Loss
* Ubiquitous Internet Access
* Lightweight and Small
* No corrosion
* Can be extended to the end user
* Low energy consumption

## Session Description Protocol (SDP)
*  Negotiation of media or session properties
* Description of the media (audio/video/text) that can be used in Multimedia over IP sessions

SDP is primarily used for negotiating the parameters and characteristics of multimedia sessions, such as audio and video streams, in protocols like SIP (Session Initiation Protocol). It describes the media types, codecs, and other session properties.


## Optical Amplification
Optical Signals are most commonly amplified by Erbium-Doped Fiber Amplifiers (EDFAs)

## Gain Saturation
For input powers above a certain level an increase in input power doesn't produce higher output powers

## Advantages of MPLS
* Scalable VPNs (Traffic Segmentation)
* Any Protocol Supported (AToM - any transport over MPLS)
* Traffic Engineering
* Quality of Service
* Scalable
* Traffic Optimisation (Fewer DNS Lookups)
* Global Reach

## Protocols for real time media data transmission
* RTP (Real-Time Transport Protocol)
* MGCP (Media Gateway Control Protocol)
### Controll only:
* RTCP (Real-Time Control Protocol)
* SIP-T (Session Initiation Protocol for Telephones)

## Loss/Gain Calculation
$db = 10 * log(\frac{current}{initial})$

## DSL Types and Speeds

* ADSL (Asysmmetric)
* SDSL (Symmetric)
* IDSL (ISDN)
* VDSL (Very Hight Bitrate)
* VDSL2 17a
* VDSL2 35b
* G.fast

## Fabry-Pérot filter
The Fabry-Perot filter is a optical filter for a range of wavelengths. It consists of two parallel highly reflective surfaces. By reflecting the waves multiple times, the wave cancel themselves out or if the wavelength is a multiple of the distance it will pass through as it won't cancell itself out