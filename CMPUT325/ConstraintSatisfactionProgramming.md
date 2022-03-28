# Constraint Programming

- Constraint programming is the study of computational models and systems based on constraints.
- The idea is to model and solve a problem by exploring the **constraints** that can **fully characterize** the problem.
  - Hence any solution of the problem must satisfy all of the stated constraints
- In constraint programming, the programming **process** consists of **specifying constraints** and solving them by a specialized constraint solver.   

------

## Constraint Satisfaction Problem (CSP)

------

- One way to solve a constraint problem
- A CSP consists of three parts:
  1. A set of variables $X = \{x_1,...,x_n\}$
  2. For each variable $x_i$ , a finite set $D_i$ of possible values (its domain)
  3. A *set of constraints* **restricting** the values that variables can take simultaneously.
- Note that values need not be a set of consecutive integers (although they often are), 
  - they need not even be numeric.
- A solution to a CSP is an assignment of a value from its domain to **every variable**,
  - in such a way that every constraint is satisfied.
- i.e. $x_i=d_i$ where $d_i \in D_i$ such that $X=\{d_1,...d_n\}$ satisfies every constraint.  
- We may want to find:
  - just one solution, with no preference as to which one,
  - all solutions,
  - an optimal, or at least a good solution, given some objective function defined in terms of some or all of the variables.

------

## Constraint Solving Methods

------

- A constraint is local but a solution to all constraints is global.
  - Satisfying a single constraint cannot give a solution when other constraints are considered. 

------

### Systematic Search Algorithms

------

- ***Backtracking paradigm (BT)***, one of the most common algorithms for performing a system search.
- ***Backtracking*** incrementally attempts to extend a partial solution toward a complete solution, by repeatedly choosing a value for another variable.
- Whenever a variable is assigned, it's checked against all previous assignments to see whether 
  - the constraints involving these assigned variables are not violated.

------

#### Consistency Techniques

------

- The late detection of inconsistency is a major disadvantage of ***BT***.
  - The program discover that
    - it is not a solution for a CSP with specific value assignment and domains 
    - only when it reach to specific points
- Consistency techniques are applied
  - initially before any variable is assigned,
  - and during the backtrack search,
  - after each variable is assigned.
- The idea is to discover values that are not possible, so they can be safely removed from the assignment so far.
  - they are not removed permanently
  - they will be recovered upon backtracking
- ***[Node consistency](https://en.wikipedia.org/wiki/Local_consistency#:~:text=variables.%5Bclarification%20needed%5D-,Node%20consistency,-%5Bedit%5D)*** only applies to constraints with one unassigned variable.
  - It is used for check which values for a variable that are not possible, and then removed
- ***[Arc consistency](https://en.wikipedia.org/wiki/Local_consistency#:~:text=simplifies%20later%20stages.-,Arc%20consistency,-%5Bedit%5D)*** only applies to a constraint with two unassigned variables, say X and Y.
  - If for a value of X, there is no value of Y such that the constraint is satisfied, 
  - then this value for X can be removed.
  - This is done repeatedly until no domain reduction is possible.