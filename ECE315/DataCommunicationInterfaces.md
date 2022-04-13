# Data Communication Interfaces

## Data Communication Protocols

------

- The purpose of protocol is to provide safe communication between agents.
- Five elements of a communication protocol (apply to all communication protocols in general ?)
  - vocabulary: what kind of message need to be sent and received
  - encoding: how to encode message into bits

------

#### Session and Application Layer Protocols

------

- A **session layer** protocol provide rule and guideline to set a up a session
- A layer is used and guarded by another layer and its protocol once it's setup correctly.
- Four general steps use 
  - Request
  - Indication
  - Response
  - Confirm

------

### Layered Protocol

------

- Connections between layers that are not lowest are virtual.
  - They are all handle by lower layers down the chain.
  - Layer N wants to communicate to another entity's Layer N by requesting Layer N - 1 to set up the connection.
  - Detail in the lower layers are hidden 
    - (information hiding, ignore information that is not important to current layer)
- Layer N Protocol Primitives can apply to any layer level.

------

### Protocol Overhead in Data Packets

------

- When data / message is pass down to each layer stack, each layer will attach a header used on this layer for various use
  - error detection
  - addressing
  - etc.
- At the end, all these header and the actual data become bit 0 and 1.

------

### OSI Protocol Interface

------

- Layer 7 to 4 only focus on end-to-end (focus on four general steps, request, indication, response, confirm ?)
- Layer 3 to 1 only focus on communicate aspect and detail between nodes

------

#### Routers

------

- WAN is wide area network, the main network over a specific range of area (e.g. outside the house)
- Local (e.g. Wi-Fi )