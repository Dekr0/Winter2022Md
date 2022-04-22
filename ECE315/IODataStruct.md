# Data Structures Used In I/O Software

## Buffers

---

- What is overhead ? (Google it)

---

## Double Buffers

---

- One advantage : decoupling effect
  - one of two processes don't need to be blocked until another finish
  - two processes might have different processing speed - synchronization
- Advantage - example
  - write an image into the buffer but it won't be available until the scene of the entire is built up.
  - writing order and reading order can be different between two processes.

---

## Stacks

---

- Dangerous of stack :
  - stack overflow : 
    - cause : 
      - recursion (keep storing the current context of the memory and end up trash the memory, overwrite the content of OS). 
      - try to store large memory in the stack
- Fast and efficient way to manage memory

---

## FIFO Queues

---

- Decouple producer and consumer processes
  - easy to design and verify
- Provide elastic storage
- It is not always the case that a new datum is pushed to the back end of the queue
  - High priority task, respect priority.
- pointer for FRONT and BACK both move simultaneously.
- Main fundamental issue of FIFO : both pointers of the queue move in memory
  - may lead to overwrite content in the memory.
  - need to contain a queue in fixed region of the memory.
  - solution : circular buffer

---

## Circular Buffers (Queue)

---

- Need to determine the maximum capacity

- What happen if write pointer = read pointer ?

  - means both empty and full, which is ambiguous
    - need empty flag and full flag

- `mod N` is used to wrap around

- Circular Buffers can appear in a device driver such as Ethernet and other communication devices

  - ISR will fires when something arrive / there are more data to transfer when the device is IDLE / etc.
  - It is better to copy the buffer to/from the user provided buffer to pool of buffers in device driver

- Device driver is a software and the data structure to run a hardware interface

  - have to be trusted, expert-designed code because many users are using it and should be done correctly
    - It's something one doesn't want to do if one doesn't have any prior experience.
    - It take a lots of time get it right so it's better to use existing build and modify on top of it.
  - Device driver are generic because they need to handle many different hardware interfaces.

---