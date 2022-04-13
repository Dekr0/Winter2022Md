# TCP

- It create a illusion that there's a permanent connection and bidirectional bytes pipeline. 
- UDP is a light weight version of TCP that does not require response from the receiver (like sending time, etc).
- TCP only focus on transferring bytes back and forth. It is up to the application layer to interpret what those bytes mean.
- TCP is rather complicated and application layer don't need all the services provides by the TCP.

------

## Packet Structure

------

- Port number identifies an application within the node
- The UDP and TCP segment are within the IP payload => Data Field
  - There is no IP address. It's provided by IP Protocol.
- All data bytes always contain a sequence number regardless how many it's split by IP layer because the first data byte always is a **sequence number**
  - The sequence number specify the order of receiving packets to ensure data doesn't get lost.
- The acknowledgement number
  - notice that it identifies the sequence number of the next data byte. 
    - This implies the all previous byte are received successfully.
  - if acknowledgement number does not match, then packets are most likely lost in the transmission
    - Wait for retransmission of the missing parts until the data go through (sender will keep sending it)
- For example, if one send ACK. number 1001 to another the end
  - this mean the previous all 1000 segments were received, 
    - or this end received number 1000 byte without lost and it need the next byte -> 1001

------

## State Machine

------

- SYNC Packets / Segments (Check TCP/IP Illustrated, Page 307)
- SYNC-SENT and SYN-RCVD record the progress of establishing connects.
- SYNC is the flag in the segments
- The server might make a copy of itself (child processes) to accept multiples clients.
  - There is not only one state machine.

------

### Establish Connection Process

------

- The SYN segment is sent when a client want to make a connection.
- The client is expected to receive an SYNC + ACK segment to come back from the server.
- The client is then send an ACK segment to the server.
- Everything need to be acknowledge to ensure another side receive the message.

------

## BOOTP And DHCP

------

- When a machine is live and is required an IP address, it needs to send UDP segment to port 67 where the BOOTP server resides.
  - BOOTP server has a pool of hardware addresses and can be assign to each machine.

------

## HTTP

------

- One can actually open up a socket to a webserver and type in all the HTTP commands manually as ASCII.
- Method, Port, Path field are optional unless one want to specifies for more specific actions
  - Default is usually HTTP but other protocols are allowed