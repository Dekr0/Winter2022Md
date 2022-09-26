## Comment on BFS, Dijkstra, DFS, Bi-BS
---
- They are performing uninformed search
  - The direction of the search for these algorithms will consider all directions equally instead of applying intuition and inference as human does
---
## Heuristic Function
---
- Assumption
  - Remove walls from the map to relax the problem for the sake of study
- Apply **Manhattan Distnace** for Heuristic Function
- Defition of $h$-function : function $h$ that receives a state and returns an estimate of the cost to go.
---
### Quiz
---
- What should be done with $g$-value and $h$-value?
- $f(n)=g(n)+h(n)$
  - **Estimate cost of a solution going through $n$**
  - $g^*(n)$: optimal cost between $s_0$ and $n$.
  - $h^*(n)$: optimal cost between $n$ and $s_g$.
  - $f^*(n)$: optimal cost of a solution that goes throughb n.
---
## $A^*$ Algorithm
---
- Similar to Dijkstra's Algorithm but sort the nodes in `OPEN` by their 
- If there's barrier in between the estimated path between the start and goal
  - treat the barrier is not there and compute values directly
  - treat the barrier later once hitting the wall and turn around
  - After each a barrier is placed, it push the search direction away the goal / desired direction
---
### Properties
---
- Complete
- Optimal but require some specific condition
  - sufficient but not necessary condition : for all $h(n)$ in the graph, $h(n) \leq h^*(n)$ 