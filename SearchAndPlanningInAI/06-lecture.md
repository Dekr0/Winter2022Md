## Itenative Depending A*
---
### Overview
---
- IDDFS uses the bound to estimate the optimal solution cost.
  - i.e. $B = 0, 1, 2, ..., C^*$
- Initialize $B$ with the h-value of the start
- Prune nodes whose $f$-cost $\gt B$.
- Increase $B$ by the cheapst $f$-value pruned in the previous iteration.
---
### Properties
---
- Optimal if $h$ is admissible (sufficient but not necessary)
- Complete
- Memory Complexity: $O(d)$
- Time Complexity: ? due to the use of herustic function