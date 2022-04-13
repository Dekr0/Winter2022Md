# Interface Kernel to TCP/IP

- Recall NetBurner TCP/IP Stack
  - Cautions
    - There is overhead to do multitasking between different tasks.
    - Data buffer are shared among tasks. Since data buffer are passing back and forth between task, there must be some protection to ensure only one task can access the data buffer once at a time.
    - Security concern. It is possible for an application to pierce into TCP/IP headers. 

------

## FreeRTOS+TCP

------

- Before the TCP/IP stack is initialized, there should be no task using the TCP/IP stack.
- A graceful socket shutdown
  - wait for everything to finish transmitting before shutting down. 
- Issues: some tasks may want to use the TCP/IP stack but those tasks should be created after the TCP/IP stack is initialized properly.
- `vApplicationIPNetworkEventHook` function will be called after initializing the TCP/IP stack,
  - then create all the tasks that wants to use the stack.
  - a skeleton program 

------

## Client-Server Interaction Using FreeRTOS

------

- Server task will create a child task and pass the socket created by `accept()` into the child task to let it handle client connection
- For performance issue, the child socket task might not be deleted. The server task might create a pool of child socket tasks instead.
- Once the connection is closed, the child socket task will be return back to the pool of child socket tasks.
- The port number is not bind for the client side. 
- The port number can be varied depends on what type of application the client is using
- Why create a socket just for sending data (or one transmission)?
  - There are some protocols (such as HTTP), they create a socket for a webpage transmission.
  - The webpage transmission can take several TCP segments to send.

------

## The Lightweight IP (IwIP) Stack

------

- One limitation (very serious): only one application task can be using sockets at a time.
  - If one is building an embedded system for industry systems and other similar systems, and usually have one server within in the system, this limitation will be fine.
- For a multitasking operating system, there must be a thread to run IwIP stack.
- If a task want to use the stack, that task need to communicate with the stack.

------

### Architecture

------

- CPU with a C compiler
- Hardware Timer for accurate time measurement.
- Network H/W (WIFI, 5G modem, etc.).
- RTOS Port, layer of software that handle processes' detail such as context switching, the number of register in the CPU and so on.
- RTOS Core, C function call to access the function in the OS.
- RTOS Configuration

------

### IwIP Core

------

- It's implemented in the thread.
- It has its own data buffer system for running in the stack that is compiled in C.
  - It's independent from the OS buffer system.
- It provides an application interface,`IwIP API` (like socket).
  - Information hiding.
- It restrict the usage of user on the TCP / IP stack to prevent unsafe behaviors.

------

#### OS Emulation Layer

------

- IwIP core interact with the system using OS Emulation Layer
- The layer make minimal assumption about the OS.
  - Simple messaging and timer.
- If OS is changed, the only thing needed to be change is the OS Emulation Layer.
- It's very portable.
- One-shot timer is used to control retransmission of TCP segments
  - records the time lap between each segment it sends out

------

#### IwIP Core with Device Driver

------

- The IwIP Core is responsible for Network H/W.
  - There must be a device driver layer.
- Different network interfaces can have different device drivers.
- All drivers are similar in face because the software covers up hardware differences.
- A table of drivers are available for IwIP Core to select. based on a specific network H/W.
- When making a function call from a specific driver, it will have a pointer points toward that driver.

------

### TCP / IP Data Processing

------

- There are two buffer for two directions.
- They have a period of life time.
  - Receive: Load -> unload -> recycle
  - Transmit: Load -> pause for transmission -> wait for ACK -> ACK -> recycle
- They are in shared heap space but have different life time.
- TCP checksum covers the entire TCP segments.

------

#### Receive Direction

------

- When something arrives in the cable, there's a PHY chip for listening to the signals.
  - It starts to receive symbols at a specific bit rate and collect the bits.
  - The PHY chip notifies the MAC to get ready for receive an upcoming IP datagram in terms of bits
  - Bits are dumped into the buffer system.
  - The purpose of chip is to collect buffer full of data.
- The buffer is passed to IP layer.
  - First, it requires to remove the Ethernet header (Ethernet CRC).
  - It becomes a frame, and is passed to IP layer.
  - IP layer looks for the IP header
    - The GEC chip already viewed the destination IP address to ensure the packet arrives at the right place.
    - Otherwise, that packet will be dropped or sent it out.
    - If it is router, it need to be passed to next destination / node.
  - If the destination IP address is the current destination, remove the IP header.
- The payload is passed to TCP layer.
  - look for the TCP header
  - process the TCP state machine and find the correct application
  - remove the bytes from TCP segments
  - pass the remaining bytes into buffer
- The buffer is passed to application layer for further processing.
- Buffers are passed through different layers by using pointers.
  - Users can mess up the buffer, or forget to recycle the buffer and lead to memory leak.
  - The safe approach is to copy the buffer from `tcp_receive()` to a separate buffer handled by an application.
  - Acknowledge number must be obtain before the buffer is recycled.
    - TCP layer uses the copy of ACK number to ensure that previous sent was received and acknowledged. 
    - Otherwise, retransmission if the timer is expired.
  - If acknowledge number isn't obtained, then both side can't make confirmation
    - ACKed segments are never recycled, keeping build up in the buffer, and sent to another side.

------

#### Transmit Direction

------

- `tcp_write()` add the TCP header and other fields upon the data field after application called the API send function call.
- The segment is then put into a queue and ready for transmitted.
- IP layers append the IP headers after `tcp_output()`
- IP layers output the IP datagram by calling the `ip_output_if()` routine which invoke the drivers.
- Notice that some segment in the queue are waiting to be acknowledged before transmitted.