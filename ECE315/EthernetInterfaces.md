# Ethernet Interfaces in $\micro$Controllers

- loopback mode is good for debugging. Send its own signal back to itself. 

------

## Context

------

- Modern embedded systems have access to Internet.
  - They are network nodes
- Both advantage. and disadvantage.
  - Others can hack into embedded computer
- When an embedded computer connects to the public network, security must be in place.
  - Otherwise, network is open up to others for potential interruption.
-  Most industrial systems use wired connection.

------

- MAC is usually implemented in the $\micro$Controller.
  - Purchase one and install it directly.
- Every computer need a PHY chip to connect the Ethernet.
- Every embedded system must include a MDIO interface to control the MAC-PHY interface.
- The voltage from the cable is usually larger than the voltage a $\micro$Controller can handle.
- $\micro$Controllers usually use a MAC chip to communicate with the PHY chip.
- Isolation Transformers blocks any DC offset from Tx & Rx 
  - so that the ground voltage from both end of the cable doesn't need to be the same.
- PHY chip converts the analog signal to digital signal for MAC and $\micro$Controller.
- Anything that need to be remain the $\micro$Controller after power is turn off should be stored in the Flash Memory.
  - Essential data, configuration, FPGA configuration and so on.
  - An alternative way to is to download it from the remote server.
- $\micro$Controller can config and control the PHY chip using MDIO interface.
  - PHY chips have register and operation mode.
  - speed negotiation
  - full and half-duplex
  - different power plans
- MDIO signal goes through 2 wires that have both directions.
  - One is clock for signal, one is MDIO signal

------

## Micrel Ethernet PHY

------

- Micrel Ethernet PHY chip transfer in bits through Tx (TXD0 ~ TXD3) and Rx (RXD0 ~ RXD 3) streams.
  - Each stream is in a slower rate (25 Mbps)
  - but together it reassemble the desire rate into Tx / Rx streams that have much higher bit rate.
    - It's easier to handle electrically (Detailed ?).
- There are two independent blocks for 100 Mbps and 10 Mbps.
  - They are very difference so 100 Mbps and 10 Mbps are handle separately.
- Pulse Shaper ensures the input / output pulse are smooth without too much high frequency content.
- The clock isn't sent in a separate wire instead of embedding into the data.
  - The data will passed into a separate clock stream after decoding.

------

### The Manchester Code

------

- The Manchester code provide a way to encode the clock into the data. 
- 0 and 1 are represented in two separate transitions.

------

### The MLT-3 Line Code

------

- This encoding can avoid expanding the frequency of the content too much.
- It encodes more information because each bit has 3 levels instead of 2 levels.
- There are 3 voltage levels in 100 Mbps
- There are 7 voltage levels in 10 Gbps for 4 twisted pairs in both Tx and Rx direction.
  - It's much more complicated.

------

### PHY 100-Mbps Transmit and Receive Signals

------

- Raw serial data rate = 100 Mbps
  - MII Transmit Data (// inputs) at 25 MHz with 4 transmit streams TXD[3:0].
  - TXD[3:0] transmit 4 bits at a time overall.
- TX+/TX- analog bit signals is at 125 MHz because of 4B/5B line code.
  - increasing the bit rate by 25% => 100 MHz * 1.25 = 125 MHz.
  - an extra bit is included, 5 bits instead 4 bits.
- PHY on the receive side first finds out the clock, taken out the extra bit for encoding purposes
- Then, processing 4 bits one at a time RXD[3:0]
- The frame is discard even if there is one dirty bit within