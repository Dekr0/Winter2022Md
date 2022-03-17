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

------

## List and Unification

------

- Using **unification** to perform pattern matching (LHS = RHS).

  - Example 1: `f(X) = f(a).`
    - set `X` to a
    - `f(a) = f(a).` is **unified**
  - Example 2: `f(g(X), a) = f(Y, Z)`
    - Head of clause in LHS = Head of clause in RHS $\to$ `f` = `f`
    - set `Y` to `g(X)`
      - `f(g(X), ...)` = `f(g(X), ...)`
      - first parameters in LHS and RHS are **unified**
    - Set `Z` to `a`
      - `f(..., a) = f(..., a)`
      - second parameters in LHS and RHS are **unified**
    - `f(g(X), a) = f(g(X), a)` is **unified**
  - Example 3: `f(X, X) = f(a, b)`. 
    - LHS and RHS cannot be **unified**
    - Two parameters in LHS are both `X`. Setting one of them will contradict another.

- **Unification** algorithm is used to solve each pair of arguments. 

  - It is recursive. 
  - An argument can have pairs of arguments.

- `[]` is an empty list

- list can be nested

  - `[ [a, 1], [b, 2] ]`

- `[...|...]`

  - LHS of `|` $\to$ first element of the list
  - RHS of `|` $\to$ rest of the list
    - Single `[]` will concatenate with the LHS

- Using **unification** to perform pattern matching with list (same principle, LHS = RHS)

  - Example 1: `[a, b, c] = [X, b, c]`

    - `X = a`

  - Example 2:  `[a, b, c] = [X|R]`

    - `X = a`
    - `R = [b, c]`

  - Example 3:  `[a|[b]] = [X, R]` ***

    - `X = a`
    - `R = b`

  - Example 4: `[ [a, 1], [b, 2] ] = [ [X, Y] | R]`

    - `[X, Y]` = `[a, 1]`
    - `R` = `[ [b, 2] ]` ***
      - It's not `[b, 2]` because this will become `[ [X, Y], b, 2]`

  - ```Prolog
    member(A, [A|R]). % Base case, A appear in the first element
    member(A, [B|R]) :- A /== B, member(A, [A|R]).
    ```


------

### Unification

------

- A unification is a two way matching process. (LHS = RHS)
- The concept of substitution $w = \{x_1/t_1,...,x_n/t_n\}$
  - replace each $t_i$ with $x_i$
- The concept of **unifier**
