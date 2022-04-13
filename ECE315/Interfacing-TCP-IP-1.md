# Interfacing Kernels to TCP/IP

- TCP / IP communication must be protected from various type of things
  - context switches,
  - ISRs from H/W,
  - IRQs from Tx & Rx hardware,
  - H/W timers.
- There can be multiple buffer in different places (OS, stack protocol layers and so on).

------

## Protocol Layers as Tasks

------

- It allows work at one layer at a time without interfering other layers.
- Context switching cost time
- Buffers are shared among different tasks. They need to be carefully controlled (Synchronization).
- If TCP task want to look down and access information in the IP task, it need to communication with other tasks. It slow things down.

------

## All Layers Into One Task (Outside Kernels)

------

- User need to use msg. passing and function calls to access the task.
- Task have complete control over the stack protocol and it can take shortcut as much as it can to gain efficiency.
- Task can be written in generic C and be ported to other kernels with making minimal assumption of other OS. 
- The stack might have its own buffer complied by C.
- Code based is not protected.

------

## All Layers Into One Task (Inside Kernels)

------

- They are usually daemon processes that are running in the background and not visible.

------

## The NetBurner TCP/IP Stack for MicroC/OS

------

- The hardware driver task has the highest priority.
- Once the device is committed a communication to another device, that task must operate at hardware speed.
- The driver task need to keep up with the speed of transmitted packets.
- When the packet is received, it must be handle by first the lowest level (hardware driver) otherwise it will be lost.
- Delay cannot be tolerant in terms of physical transmission of the packets.
- It make sense that IP has the higher priority than TCP because IP need to be handle first before TCP.
- If IP layer is not handle fast enough, it will be unable to handle TCP.
- This OS cannot have two tasks in the same priority.