# Inference Engine in Prolog

- Recall that a rule in Prolog is `if ... then ...` statement
- Recall `if p1 and p2 and ... and pn then q1 can be written as
  -  `not (p1 and p2 and ... pn) or q` 
  - that means the atoms inside a rule are negation.

------

## Tree Search (Depth First Search)

------

- Go into the leftmost path in a tree search
- Recall 

------

## Make Use Inference Engine

------

- Manually create a predicate that allow Prolog to backtrack and find an alternative path
  - This allows `findall` to search for all possible results
- Use DFS in inference engine to construct the logic of a predicate
- Make use of  the ability of a inference engine can find solutions for different arguments, and use those arguments in the body of predicate.
  - `append(L1, [q|L2], [a, b, q, r, q, a, b, c])`

