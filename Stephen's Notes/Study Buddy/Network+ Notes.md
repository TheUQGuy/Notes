## Chapter 1
### The OSI model
![[Pasted image 20250906121739.png]]

#### Physical Layer
The physical layer sends and receives bits (electric pulses) symbolizing 0s and 1s. They use the medium of Unshielded Twisted Pair Cables which are sent to a cable center known as a central box. 

#### Data Link Layer 
To interface between multiple devices, they made a Network Interface Card (NIC). 
##### NIC
Used to be a PcIE card that was an addon, but now is embedded into each motherboard. The NIC contains the necessary MAC address that makes the Data Link Layer Run.

##### MAC
The MAC address stands for Media Access Control address and is a 48-bit value. This value uniquely identifies each network device and allows inter-communication across the data link layer.

The address is assigned by the IEEE (institute of electrical and electronics engineers) and is denoted by 12 hexadecimal characters. The first 6 characters are reserved as each manufacturer's unique ID, also called the OUI (organizationally unique identifier). The last 6 characters are the device's unique ID.

Also known as physical addresses.

##### Frame
A Frame Encapsulates the large string of incoming bytes into groups.
This Frame is then read and interpreted by the NIC

![[fields-of-frame.png]]

###### FCS
FCS is the trailer of any given frame. It is 8 bytes long and has a checksum that double checks that all data is intact. It uses something called a Cyclical Redundancy Check (CRC).

CRC is a modulo calculation of 4 bytes that calculates the remainder of the other 1496 bytes in the frame. The NIC then runs its own calculation on receiving the frame and if it doesn't match, it drops the frame and waits for the next one.  

By Ethernet standards, each frame carries 1500 Bytes and a Frame makes sure that 2 NICs don't speak at the same time. 

The central box/hub initially sent all frames to all devices connected to it. As a result networks would bottleneck quickly with each connected device having to drop the frame if it wasn't the desired recipient

Recently these dumb hubs were changed to a switch which filter things by mac address.

