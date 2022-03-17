# Sockets

## Design : Unified Interface

------

- C struct to exchange information between processes and OS
  - struct varies from domain and address family
- A number of API function applied for all types socket
  - one argument appear in all function is generic struct `sockaddr` 

------

## Internet Layer

------

- Application layer (layer #5 / top layer) : 
  - programs (client / server) reside in this layer
- Transport layer :
  - Establish logical connectivity between two processes (same / different machine)
  - TCP / UDP - transport layer protocol
- Network layer :
  - Provide connectivity between two network interfaces (hosts)
  - Each network interface is assigned with network layer address based on network layer protocol (IPv4 or IPv6)

------

## TCP Sockets

------

### Transport Layer

------

- important information : port #
  - source port #  client listening
  - destination port # server listening
- A host can have queues for different types of sockets
  - A queue of UDP sockets
  - A queue of TCP sockets
- When packets are sent into the host, transport layer needs to redirect each packet to the correct socket queue
  - Transport layer use demultiplexing to redirect them
  - Demultiplexing use port number to redirect packet to the correct socket queue

------

### Network Layer

------

- Network layer address consists of two tiers
  - network part (most significant)
  - host part (least significant)

------

## Sending and Receiving

------

- `recvfrom()` and `sendto()` remark : UDP has no notion of connection.
