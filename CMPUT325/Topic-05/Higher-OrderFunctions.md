# Higher-Order Functions

- Often used to separate a computation pattern from the specific action
- Some typical higher order functions
  - Mapping
    - Example, iterate over a list, and "do something" with each list element
  - Reduced
    - Example, reduce a list to a single result by repeatedly applying the same computation
  - Filter
  - Vector

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
  - `id` return is the based case value for function `g`
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

- Lisp built-in `reduce` works this way by default

- Example

  - `(reduce ’* ’( 2 6 4))`
  - `(reduce ’append ’((a b) (c) (d e)))`

- Define your own version `myreduce` that takes two arguments

------

## MapReduce for Big Data

------

- Imagine huge amounts of data spread over many disks (or distributed memory)
  - Examples: transaction records, web pages, image databases
- Imagine a statistical query on all that data
  - Examples: find all overdrawn accounts, find all webpages containing the word “Lisp”, find all images of cats
- Map: apply the same operation to each data item
- Reduce: compute summary statistics, or sort and present the top 10 pages, ..
- Several large scale implementations exist, e.g. in MPI, or Hadoop
- Provides an easy API for using large clusters
- The aim is to hide the complexity of the distributed computing support
- Performance can be worse than specialized database technology
- Good for quick, “one shot” tasks

------

## Filter

------

- Goal: Select all elements from a list which satisfy a given test predicate
- In Fun

```
filter (Pre, L) = 
	if null(L) then nil
	else if Pre( car(L) ) then
		cons ( car(L), filter( Pre, cdr(L) ) )
    else
    	filter(Pre, cdr(L))
```

- Example : think of internet search as applying a filter to a list of all web pages

------

## Vector

------

- Apply a list F of functions to an object x and get the list of all results of the applications.

```
vector (F, x) = if null(F) then nil
				else cons(car(F) (x), vector(cdr(F), x))
```

------

## Defining new Higher Order Functions in Lisp

------

- Use case: a common computation pattern, where the details (e.g. function to apply to each element in a list) can vary.
- In terms of software engineering, this means removing code duplication.
- In most languages, it is clear what is a function call, and what is not
- In Lisp, no such “syntax barrier” between code and data
  - Not easy for Lisp to figure out which s-expr is really a function call within a higher order function
  - Lisp built-in functions `apply` and `funcall` tell Lisp that a function application is meant.

------

## `apply` and `funcall`

------

- Using `apply` and `funcall` tells Lisp that there is a function to be called
- These two built-in functions have the same functionality but differ in syntax
- In practice, choose whichever one is more convenient

```lisp
(apply function_name (arg1 ... argn))
(funcall function_name arg1 ... argn)
```

