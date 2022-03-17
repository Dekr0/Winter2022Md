# Order of Reduction

- How to reduce nested function application ? What order should follow ?
- Two Important Orders of Reduction
  - Normal Order Reduction (NOR)
  - Applicative Order Reduction (AOR)

------

## Normal Order Reduction (NOR)

------

- evaluate leftmost **outermost** application

------

#### Example

------

- Function application `f(g(2))`
  - With `f(x) = x + x`
  - `g(x) = x + 1`
- `f( g(2) )` $\rightarrow$ `g(2)` + `g(2)` $\rightarrow$ `3 + g(2)` $\rightarrow$ `3 + 3` $\rightarrow$ `6`
- Actually, the outermost function is the `+`.  But if the built-in + requires evaluated arguments, then we need to evaluate them first

------

## Applicative Order Reduction (AOR)

------

- evaluate leftmost **innermost** application

------

#### Example

------

- Function application `f( g(2) )`
  - With `f(x) = x + x`
  - `g(x) = x + 1`
- `f( g(2) )` $\rightarrow$ `f(3)` $\rightarrow$ `3 + 3` $\rightarrow$ 6 

------

## Efficiency

------

- In NOR, `g(2)` is evaluated twice
- In AOR, only once
- AOR is generally more efficient
- However, NOR terminates more often...

------

### An Example where NOR Terminates and AOR Does Not

------

- `g(x) = cons( x, g( x + 1 ) )` infinite nested call, trouble ...
- `f(x) = 5` a constant function
- Reduce `f(g(0) )`
- NOR : `f(g(0) )` $\rightarrow$ 5
- AOR : `f(g(0) )` $\rightarrow$ `f( cons( 0, g(1) ) )` $\rightarrow$ `f( cons(0, cons(1, g(2) ) ) )` $\rightarrow$ ...

------

## Church Rosser Theorem

------

- The existence of expression D such that $B\to D$ and $C\to D$ is independence from termination of $A\to B$ and $A\to C$.

  