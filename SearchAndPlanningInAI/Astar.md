## Heuristic Search
---
### Comment about uninformed algorithms
---
- **uninformed** $\rightarrow$ do not use the info. of the goal state (conditions) to guide the search to a solution path.
- can be inefficient
---
#### Example - Dijkstra
--- 
- Dijkstra expands states equally in all directions from the inital state.
  - form a circle aorund the inital state that grows as the Dijkstra expands more states
- **wasteful** as the algorithm explores states that might be **far from** the goal
---
### Heuristic Function
---
- Provide estimate distance from a state, s, to goal - $h(s)$ 
  - No need to be perfect
  - Might speed up the search
    - Often inaccurate heuristic fucntions are able to dramatically reduce search time
    - Example, a heuristic function ignoring all obstacles on the map
---
#### Example - Manhattan Distance
---
- The sum of the absolute difference between the two coordinates in the $x$ and $y$ coordinates of the map.
  - i.e. $|x_2 - x_1| + |y_2 - y_1|$
---
### $A^*$
---
- Using two values to guide the search
  - $g(s)$, cost from the **start** to state $s$
  - $h(s)$, estimated **cost-to-go** from $s$ to the **goal**
- $f(s)=g(s)+h(s)$
  - provides an **estimate** for the cost of a solution that goes through $s$
- Sorts the nodes in `OPEN` by their $f$-value
  - The state with the **smallest** $f$-value will be exapnded
- Complete
  - inserts into `OPEN` all states generated in searcha, 
  - thus trying all paths encountered in search
---
#### Example (Lecture note)
---
- Notice that $A^*$ focuses its search in the direction of the goal
  - due to the heuristic fucntion
- Unlike Dijkstra which treats eqaully the states aboevr and below $s_0$ as they both have the $g$-value of 1.
- With non-perfect heuristic function, $A^*$ is still able to using heuristic to find a solution (obstacale example)
  - $A^*$ is focusing its search downwards and does not expand states at the top corners of the map
---
### Admissibility of Heuristic Functions
---
- $h(s) \leq h^*(s)$ for all states s.
  - i.e., heuristic function never overestimates the optimal solution cost
  - $h^*(s)$ is the optimal solution cost of state $s$
- If "$h(s) \leq h^*(s)$ for all states s is satisfied, 
  - then heursitic is **admissble**
- The admissibility condition for optimal solutions is **sufficient**
  - but **not necessary**
  - example, $A*$ might still find optimal solutions even if using a inadmissble heurstic ($\neq non-perfect$)
---
#### Proof of Admissibility Property (PDF)
---