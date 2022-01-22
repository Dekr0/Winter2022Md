# Higher-Order Functions

- Often used to separate a computation pattern from the specific action
- Some typical higher order functions
  - Mapping
    - Example, iterate over a list, and "do something" with each list element
  - Reduced
    - Example, reduce a list to a single result by repeatedly applying the same computation
  - Filter
  - Vector
- Whenever seeing a computation process that repeatedly happen as a pattern, try to define a higher order function

------

## Definition

------

- Takes other function(s) as input, and  / or
- Produces function(s) as output

------

## Map

------

- Apply a given function to each element in a list
- Collect all the results in a list

------

### Example

------

- Salary raise
- Input : payroll, and a function implementing the raise
- Output : the new payroll with increased salaries
- Payroll representation
  - List of dotted pairs `(name . salary)`
    - `((John . 23000) (Mary. 50000))`
  - Raise salary by `x` amount
  - In Fun : `inc(E, x) = cons(car(E), cdr(E) + x)`

```
raise(L) = if null(L) then nil
			else cons (inc(car(L)),
						raise(cdr(L)))
```

- Apply mapping instead

```
map(f, L) = if null(L) then nil 
            else cons(f(car(L)),
                     map(f, cdr(L)))
```

- In Common Lisp

```lisp
(defun inc (N)
    (cons (car N) (+ 100 (cdr N)))
)

;(mapcar 'inc '(list of dotted pairs - (name . salary)))
```

------

## Reduce

------

- In a list, repeatedly apply the same function to two arguments, which produces a single argument
- Given a function `g`, its identity `id`, and a list `L = (A1 A2 ... An)`
  - `id` return value of base case
- Computation pattern `(g A1 (g A2 ... (g An id) ... ))`
- Example : sum of a list of numbers, using function `+` and identity `0`
- Example : product of a list of numbers, with function `*` and identity `1`

```
reduce(f, id, L) = 
	if null (L) then id
    else f(car(L)
           reduce(f, id, cdr(L)))
```

------

### Reduce Without Identity

------

- The identity is not needed if we define reduce as

  `(g A1 (g A2 ... (g An-1 An) ... ))`

-  Lisp built-in `reduce` works this way by default

- Example

  - `(reduce ’* ’( 2 6 4))`
  - `(reduce ’append ’((a b) (c) (d e)))`

------

