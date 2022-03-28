# Prolog

## Introduction

------

- Unlike other programming language, Prolog inferences and deducts new information using existing data in Prolog program (database).
- Data in Prolog are represented as clauses, more specifically, facts and rules. These clauses provide knowledge and relationship between data. Database in Prolog is also called knowledge database.
- ***Query*** is a logic formula. Using a query is same as asking whether if this logic formula is a logical consequence of a Prolog program.
  - Whether if this logic formula logically follow a Prolog program or,
  - Whether if a Prolog program logically entail / imply this logic formula.
- Prolog inference process is similar to recursive function call with backtracking.
  - It analogs to working through a search tree.
  - It might not terminates.

------

## Sample of Execution

------

- Query: `grandparent(ken, john).` (1)
- Match with head of clause `grandparent(X,Z) :- parent(X,Y), parent(Y,Z)`
- `X = ken` and `Z = john`
- Replace `grandparent(ken, john).` with the body after vars. binding.
- New query: `parent(ken, Y), parent(Y, john).` (2) from query (1)
  - `Y` is still an unbound var (free).
  - Free variables are **existentially quantified**.
    - **Existentially quantified**: do not need to show that the query is true **for all Y**
    - **Existentially (CMPUT 272)**: at least one
  - There exists some Y such that `parent (ken, Y)` and `parent(Y, john)` are both true.
- Match with head of clause `parent(X, Y) :- father(X, Y)`.
- Subquery `father(ken, Y)`
- `father (ken, Y)` matches the fact `father (ken, mary)`
  - set `Y = mary`
- Now `Y = mary` is for query`parent(Y, john)`
  - Perform similar process


------

## Prolog Syntax

------

- In Prolog, everything needs to be expressed in terms of relationship and predicate
- `=<` is less than
- Arithmetic functions aren't predicates.
  - can't query over arithmetic functions
- Everything start with upper case is a variable
- use `is` to use along with arithmetic functions.
  - All variables in `is` predicate are **bounded** to some values.
  - `E is 3 + 5`
- Prolog has it renaming systems.
  - During inferences and deviation, a lot of variables name need to be generated. 
- `A \== a` is always true. `A` can be set to anything that is not `a` This situation should be avoided.
  - Both side should be constant when doing comparison.
- To make a predicate behave as a function, it is better to specific the input terms and output in the predicate.

