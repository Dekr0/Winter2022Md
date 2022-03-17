# Lambda Primitive

## Natural Numbers

------

- If $f$ and $x$ are lambda terms, and $n\geq0$ a natural number, write $f^nx$ for the term $f(f(...(fx)...))$, where $f$ occurs $n$ times.
- For each natural number $n$, define a lambda term $\bar{n}$, called $n$ *th Church numeral*, as $\bar{n}=\lambda fx.f^nx$.

------

### Successor Function

------

- **succ** = $\lambda nfx.f(nfx)$.
  - $n$ is the $n$ *th Church numeral* 
  - $f$ and $x$ are the arguments of binary function to represent the *Church numeral*
- **SUC** = `(Lxsz | s(xsz))`
  - `x` is the *Church numeral*
  - `s` is a lambda term used along with `x` to represent *Church numeral* in a binary function 
  - `z` replacement variable of `x` so the successor of `x` (`x` + 1) is represent using `z` instead `x`

------

### Add

------

- **ADD** = `(Lwzsx | ws(zsx)`
  - `w` and `z` are two *Church numeral* needed to add
  - `s` and `x` are lambda terms for representation Church numeral