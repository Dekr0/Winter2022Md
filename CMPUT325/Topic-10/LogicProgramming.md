# Logic Programming (LP)

## Horn Clause LP

------

- A **Horn clause** is a logical formula of a particular rule-like form which gives it useful properties.
- A **Horn clause** is a **clause** (a **disjunction** of **literals**) with at most one positive (unnegated), literal

------

## Constraint Programming

------

- Specific constraints along with other things that are not sequential step / procedures.
- Let the program find a solution based on constraints and information. Procedure of how program find such a solution is irrelevance.
- The procedure of a program finding such a solution involve different degree of backtracking if a solution does not satisfy the constraints.
- Naïve solution / algorithm (worst cases) : enumerate all possible solution 
- Improved solution / algorithm, for example: 4-Queens problem, there are some common placement we're already seen in such a question that guarantee that it does (does not) give a correct solution
  - Earlier failure technique, search in specific ways that fail earlier such that the program doesn't get trap a long process of searching.

------

## Answer Set Programming (ASP)

------

- Solve a problem declaratively without providing sequential procedure.
  - Write a program, and let this program to run on a solver
- Similar to constraint programming.
- Not completely based on classical logic, there are default logic embedded.
- Classical logic, more premises we have, more entailed our conclusions are. However, real world doesn't always behave such a way.
  - More premises (information) we have, less entailed / more uncertainty our conclusions are IRL. 
- Default logic capture the concept of common sense and assumption of which when a normal person encounter a problem.