# TCP / IP

- TCP (too complicated in one) was split up into two distinct protocols for solving two distinct problems.
  - One is reliability and correctness of the datagram
  - One is addressing
  - TCP layer provide reliability and correctness / patch the issue on IP layer (lower layer)
  - Divide and Conquer, use Layer protocol's advantage
- Once the number of participates in a system reach a critical size, there is snow ball effect 
  - (for example, more and more people want to join into the Internet).'
- Payload portion of the packet contains the data that a user or device wants to send.

------

## Context of developing TCP / IP: 

------

- There various types of transmission protocol: tokens ring, various favour of Ethernet, and other protocol
- One basic commodity among those protocols are used packet based transmission
  - data and information are packed into small packets
- Headers and size of the packets are different among those protocols
- How to make use of these current situation to create something that can works in all current existent protocol? 
  - First thing it's coming up a naming scheme to uniquely identify each node in WWW. 
  - This naming scheme must coexist with naming scheme that already exists in the local network.
  - Each node will have one global address and local address.

------

## IP

------

- IP layer is correspond to the network layer where taking care of addressing
  - uniquely identify a node in the network and route packet around the network
- Packet based transmission system does not have permanently connection like the telephone system 
- IP provide basic function on transmission and relies on TCP handle the reliability
- IP has the flexibility to provide variable-length packet size to suit into other protocol that needs different packet sizes.
  - but it's harder to assemble due to overhead and less efficient.
- If a IP datagram is corrupted or too large, or a IP datagram has a error in the checksum, throw it out.
  - It's up to the higher layer to due with it.
- IP does not care not what's in the data field

------

### IPV4

------

- Total length - size of the datagram
  - place in the head for overhead, telling how much resources needed to be allocated
- Header Checksum provide error checking only for the header field (error -> throw it out)
- Padding for rounding the up word
- Data field consists of TCP frame (recall the data packet overhead)
- Hop limit prevents the datagram going around the internet for too long.
  - Exceed limit, delete it.
- Subnet mask is used to tell where the based address is, where the block address is, and the subnetwork (local network)
  - bitwise AND operation must perform in hexadecimal instead of decimal with dot notation
- DNS is used to convert name into addresses
- One dangerous thing about one successful standard is that it lock in the way doing things. 

------



