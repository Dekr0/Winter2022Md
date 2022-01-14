## Lecture 02
---
##### 2022-1-11
---
### Recursion (Induction)
---
- Do not trace through the recursion initally
  - examples approach : bottom to top and top to bottom

- Two essential parts : *base case* and *reductive case*

- *Base case* - terminate condition

- *Reductive case* - subproblem
  - case / problem need to be reduced in some way from larger problem
  - Assume the reductive case / subproblem always give back the right answer by **Induction**
  - Find a way to use the result from reductive case / subproblem

- At this stage, trace through the recursion to check it whether it is work
---
### Implementation of some functions using recursion
---
Append two lists
```lisp
append (L1, L2) =
    if null(L1)
        then L2
    else
        cons( f(L1), append( r(L1), L2) )
```

Get last item
```lisp
get-last( (1 2 3) ) => 3

get-last (L) = 
    if null(r(L))
        then f(L)
    else
        get-last(r(L))
```

Remove last item
```lisp
rm-last(L) = 
    if null(r(L))
        then ()
    else
        cons( f(L), rm-last(r(L)) )
```

Reverse a list
```lisp
rev(L) = 
    if null(L)
        then L
    else
        append( rev(L), cons(f(L), ()) )    
```

- To put two lists together, two arguments need to be a list

- Recursive call should always input smaller list and output smaller list

- Common way to reduce the list : r or rest (cdr in LISP)

- Do recursion over one list instead of mutiple lists. If a recursion involve handling mutiple lists, decompose  the problem into smaller problems.
---
### Introduction to LISP
---
- For every (...), LISP intereperts as a function call
  - ( null (1 2) ), (1 2) is also considered as another function call where the function name is " 1 ".
  - To let a list or (...) inside a function call be argument, use quote or " ' " to tell LISP not to evaluate it / treat as a function call.
---