So how does a NIC send data to a new MAC address?
- It sends a broadcast signal across the FF FF FF FF FF FF MAC address
- The broadcast signal will be processed by all attached NICs
-  The receiving computer will use [[#Network Layer|IP]] to send the frame to the best-fit next device in the chain. 
- Once the desired MAC address is hit, it sends back the desired MAC address

##### Putting it all together (Frames)
- The sending system sends data to the NIC.
- The NIC then builds a frame to transport that data to the receiving NIC
- The frame consists of the send and receive addresses, Payload and the Trailer with the FCS containing the secure CRC modulo calculation
- The frame is sent down the wire into the central box. 
- The switch sends unicast frames (when frame is addressed specifically to another device's MAC address) to the recipient address.
- In tandem, the switch also sends broadcast frames to all systems on network
- The receiving NIC strips all of the excess data off the frame and sends the remaining data to the OS

Data link layer is distinct because it is split between the Media Access Control (Converting the upper layers to the physical layer), checking the FCS and sending frames down the physical layer and the Logical Link Control (LLC) which takes frames to the operating system and network protocols.

As a result Layer 2 is the only layer that is split, AND NICs are technically both layer 1 and 2 of the OSI model.

#### Network Layer
The problem with MAC addressing is that for super large networks, you have to broadcast over and over to every device in the world in order to find a specific address. 

The solution to this is in the network layer where large networks are divided into subnets that are then routed to.

##### TCP/IP 
TCP/IP is a suite of various protocols but with TCP and IP doing the bulk majority of the work. 
IP is in the network layer and TCP is for the [[#Transport Layer|transport layer]]. 

At the network layer, packets are created and addressed so they can go from one network to the other. In order to do this they give each computer an IP address

##### IP
An IP address is a unique identifier of 4 8-bit integers. It is normally denoted by 4 numbers separated by periods. It is also known as a logical address

192.2.16.31

No 2 systems share the same IP address. What makes logical addressing work is a router that interconnects the subnets. A router makes it so that we don't only have to use ethernet in order to connect multiple devices together. This makes it possible to do things wirelessly through wifi and other connections.

In TCP/IP every device has both a physical and logical address.

##### Packet 
For IP and TCP to work, the frame contains MAC data in its wrapper, and its payload is an inner container that provides IP information to route the packet.
![[segmentpacket.webp]]

When sending data across the web, each router strips the frame, analyses the packet for the IP details, then repackages the frame with new MAC details so it can get sent along the chain. 

Segmentation is the process of splitting a large quantity of data (say a large file) into size appropriate frames. These segments are compiled and assembled into the full file by the recipient device.

Data segments have a sequence # (In contrast to datagrams in layer 4 which don't have sequence numbers)

#### Transport Layer
Transport layer has a bunch of different protocols by which to send different types of data.
There is SMTP- simple mail transfer protocol by which to send simple emails.

Typically there are 2 types of transport protocols. Connection-oriented which would be TCP (transmission control protocol) and connectionless which is UDP (user datagram protocol).

TCP deals its data in segments. The main features of a segment is that it deals in ports and has sequence and acknowledgment numbers. 

![[tcp-header.png]]

##### Port
A port is a number between 1-65536. Each port number is assigned to a specific service. Classic examples of a web server use port 80 and port 443.

#### Session Layer
A session is just an ongoing connection between 2 devices. Multiple sessions can be ongoing but cannot use the same port at the same time. 

A session is denoted by IP:Port -> IP:Port
	1.1.1.1:75        2.2.2.2:80

#### Presentation Layer
This translates the TCP/IP data to useable data. It has some dificulties and debates on what constitutes layer 5 because services like transport layer security (e-com encryption) starts in the session layer and crosses over into presentation for encryption/decryption.

#### Application Layer
Application Layer is the code of individual applications that allows the use of network.

Most do this through the use of Application Programming Interfaces (APIs).

Encapsulation is the process of taking data from the Application Layer, and compartmentalizing and wrapping it until it hits the Physical Layer.
Decapsulation does the opposite.

## Chapter 2
### Network Topologies
![[Topology Diagram.jpg]]
#### Bus topology
A straight line that require terminators at the end of the cable so that the network doesn't fry as the signal  reflects back through the cable otherwise.

#### Ring topology
Ring topology is where all of the computers interconnect to one another

In both star and ring one cable break destroys the whole network

#### Star topology
Star topology/hub-and-spoke topology uses a central box as a main connector to the other computers. It offered fault tolerance where if one cable broke the others could continue communication.

It wasn't as successful because it was hard and expensive to rewire the previously existing networks into star ones.

Instead they did a hybridization of star incorporated into the bus and ring topologies. In Ring they put the ring into the switch box and used that. In bus they routed all of the cables through the box but kept the same functionality.

#### Physical Topology
The physical topology is what the actual wiring looks like (in the hybrid cases the physical topology is the star).

#### Logical Topology
The logical topology/signal topology is what an electrical diagram would show, in this case it is the bus and ring topologies respectively.

#### Mesh Topology
A mesh topology is where each node is connected to at least 2 other nodes. Partially meshed means that at least 2 nodes have redundant connections. In a fully meshed system, every node connects to every other one

![[Mesh topology differences.png]]


### Network Technologies
Network technology is a practical application of a topology that gets data from one PC to another.

#### Network Cabling
The most common form of cabling is called copper cabling which are coaxial and twisted pair cables.

##### Coaxial
![[Coax Cable.jpg]]

Coaxial cable is copper conductor wire surrounded by a braided shield. It is called coaxial because the wire and the mesh share an axis (co-axis). This mesh over wire, shields the transmission from interference. Many devices generate magnetic fields which leads to electrical currents hitting the wire. Extra current is called electromagnetic interference which can be interpreted as a signal.

Old bus topologies use bayonet coax connectors (BNC)
![[Bayonet Connector.jpg]]

Whereas now they use F-Connectors which connect ISP from a cable modem![[F-Connector.jpg]]
In TV they use RG-59 and RG6 graded cabling which are rated at 75 Ohms

##### Twisted pair
Twisted pair are twin axial cables that have 2 copper cables wrapped around a shield. It is a short version of fiber and is much cheaper. This fiber substitute is also known as direct attached cable (DAC). 
![[Twisted Pair Cable.jpg]]

The twisted pairs reduce crosstalk (talk between pairs) thanks to the jackets. 

Shielded twisted pair (STP) are shielded to prevent EMI risk. They are differentiated on which part of the cable is shielded. 

![[UTP Cable Types.webp]]

Unshielded twisted pair (UTP) is less resistant to EMI but is much cheaper than the STP variants.

#### Cat Ratings
![[Cat-Cable Ratings.png]]

Regulating CAT ratings is the International Org of Standardization (ISO) and American National Standards Institute (ANSI). 

Bandwidth is amount of data that goes through the cable per second

Devs have implemented bandwidth-efficient encoding schemes which means squeezing more-bits into the cable if possible.

Cat5e can handle a throughput of 1 Gbps even though its rated to handle 100Mhz. Most use Cat6 as of now. 

Old landlines plug with a registered-jack (RJ) connector. Telephones used RJ-11 connectors whereaas now we use 8 position 8-contact (8P8C) which is colloquially known as RJ-45. 

#### Fibre
Fibre juxtaposed to twisted pair uses light as the means of transmission. This makes it reachable for much longer distances or for places with lots of EMI.
Glass fiber has the glass core, cladding (what makes light reflect), a buffer and the insulating jacket.
![[Fibre Optic cable.jpg]]

Fiber has 2 measurements according to the core/cladding. Commonly 9/125 50/125 and 62.5/125 micrometers. Originally they would have one cable for sending one cable for receiving but nowadays they run duplex. 

Multimode-fiber uses LEDs (MMF) whereas single-mode fiber uses lasers (SMF).
MMF wavelengths are either 850nm or 1300nm
SMF wavelengths are 1310nm ir 1550nm

MMF has modal distortion where signals sent at the same time don't arrive at the same time. 

The four main connectors are ST SC LC MT->RJ

![[Fiber Connectors.webp]]

LC and MTRJ are duplex whereas SC and ST are single.
Snap & twist= ST
Snap & Click = SC
lil connector =LC

Fire ratings on cables are plenum vs PVC (polyvinyl chloride)
Plenum=fire resistance but very costly. Buildings require plenum cabling
PVC is not fire resistant but much cheaper.

IEEE has a committee called 802 which defines frames, speeds, distances, and types of cabling.

![[802 IEEE standards.jpg]]

## Chapter 3
The chain of ethernet development was:
bus topology @ 3Mbps -> DIX Ethernet @ 10Mbps -> IEEE for additional standards.

| Standard | Description                                  |
| -------- | -------------------------------------------- |
| 802.3i   | 10Mbps Ethernet using twisted pair           |
| 802.3ab  | Gbps over twisted pair                       |
| 802.3by  | 25Gbit over fiber                            |
| 802.3cm  | 400Gbit over MMF                             |
| 802.3cu  | 100Gbit-400Gbit over SMF using 100Gbit lanes |
CSMA/CD is the process of finding out what goes where with collision detection.
![[CSMACD.webp]]

Thankfully frames prevent the monopolization of the bus and makes transmitting data more efficient.

![[Ethernet Frame.jpg]]

The preamble is a sequence of 0s and 1s in the form of 1010101 which gives a NIC time to recognize it is a frame. Then it has the destination IP and SRC address. The type differentiates between IPv4 and IPv6. The data is the payload of the frame which is padded to make the frame minimum of 64bytes long. 

FCS contains a cyclical redundancy check and attaches the result at the end. This is meant to check the accuracy of the frame and verify if the frame has been tampered with or contains errors. 

Initially the router just sent everything down every other channel but advanced switches can avoid things like this.

### Ethernet Standards

Num Base-XX
Num-> Refers to the speed in  Mbps
Base-> Refers to Baseband (cable carries 1 signal)
XX-> Refers to the cable type. T being twisted pair

#### 10Base-T
Was the original ethernet signal. 10Mbps via connection to a hub. It used Cat3 UTP cable in doubles with an RJ-45 connector.
It had 4 pairs of cable but only used 2 pairs for various reasons. 1&2 sent data whereas 3&6 receive data. That said, even with multiple pins they couldn't send and receive data at the same time.  

NICs that can only do one task at once run what's known as half duplex whereas those that can send and receive data at once run full-duplex. 

##### RJ45
The RJ-45 is known as a crimp which is the process of adding the end onto the UTP wire.

 ![[Pasted image 20251113161555.png]]
The difference between 568A and 548b is GO, green is first for A and orange is first for B.

##### 10BASE-FL
10BASE-FL is the fiber based alternative to 10BASE-T. First, 10BASE-FL could go for over 2km which addresses the distance issue. The second strength is the resistance to EMI that twisted pair lacks. It uses 62.5/125um with ST-SC connectors. It also uses single band/half-duplex so it requires 2 fiber runs. 


#### Standards Summary
| Standard  | Speed  | Type     | Distance                | Node-Limit | Topology                  | Cable          |
| --------- | ------ | -------- | ----------------------- | ---------- | ------------------------- | -------------- |
| 10BASE-T  | 10Mbps | Baseband | 100m between hub n node | 1024 nodes | Phys-Star logic-Bus       | Cat-3          |
| 10BASE-FL | 10Mbps | Baseband | 2km from node and hub   |            | Physical-Star Logical-bus | 62.5/125 ST-SC |
|           |        |          |                         |            |                           |                |
|           |        |          |                         |            |                           |                |
|           |        |          |                         |            |                           |                |

## Relevant Commands
```
nestat -a #shows all ports and sessions active
```