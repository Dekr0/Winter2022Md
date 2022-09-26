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
- If "$h(s) \leq h^*(s)$ for all states s" is satisfied, 
  - then heursitic is **admissble**
- The admissibility condition for optimal solutions is **sufficient**
  - but **not necessary**
  - example, $A*$ might still find optimal solutions even if using a inadmissble heurstic ($\neq non-perfect$)
---
#### Proof of Admissibility Property
---
- Consider the following general scenario
- $s \rightarrow$ inital state
- $m \rightarrow$ goal state
- The path at the top, $s$ to $m$, is **suboptimal** and has the cost of $P$.
- The paht at the bottom, going through $n$, is **optimal**.
- Define $g^*(n)$
  - cost of the optimal path between $s$ and a state $n$.
- Since the optimal path between $s$ and $m$ goes through $n$,
  - cost between $s$ and $n$ must also be optimal
  - $\rightarrow g^*(n)$
- Suppose that at a given iteration $A^*$ has both
  - $n$ with the $f$-value of $g^*(n) + h(n)$
  - and $m$ with the $f$-value of $P$ in `OPEN`
- $A^*$ retrieves the optimal path only if $n$ is expanded before $m$.
  - i.e. $g^*(n) + h(n) < P$
  - further $h(n) < P-g^*(n)$
    - This depends on the value of $P \rightarrow$ not helpful
- Recall a fact, the path going through $n$ is **optimal**
- Let's replace $h(n)$ with $h^*(n)$ to obtain a meaningful property 
  - since the admissibility condition includes this term
  - and this can help to further lead to conclusion of the proof
- Then $g^*(n) + h^*(n) < P$
  - then, $h*(n) < P - g^*(n)$
- If $h(n) 