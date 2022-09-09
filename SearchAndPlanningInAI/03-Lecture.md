## Depth-FIrst Search (Unitary Cost)
---
### Algorithm's Overview
---
- Store a single path in memory
  - i.e., return the next path
- Parent prunning
---
### Design
---
- Two initial problems without opttimization
  - Not complete
  - Not optimal

- Idea 1: Bound the saerch depth with the optimal solution depth
  - optimal solution depth varies by questions
  - problem: what and how to find optimal solution ddepth

- Idea 2: Guess that the optimal solution depth is 0, 1, 2, ... until a goal is found
  - expensive
---
### Data Strctures
---
- `OPEN`
  - LIFO
---
### Pseduo Code
---
```python
def DFS(n, s_g, T, B):
    if n is s_g:
        return True # Find the true

    if B < 0:
        return False

    # Perform DFS on children of node n
    for _n in T(n):
        if DFS(_n, s_g, T, --B): # Whether a child can find a soution
            return True
    
    # No solution under node n since if DFS returns false for every single child of node n 
    return False

def IDDFS(s_init, s_g, T):
    B = 0
    while DFS(s_init, s_g, T, B): # Search within bound
        B += 1
```
---
### Properties
---
- Complete
- Optimal if a question has unitary cost
- Memory complexity $O(n)$
- TIme complexity
  - Assume
    - branching factor is fixed
  - $bd+b^2(d-1)+b^3(d-2)+...+b^d=O(b^d)$
    - $b$, number of childrens in every branch
    - $d$, solution depth
---
## Depth-FIrst Search (Non unitary Cost)
---
### Algorithm's Description
---
- IDDFS - General Case
  - Start $B=0$
  - Set $B$ to the smallest $g$-value of a node prunned in the previous iteration
  - Stop when ***goal is expanded***
- Worst case: If Dijkstra's Algorithm expands $N$ states, IDDFS could expand $O(N^2)$.
---