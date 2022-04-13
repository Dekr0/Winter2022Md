# Constraint Logic Programming (CLP)



- ***Unification*** in Prolog is about solving constraints over equations in the sense of ***pattern matching***.
  - solve not only constraints over equations but constraints over other domains.

------

## Constraint Store

------

- There is a conjunction of equations and inequalities to solve.
- They can be pull in a ***constraint store***
  - a collection of some primitive constraints (for example, X > 1).
- Any non-user defined predicates will be decomposed into primitive constraints which are sent to the ***constraint store***.
- Every time a constraint store is modified, Prolog will check.
- If Prolog can determine that it cannot be solved then stop right away,
  - then backtracks.

------

## Solving CSPs using CLP (FD) solver

------

- Recall a ***CSP*** is described by three components:
  - variables,
  - domain of each variable,
  - constraints.
- Structure using CLP(FD):
  - Load the library `clpfd`,
  - Specify constraints (prefixed `#`)
  - Optionally, declare ranges of values for the variables
  - tell Prolog to use *labeling*: a systematic search over the remaining possible values for the variables, until
    - a solution that satisfies all constraints is found,
    - or until it is proven that no solution exists.
- 
