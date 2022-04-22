# Flow Control

- Flow control is to deal with problem of which data production and data consumption are not exactly same.
- stop (slow down) production if a buffer is full (nearly full), then restart (speed up) consumption or
- stop (slow down) consumption if a buffer is empty (nearly empty), then restart (speed up) production.
- Requires a feedback so that control signals can send back the transmitter
  - seen in stepper-motor
- Control signals can compensate such that the flow of data out of the transmitter and in of the receiver is equal.

---

## Flow Control Mechanisms

---

### X-on / X-off Flow Control

---

- FIFO buffer provide some elasticity but when transmitter is producing data faster the receiver can consume
  - buffer will fill up and new transmitted data will be lost (no space to save)
- Manually sending X-on and X-off isn't reliable.
- What if receiver incorrectly sends an X-off, X-on will be lost, 
  - in which case both transmitter and receiver are both waiting (similar to deadlock)
  - setup a timer, send a X-on / X-off, if nothing changes, try again.
- Cons : 
  - relatively slow response time if done in software especially if one is operate very high hardware speed
    - it would be too late when transmitter receives X-Off, data can be lost.

---

## Ethernet Flow Control Using Pause Frames

---

- A receiver can keep sending pause frame to keep the pause period extended.
- When a receive is ready, stop sending pause frame so that the transmitter will resume. 

---

## Hardware Flow Control

---

- To disable hardware handshake signals if one doesn't need it
  - via wiring
  - feed RTS wire back to CTS terminal in the same side
  - or both RTS wire to DCE and CTS wire to DTE to 0.

---

## Flow Control in TCP

---

-  Before establish a TCP/IP connection, both side needs to negotiate for the correct windows size.
  - Window size of two sides can be different
  - prevent bytes arrive in the burst fashion such that it overflow the circular buffer,
  - overwritten some old content in the buffer / bytes start fall over the place in receiver's side and lost

