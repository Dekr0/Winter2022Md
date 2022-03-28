# List and Unification

## List

------

- `[]` is an empty list

- list can be nested

  - `[ [a, 1], [b, 2] ]`

- `[...|...]`
  - LHS of `|` $\to$ first element of the list
  - RHS of `|` $\to$ rest of the list
    - Single `[]` will concatenate with the LHS

------

## Unification

------

- A unification is a two way matching process. (LHS = RHS)
- The concept of substitution $w = \{x_1/t_1,...,x_n/t_n\}$
  - replace each $t_i$ with $x_i$
- The concept of **unifier**

------

### Pattern Matching

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
- **Unification** in a 

------

### Unifcation on List

------

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