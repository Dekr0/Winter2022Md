# Ethernet Interface on Zynq-7000

- Flexibility, elasticity, overhead, decoupling.

---

## Structure Overview

---

- Two Gigabit ethernets have registers mapped in the addressed map visible to the CPU.

  

- 512 KB L2 Cache & Controller is connected by two gigabit ethernets but in fact is ignored.
  - Registers are volatile and easy to change
  
  - If the content in a register is read and cache has a copy of it in the cache, 

  - and one relies on the copy to define what the register contains, one can be fooled by this.
  
    
  
- There are various of ISR available produced by the two Gigabit Ethernet controllers (like SPI and UART).

  

- Once one is committing to sending a ethernet frame, need to supply bits in very high rate, and supply data really quickly => 
  - high speed port (for both receiving and transmitting)
  
- Also, delay is not allow because bits and data are sent in such a high fix rigid rate, 
  - any delay will trash the transmission
  
  - require a buffer for overhead so that 
    - when one needs to transmit the bit, there are supplies of bit ready for transmit.
    
      
  
- Control registers are used to config how the Gigabit Ethernet operates

- Advantage of reducing pin in RGM-II :
  - number of package are smaller
  - less soldering join
  - more reliable

---

## GEM Architecture

---

- DMA controller is included for block of data movement
  - numbers of MOVE instructions are inefficient because it requires fetch, decode and execution
  - DMA can issue one instruction and transfer a block of data
- Key operating statistics can be used for error-checking, billing and others used.

---

## Transmit and Receive Buffer Overview

---

- Think of ethernet is a paper of letter. The letter itself is the payloads.
- Ethernet (transportation sequence) doesn't care what's in the payloads, it's just a sequence of bits
- Ethernet was built for shorter transmission so that it's reliable 
  - because larger / longer data are easily corrupted in the time when Ethernet was developed.
  - Optical fiber have very low error rate, it's make sense to have longer packet instead of short one
  - However, Ethernet has became a standard.
    - Lots of traffic are short packet.
- Shorter packet is not efficient because the ratio of overhead to data is higher than it should be.

---

### Tx and Rx Buffer List

---

- ```
  +---------+
  | pointer |
  +---------+
  | control | 
  +---------+
       -
       -
       - 
  array of pointer descriptor shown above
  ```

- pointer descriptors have two fields

  - buffer pointer
  - control field : size of the buffer and various other flags

- When processing data buffers, process the first one until the last one and wrap around (circular buffer) (for both Tx and Rx side)

  - Wrap = 1 means the last buffer in the circular buffer
    - indicates wrap around is required next

- Buffer descriptor lists have the flexibility make the length varies

  - Longer list, a stack of ethernet frames can be built up and ready to go
    - then, the software can load the frames and perform other things

  - Longer list can decouple the process of loading the frames and sending the frames from other tasks the CPU need to do.
    - Same for receiving side, let them stack up together


---

### Ethernet Frame

---

- 64 bit for each buffer descriptor
  - first 32 bits is pointer
- Example, using 4 buffer descriptor to store 1 ethernet frame (Chapter 7).
- L(ength): bit #11-0 is set to 1 when
  - how many bytes within the frame just received
  - hardware will look into length field when receiving the bits so it know what it exactly to expect, 
    - and if CRC is correct
    - then length field is set
