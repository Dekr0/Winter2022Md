## Bidirectional $A^*$
---
### Design stage
---
- Directly apply $A^*$ will void the original properties of brute-force bidirectional search due to the use of heuristic function ($f=g+h$)
  - The depth of a search might exceed the $d=\frac{C^*}{2}$
  - The exponential saves is not longer valid
    - i.e. one of the searches might expand majority of the nodes while another might expand little.
- How to fix the issue?
---
### How to meet in the middle?
---
- Assuming a consistent (and admissble) $h$
- Use the cost function:
  - $P(n)=\max (f(n), 2g(n))$
  - $f_F(n)$ is the usual $A^*$ cost function
  - $2g_F(n)$ prevent a search from expanding too far (exceed the middle of the search $\rightarrow$ $d=\frac{C^*}{2}?)
    - Increase $P(n)$ by apply $\max$ allow the algorithm to switch from one direction search to another direction if a search goes too far
    - Reminder: expanding the cheapest from either open list
- "Meet in the Middle" (MM) Algorithm
---
#### Intuition of why MM works
---
- Given the fact that $s_{k+1}$ exceed the middle between start and goal
  - This results in $g_F(s_{k+1}) > \frac{C^*}{2}$
- Key Question: Why isn't $s_{k+1}$ expanded in the forward search?
- Answer: $P_F(s_{k+1})=2g_F(s_{k+1})$, and this prevent forward search expand $s_{k+1}$
  - Use the given fact $g_(s_{k+1}) > \frac{C^*}{2}$
---
### Pseudo Code
---
- Stopping condition:
  - Obtain the maximum of all the possible lower bound and compare with cost of the current search $u$.
---
#### Why are these lower bounds 
---