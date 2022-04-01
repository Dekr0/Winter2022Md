# Network Topology

- Topology: 拓扑 - 物体间的位置关系.
- Topology studies properties of spaces that are invariant under any continuous deformation.

------

## Type of Network Topologies

------

- Ring
  - one single logical token will be passed around the ring.
  - one that holds the token have a permission to transmit.
  - If a single token is lost, nobody can transmit
    - How to fix it?
      - A system check the arrival of a token with timeout
      - Reset token
  - If having n tokens, collisions can arise
- Mesh - any arbitrary nodes connection
- Fully connected
  - It's very expensive because the number of edges grows in square of the number of nodes.
  - Ideal for supercomputer center

------

## Ethernet Frame Format

------

- The last two in SFD indicates the start of transmitting content
- In the present time, data length is usually longer the amount of data can hold in ethernet frame.
  - This means that data is actually sent in number of packets
  - Notice that sending multiple packets is no very effective because of overhead

------

### Checksum

------



------

