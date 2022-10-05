# Latches and Flip Flop
---
## SR Latch
---
- Basic storage element
- It latches "0" or "1"
- S stands for set
  - Output Q = 1
- R stands for reset
  - Output Q = 0
- When a SR latch is intially power up, the initial outputs is implmenentation based
---
### NOR SR Latch
---
- R is in the top NOR gate
- S is in the bottom NOR gate
---
#### Case 1
---
1. S = 0, R = 1, Q = 0, $\overline{Q}$ = 1 (Initial)
2. Set R to 0
3. S = 0, R = 0, Q = 0, $\overline{Q}$ = 1 $\rightarrow$ Memory
---
#### Case 2
---
1. S = 1, R = 0, Q = 1, $\overline{Q} = 0$ (Initial)
2. S = 0, R = 0, Q = 1, $\overline{Q} = 0$ $\rightarrow$ Memory
---
#### Case 3
---
- Recall NOR gate
  - If one input is 1, the output is 0 regardless another input
- S = 1, R = 1, Q = 0, $\overline{Q} = 0$ (Not used)
  - It deviates the purpose of using the set and reset features of SR latch since a SR latch is designed to use either set or reset but not both.
  - It yields two possible outputs when both S and R go to 0.
    - Q = 0, $\overline{Q} = 1$
    - Q = 1, $\overline{Q} = 0$
---
#### Trtuh table for all cases
---
| S | R |    Q   | $\overline{Q}$ |
|:-:|:-:|:------:|:--------------:|
| 0 | 0 | Memory |     Memory     |
| 0 | 1 |    0   |        1       |
| 1 | 0 |    1   |        0       |
| 1 | 1 |    X   |        X       |

---
### NAND SR Latch
---
- S is in the top NAND gate
- R is in the bottom NAND gate
---
#### Truth table
---
| S | R |    Q   | $\overline{Q}$ |
|:-:|:-:|:------:|:--------------:|
| 0 | 0 |    X   |        X       |
| 0 | 1 |    1   |        0       |
| 1 | 0 |    0   |        1       |
| 1 | 1 | Memory |     Memory     |

---
### Clock
---
- A signal that goes from low and high
  - This repeats in a fixed frequency
- 0 to 1 $\rightarrow$ leading edge
- 1 to 0 $\rightarrow$ falling edge
- One can design a flip flop that is enabled when
  - the clock is high (low), i.e., level triggering
  - a leading (falling) edge occur (very short period), i.e., edge triggering
- Prevent SR latch changes right after inputs change.
- Regulate SR latch behaviour to be more predictable
- Duty Cycle = Ratio of the amount time when clock is high and total time
---
## Differences between latchand flip flop
---
- A flip flop has an additioanl enable input to control the input latch using a edge triggering (usually)
- A latch is level sensitive
  - with no enable input, directly sensitive to inputs
  - with enable input and level triggering
- A flip flop is operateable whenever there is leading (falling) edge
---
## Flip Flop
---
### SR Flip Flop
---
- Notice that part of circuits of SR flip flop is SR Latch (NAND or NOR)
- Recall the truth table SR Latch (Using NAND version in this discussion)
- $S^* = \overline{(S \cdot clk)} = \overline{S} + \overline{clk}$
- $R^* = \overline{(R \cdot clk)} = \overline{R} + \overline{clk}$
- 
