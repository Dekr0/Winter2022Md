## Uniformed Search Algorithms
---
- Study Breadth-First Search (BFS) and Dijkstra's algorithm
- The entire state space $S$ might not be stored in memory.
- Instead of storing entire state space $S$, start with the following elements
  - start and goal states,
  - a transition function,
  - and a cost function.
- The initial state and the transition function can perform the search without necessary storing all the state space in memory.
  - i.e., state space expands during the runtime by each individual state and a provided transition function
  - begin the search in the start state
  - the transition function can return its neighbors, and the neighbors' neighbors
  - until a goal state is found and returned.
- Things to keep in mind when studying algorithms:
  - completeness
    - it is guarantted to find a solution if one exists 
  - optimality
    - it is guarantted to find an optimal solution
  - time and memory complexities
---
## Breadth-First Search
---
### Algorithm's Overview
---
- It expands all nodes $X$ edges away from the start ebfore expanding nodes $X+1$ edges away the start.
  - i.e., it expands in term of levels (layers) of the search tree.
  - e.g., level 0 $\rightarrow$ start state, level 1 $\rightarrow$ the children of start, etc.
- It enumerates all possible states, level (layer) by level (layer), until a goal state is encountered.
---
### Data Structures
---
- `OPEN`
  - FIFO structure
    -i.e., first node that is stored first in the structure will be expanded first
  - guarantees that the nodes at level $X$ are expanded before BFS expands nodes at level $X+1$.
- `CLOSED`
  - hash table
  - avoid expanding transposition and cycles
    - i.e., stores all states encountered in search
    - BFS will not add it to `OPEN` if it encounters a repeated state.
  - recover the solution path via pointers (references), once one is encountered
    - i.e., store each node $n$ in `CLOSED` and information of $n$'s parent in the BFS search tree.
    - with pointers (references), it can follow these all the way back to the root of the tree to recover the solution path
---
### Algorithm's Procedure
---
- `OPEN` stores all states encountered in search but that were not expanded
- `CLOSED` stores all states encountered in search.
- `OPEN` and `CLOSED` are initalized with the start state.
- BFS then removes it from `OPEN` and adds its children to both `OPEN` and `CLOSED`
- For every iteration
  - a state from the level, which is currently being expanded, is removed from `OPEN`
---
### Pseduo code
---
```python
def BFS(s_0, s_g, T):
  OPEN.append(s_0)
  CLOSED.add(s_0)
  while not OPEN.empty():
    n = OPEN.pop() # pop a node / state n
    for _n in T(n): # _n is n'
      if _n == s_g:
        return path() # path() will return path between s_0 and n', implementation specific
      if _n not in CLOSED:
        OPEN.append(_n)
        CLOSED.add(_n)
```
---
### Properties
---
- Complete because it checks all states encountered
- Optimal iff solution cost is minimal, i.e., all actions have the cost of 1
- Time Complexity:
  - Assume branching factor is constant, i.e., the number of children is constant for all nodes
    - denoted as $b$
  - $d \rightarrow$ depth of the serach tree, i.e., number of levels (layers) of a search tree
  - BFS generates $b$ nodes at level 1, $b^2$ at level 2, ...
  - Total number of nodes generated: $b + b^2 + b^3 + ... + b^d = O(b^d)$
- Memory Complexity: $O(b^d)$
---
### Drawback
---
- BFS minimizes the amount of edges it travel / hop but fails to find optimal solutions in general.
- Action costs often aren't unitary.
---
## Dijkstra's Algorithm
---
### Algorithm's Overview
---
### Data Structures
---
- `OPEN`
  - priority queue
    - implementation of a priority queue: heap (particularly binary heap)
- `CLOSED`
  -  same data strcutures used in BFS
---
### Algorithm's Description
---
- In each iteration, `OPEN` expands the node with **cheapest cost** that was generated but not yet expanded.
- Denote the cost of a paath connecting the root of the tree to node $n$ as the $g$-value of $n$, or $g(n)$.
- When encounter a better path to goal state, update the information about the parent of a state in `CLOSED`
- The algorithm only stops when the goal node, $h$, is removed from `OPEN`.
- Then, recover the path from the root to a goal state using `CLOSED` list in the same way as BFS.
---
### Differences between Dijkstra's algorithm and BFS
---
- BFS uses a FIFO. 
- BFS stops the search when the goal is **generated**.
- BFS always finds the shortest path (in terms of number of actions) to every node when it is first **generated**.
- Dijkstra's algorithm uses a priority queue sorted by the node cost
- Dijkstra's algorithm stops when the goal is **expanded**.
- Dijkstra's algorithm might need to update the path and the cost of nodes in `OPEN`
---
### Properties
---
- Complete
- Optimal $\leftarrow$ expands all cheapest paths before moving on more expensive ones
- Time complexity
- 
---
- Find smallest length to smallest cost
- Expand cheapest node in `open`
  - Implementation $\rightarrow$ Priority Queue (Heap)
- Implementation difference compared to BFS
  - Stop when goal comes out of `open`
  - Update cost to nodes if a better path is found (also for parent pointers)
  - FIFO $\rightarrow$ PQ
- Implementation
  1. find and remove cheapest node form `open`
    - Heap (Binary Heap)
      - Find: $O(1)$
      - Remove: $O(\log{n})$
      - Insert $O(\log{n})$
      - must be careful with the state of the heap when updating cost
      - re-heapify is expensive ($O(n)$) but happen rarely
    - paying linear complexity for finding cheapst cost node if using simple list
  2. Verify if a state was seen before in search (Hashmap / Hashtable) as well as check whether a better path is found (instead of scan through the open list)
    - $O(1)$ 
- Both open list and closed list share the same pointer / reference of all nodes 