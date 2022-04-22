# Synchronization and Flow Control

- When interfacing, there is a wide range of data (I/O) rates required to handle.
  - It is not easy to deal with.
- There is a mismatch between the CPUs' clock rate and the data rate of I/O devices.

---

## Storage Unit

---

- longwords - 4 bytes

---

## Spectrum of I/O Data Transfer Methods

---

- Polling
  - for slow I/O devices
    - A2D converted
    - Sensor
    - etc.
- Interrupt-driven
  - Notice that ISR **need to be fast**.
  - So **usually** ISR **doesn't handle** data transfer 
  - instead of **unblocking an application** such that it can perform data transfer
  - ISRs are **asynchronized** so they are **unpredictable**
- DMA
  - Why are so fast ?
    - DMA doesn't **need** to do fetch, move, decode and execute **instructions**.
      - **no executing code**.
    - DMA only perform read and write in the bus in a signal level.
  - CPU can setup a DMA transfer and handling other tasks
    - How a CPU notice a DMA transfer is finished ? ISR
  - Avoid doing DMA on the memory that 
    - need to be **cached into the CPU** 
      - because the **updated data** in the cache but it haven't **written back** to the **main memory**.
        - If DMA is moving data from the main memory, caching need to be turned off because data can be out of dated
      - DMA doesn't go into cache memory instead of main memory.
    - or virtual memory that swap back and forth from secondary storage
      - because pages can be transferred during the processes
- Each transfer method has its own usage depend on the situation, not suited for ever single cases.

---

## Polling

---

- Polling overhead - the amount of CPU time consumed during polling
- Polling time on data transfer in 16-bit words with data rate of 500 KB/s
  - Data rate 500 * 2^10 bytes per second
  - Transfer two bytes at a time (16 bits) 0.5 * 500 * 2^10
  - Each time transfer two bytes, need to poll, thus
    - 100 * 0.5 * 500 * 2^10 
- Polling time on data transfer in 512 byte bursts at an average data rate of 20 MB/s
  - Data rate 20 * 2^20 bytes per second
  - Transfer 512 bytes at a time (20 * 2 ^ 20) / 512
  - Each time transfer 512 bytes, need to poll, thus
    - 100 * (20 * 2 ^ 20) / 512
- When polling overhead is less 1% of the CPUs time, it can be ignored.

---

## Interrupt Management

---

- Priority of ISRs
  - safety, power failure, data corruption, serious malfunction and so on, they are important ISRs
- All ISRs need to be handle fairly quickly and they need to have execution time.
  - Although all ISRs are fired, CPU still needs to be able carry on and finish its tasks.
  - If a CPU is overwhelmed by ISRs, need a faster CPU or split ISRs to another CPU.
- Device drivers
  - For example, if a device send a interrupt signal to an interrupt that is already being used by other devices ?
- Hardware for handling interrupt are provided
  - It's up to the system designers to decide 3 design decisions to ensure bad service does not happen as well as good performance.


---

## DMA

---

- Move graphical data, bulk data, etc. => large quantity of data
- DMA are usually set up by software trap
  - Privilege software normal application cannot use
    - Handling various issues by OS / expertise  software.
      - are memory location ok?
      - are memory location being cached?
      - etc.
  - requires times and overheads
    - not worth it just to transfer a few bytes
- Despite of CPUs can exploit locality and then perform caching technique, 
  - executing multiple "MOVE" instructions along with other instructions is still time consuming  compared to DMA.


---

### Potential Complications with DMA and Solution

---

- Recall virtual memory
  - using a 64-bit addressing space but definitely don't have enough physical storage (2^64) for this addressing space in main memory
  - have to temporarily move parts of available virtual memory into hardware memory (secondary storage ?)
  - Pages are block stored in main memory for access in the memory.
  - other reason ? ECE 311

- Provide DMA controller with address translation H/W
  - It is expensive because it need to synchronize address translation from all the users who use virtual memory.
- Do DMA only within page boundaries in physical RAM
  - If DMA is doing the data transfer involve a page, 
  - pin it to avoid that page being swap, 
  - do the data transfer with the page being locked
  - unlock the page and is available to swap as soon as DMA is finished.

---

