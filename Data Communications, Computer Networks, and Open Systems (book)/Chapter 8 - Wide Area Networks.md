## Notes
#### Introduction
In contrast with Public Switched Telephone Networks, which support only a modest user data rate (9600bps), and which are charged on a time * distance basis, this chapter is about Wide Area Networks, which include both public data networks and enterprisewide private data networks.

#### 8.1 Characteristics of public data networks
[[Abbreviations#PDN|PDN]] - **public data network** - created and maintained by a (national) authority specifically for transmitting data. 
Two main types of PDN - packet switched ([[Abbreviations#PSPDN|PSPDN]]) and circuit switched ([[Abbreviations#CSPDN|CSPDN]]). The standards for interoperating between PDN equipment made by different manufacturers for each of these types of networks refers to the lower three layers of the ISO reference model (Network, Link, and Physical layers). The characteristics of these lower layers are made transparent to the higher layers by the transport layer (fourth layer), which offers the higher layers a network-independent message transport service.

##### 8.1.1 Circuit and packet switching
Circuit switched networks create a physical communication channel, set up through he network from the calling to the called subscriber equipment. This connection is then used exclusively by the two subscribers for the duration of the call. All telephone connections are of the circuit switched type ([[TODO]]: Still?)
Circuit-switched connections provide a fixed data rate channel - both subscribers must operate at that rate. Also, before any data can be transmitted, a connection must be set up via the network. Currently, the time to set up a call through the PSTN (telephone network) can be relatively long - tens of seconds - owing to the type of equipment used for the exchange. However, this time is getting shorter (tens of milliseconds, sometimes) because of a) widespread introduction of computer-controller switching exchanges, and b) adoption of digital transmission through the network . Also - the extension of digital transmission to the subscribers equipment means that a high bit rate (64kbps or higher) switched transmission path will be available to the subscriber. This path can then be used for transmitting data without using modems. The resulting digital PSTN can be regarded as a public [[Abbreviations#CSDN|Circuit Switched Data Network]].
Although setting up a connection for an all-digital circuit switched networks is relatively fast, the resulting connection still provides only a path with a fixed data rate.

With a packet-switched network, two communicating subscribers (DTEs) can operate at different data rates.  Also, no physical connections are establisted through the network. Instead, the data is first assembled into one or more message units, called packets. These packets include both the source and destination DTE addresses. They are then passed bit serially by the source DTE to its local **packet switching exchange** ([[Abbreviations#PSE|PSE]]). On receipt of each packet, the exchange first stores the packet, then inspects the destination address it contains. Each PSE contains a **routing directory** specifying the outgoing link(s) (transmission path(s)) to be used for each network address. The PSE forwards the packet on the appropriate link at the maximum available bit rate. This mode of working is called **packet store-and-forward**.
As each packet is received (and stored) at each PSE along the route, it is forwarded interspersed with other packets being forwarded on that link.
Each transaction only occupies a (random) portion of the available bandwidth on each link, since packets are interspersed with packets from other sources. The available bandwidth will range from zero (user is not transmitting any data) to the full bandwidth, if it is transmitting packets continuously.
A number of packets may arrive simultaneously at a PSE (on different incoming links) and each may require forwarding to the same outgoing link. If a number of long packets are waiting to be transmitted, other packets may experience unexpectedly long delays. To prevent this, and ensure that the network has a reliably fast transmit time, a **maximum length** is allowed for each packet. Therefore, a message submitted to the transport layer within the DTE may have to first be divided by the source transport layer into smaller packets before transmission. These smaller units are reassembled into a single message by the transport layer at the destination DTE.
Another difference between a CSPDN and a PSPDN is that with a circuit switched data network, the network does not apply any error or flow control on the transmitted data, so this must be performed by the user. With a PSPDN, however, sophisticated error and flow procedures are applied by the network PSEs.

##### Datagrams and virtual circuits
PSPDNs have two types of service: datagram and virtual call (circuit). 
Datagrams are usually used for the transfer of short, single-packet messages.
Virtual calls are analogous to a digital PSTN in that a link is set up between two DTEs. Then, the packets can transfer directly between them. The source DTE sends a **call request** packet to its local PSE containing, in addition to the required physical destination DTE network address, a reference called the virtual circuit identifier ([[Abbreviations#VCI|VCI]]). The PSE notes this VCI, and forwards the (call request) packet as usual. At the destination PSE, a second VCI is assigned to the call request call request packet, before it is forwarded on the outgoing link to the destination DTE. Then, assuming the call is accepted, an appropriate response packet is returned to the calling DTE ([[TODO]]: to confirm that the circuit has been established?). At this point we say that a virtual circuit (VC) exists between the two DTEs. The information transfer phase is then entered, and all subsequent data packets relating to this call are assigned the same reference numbers ([[TODO]] VCI?) on each interface link to the network. Then, both the source and destination DTEs can distinguish between packets arriving on the same link but relating to different calls.
Note that a VC is only a logical connection. Moreover, because PSPDNs provide error+flow controls, the class of service supported by a VC is much higher than that on a circuit switched network.
Normally, a vircuit circuit is cleared, and the appropriate VCIs released, after all data related to a call (ie, all the packets of that data) have been exchanged. However the VC may be left permanently established, so that a user who frequently requires to communnicate with another user does not have to set up a new VC for each call. This is known as a permanent virtual circuit ([[Abbreviations#PVC|PVC]]). 

#### 8.2 Packet Switched data networks
Internationally agreed network access protocol defined to interface a DTE to a PSPDN is X.25 (which is a collection of protocol standards).
There's an important diagram here (page 429) outlining a) how the different parts of X.25 apply to different parts of PSPDNs, and b), defining what connections constitute the different ISO layers in a PSPDN.
Here's a description of a):
DCE-to-DTE: X.21/X.21 bis
PSE-to-DTE via DCE: X.25
PSE-to-PSE: PSPDN
Here's a description of b):
PSE-to-PSE: internal network protocols
DCE to individual DTEs - physical layer
PSE to DTEs via DCE - link layer and packet layer
DTE-to-DTE via the PSEs - transport layer

At the lowest layer (physical - DCE to DTE), the interface standard is called X.21. This interface is also used with digital circuit switched networks. The link layer protocol used with X.25 is a version of the HDLC protocol known as LAPB and its function is a provide the packet layer with an error-free packet transport facility over the physical link between the DTE and its local PSE. Finally, the packet layer is concerned with the reliable transfer of transport layer messages - known as transport protocol data units (TPDUs) - and with the multiplexing of one or more virtual calls - network service access points (NSAPs) - on the single physical link controlled by the link layer. 

##### 8.2.1 Physical layer
The DCE is analogous to a synchronous modem (for telephones), since its function is to provide a full-duplex, bit-serial, synchronous transmission path between the DTE and the local PSE. It can operate at data rates between 600bps and 64kbps.

##### 8.2.2 Link layer
The aim of this layer is to provide the packet layer with a reliable (error free and no duplicates) packet transport facility across the physical link between the DTE and the local PSE.


## Specifics
 - User data rate of Public Switched Telephone Networks: 9600bps (modest compared to data networks)
 - Maximum time to set up a call through the PSTN (telephone network): up to tens of seconds (very long). Owing to the type of equipment used for the exchange
 - Average time to set up a call through digital PSTN: as low as tens of milliseconds and getting shorter. 
 - Bit rate available to subscribers on ditigal PSTN: 64kbps or higher (high)
 - Network access protocol defined to interface a DTE to a PSPDN: X.25
 - DCE data rates: between 600bps and 64kbps.




## Exercises

### 8.1
Describe the differences between a circuit switched data network and a packet switched data network. Clearly identify the effects on the users of these networks.

### 8.2
Explain what is understood by the following terms used in relation to packet switched data networks: 
a) Datagram, 
b) Virtual call (circuit), 
c) Logical channel.

### 8.3
Use sketches to illustrate the applicability and components of the X.25 network access protocol and write explanatory notes describing the function of each component.
