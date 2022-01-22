
# Reucrsion

- Recursion must happen with recursively calling (smaller) subproblems.
  
- Reduce the problem into subproblem in a specific way

- Find a specific to put all the results of subproblem from recursively call together.

- By induction, assume recursive call always **return the right result** if above steps are done **correctly and logically**.
---
## Lisp built-in function and Special Forms
---
Set variable
```lisp
(set 'a 5)
5
* a
5
* (+ a 4)
9
* (set 'a 10)
10
```
Short hand for express sequence of car and cdr (read in the reverse direction)
```lisp
(caddr (1 2 3))
3
```
---