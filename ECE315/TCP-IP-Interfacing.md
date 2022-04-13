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
- It provide an application interface,`IwIP API` (like socket).
- IwIP core interact with the system using OS Emulation Layer
  - The layer make minimal assumption about the OS.
  - Simple messaging and timer.
- The IwIP Core is respond to running the Network H/W.
  - There must be a device driver layer.
  - Different network interface can have different device driver.
  - All drivers are pretty similar in face because the software covers up hardware differences.
    - This end up having a table of drivers and pick up what driver based on demand.
    - For instance, a pointer points to a specific driver.
- 