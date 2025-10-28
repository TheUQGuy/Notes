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

## Relevant Commands
```
nestat -a #shows all ports and sessions active
```