## Comparison of BFS and Dijkstra's Algorithm and IDDFS
---
- BFS and Dijkstra's Algorithm do not suffer from transpostions
  - but memory requirement $O(B^d)$
- IDDFS can suffer from transpositions
  - but memory requirement $O(d)$
## Transposition Table
---
- It find something in between BFS and Dijkstra's Algorithm and IDDFS
- It is essentially a **hash table**.
- Limited memory
  - IDDFS does not depend on the hash table to return a path
  - BFS and Dijkstra;s depend on the hash table for correctness
- Employs policies for deciing what to do if running out of memory
  - Some policies
    - stop inserting states
    - ignore onvel states once the table is full
---
### Implementation
---
#### 1
---
```
Before expanding n:
    if n is not in TT
        add n to TT
        expand n
```

- Problem : prunes optimal solution
#### 2 (Fix problem in 1)
---
- Add the $g$-value to the table along with the node
    - we will know if a state needs to re-expanded

```
Before expaning n:
    if (n is not in TT) or (n is in TT and g(n) < TT[n].g):
        add or update to the TT
        exapnd n
```

- Problem : 
  - need to run bounded search again
    - i.e., information is not reused from previous iterations
    - e.g., (C, 2) will be expanded again
  - TT need to be removed in each iteration to prevent the algorithm stopping in some special cases
    - e.g., graph with a single chain of edges and vertices such as $A \rightarrow B \rightarrow C$
---
#### 3 (Fix problem in 2)
---
```
C1: n is not in TT

C2: n is in TT and g(n) < TT[n].g

C3: n is in TT and TT[n].g = g(n) and d > TT[n].d

Before expanding node n:
    if C1 or C2 or C3:
        add / update n
        expand n
```
---
## Bidirectional Search
---
- Search can grow exponentially with $C^*$ 
  - for example, if $b=C^*$ we could have $b^d$ leaf nodes in the search tree
- Instead of $b^d$, it would have $2b^{d/2}$
- Notation
    - start $\rightarrow_{g_F(n)}$ $n$
    - $n'$ $\rightarrow_{g_B(n')}$ Goal
---
### Nicholson's Algorithm
---
- Bidirectional Brute-Force Search (Bi-Bs)
- $f \rightarrow$ forward search, $B \rightarrow$ backward search 
- Insert $s_{init}$ to `OPEN`$_f$ and $s_g$ to `OPEN`$_B$.
- In every iteration : expand the cheapest node in either `OPEN`$_f$ or `OPEN`$_B$.
- Solution Path: every state generated in both directions
  - Not necessaarily optimal
- Use separate `CLOSED` lists: `CLOSED`$_f$ and `CLOSED`$_B$
- When state $n$ is in either `OPEN` or `CLOSED` in both directions and:
  - $g_F(n)+g_B(n) \leq g_{MINF} + g_{MINB}$
  - $g_F(n)+g_B(n)$ is the **solution path** going through $n$
  - $g_{MINF}$ is the cheapest cost in `OPEN`$_f$
  - $g_{MINB}$ is the cheapest cost in `CLOSED`$_B$
    - lower bound on the solutions yet to be disovered
  - Paths increase in cost because actions are continously added into the lsits
    - i.e., $g(n') \geq g(n)$