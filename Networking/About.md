# Notes on Networking and Telecommunications

## General Communication

Communication can range from symbols, written word, spoken word, video, and is constantly evolving.
It can be synchronous or asynchronous.

## Unified Communications (UC)

UC combines different forms of communications and provides a framework for a consistent user interface across multiple devices and improves business communications.
Typically a UC system or framework combines voice, email, and IM into a seamless business application that improves overall efficiency.

## Voice over Internet Protocol or IP Telephony

VoIP is cheaper and increasingly popular, now more popular than PSTN. Also improves productivity by allowing users to see who is currently available along with other benefits.

## PSTN

PSTN - Public Switch Telephone Network

* A collection of private and government owned telephone networks.
* digitised in 1960s
* SS7 developed in 1975

SS7 - Signaling System No. 7

* A set of signaling protocols, used to set up and tear down calls
* Basis of call routing for most of the world's calls
* PSTN and SS7 integrate with one another with the help of a signaling gateway
* Nodes in an SS7 network are signaling points, of which there are three types:
  * Service Switching Point (SSP)
  * Signal Transfer Point (STP)
  * Service Control Point (SCP)

## Codecs

VoIP involves digitising an analog signal to transfer it over IP.

| Algorithm | Voice Bit Rate (kb/sec) | Packets per Second | Packet Bit Rate (kb/sec) |
|-----------|-------------------------|--------------------|--------------------------|
| G.711 (PCM) | 64 | 100 | 96 |
| G.723.1 (MPMLQ) | 6.3 | 26 | 14.6 |
| G.723.1 (ACELP) | 5.3 | 22 | 12.3 |
| G.726 (ADPCM) | 32 | 100 | 64 |
| G.728 (LD-CELP) | 16 | 100 | 48 |
| G.729a (CS-ACELP) | 8 | 100 | 40 |

G.711, Pulse Code Modulation, is the most commonly used codec.

MOS - Mean Opinion Score - rating of the call quality of a call, 3.5-4.2 out of 5 is typical.

## Real Time Protocols

* RTP - Real-Time Transport Protocol, transports audio and video. Often over UDP.
* RTCP - Real-Time Control Protocol , carries control information.
* RTSP - Real-Time Streaming Protocol, establishes and controls multimedia sessions.

## Gateway Overview

Devices that adjust to different network signalling requirements and convert media streams from one form to another.

Types:

* Media Gateways
* Call agents - Media Gateway Controller or Softswitch
* Signaling Gateways
* Tanslators and mixers

Protocols:

* SIGTRAN - transports SS7 signals through the Internet
* Media Gateway Control Protocol (MGCP/Megaco, H.248) - works with H.323 or SIP
* Call control protocols - SIP, H.323, and Skinny (SCCP)

## SIP

SIP, Session Initation Protocol, is a Signaling Protocol and is the most common signaling protocol used in VoIP today. SIP establishes, manages, and terminates calls.

Application layer protocol for signaling and control. Establishes, maintains, and terminates sessions between parties over the internet, private networks, and cellular systems.
SIP messages manage session negotiation, user location, and termination. Sessions may involve one or more media streams, such as voice and video.

## H.323

H.323 is an ITUT (International Telecommunications Union) recommendation for audio and video communication across an IP network. A kind of wrapper for interoperability?
One of the first VoIP protocols developed, but has since been overtaken in popularity by SIP, but is still in use.

## Softphone

A software application on a computer than can make VoIP calls, and unfortunately typically has a skeumorphic UI.

## Journey of a typical Call

Phone calls begins at the subscriber or local loop which carries the signal from the subscriber's home to the central office over a copper cable.
The signal then goes to the PSTN to SS7 and then on to the internet. The final path depends on the destination of the call and the type of network.