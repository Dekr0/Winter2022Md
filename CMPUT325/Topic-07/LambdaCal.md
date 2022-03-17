# Lambda Calculus

- In lambda calculus, there are no primitive functions
- Primitive functions can be defined by language itself
- Lambda Calculus is language where we define function without giving a function name, *lambda Function*
- Lambda Calculus can be a *Turning Machine*

## Lambda Function in Lisp

------

- First step: get rid of named functions
- In pure functional programming, any computation is just some (possibly complex,nested) process of function applications
  - `defun` and `function name` is not part of the functional programming
- `(lambda (x1 ... xn) body)`
  - `lambda` is a built-in Lisp keyword
  - `(x1 ... xn)` is the list of arguments, same as with
    named functions
  - `body`  is the function definition (what the lambda function
    does)
- Example : `(lambda (x y) (+ x y))`
- Compare with named function : `(defun plus (x y) (+ x y))`

------

### Lambda Function Application

------

- ***Important***: A lambda function is not an application
- To apply a lambda function, need to provide actual values for the arguments:
  - `((lambda (x1 ... xn) body) a1 ... an)`, valid function application
  - `x1 ... xn` are the arguments of the function, used in the body
  - `a1 ... an` are the actual parameters
- Example `((lambda (x y) (+ x y)) 2 3)`

- Compare with named function application : `(plus 2 3)`

------

#### Examples of Applying Lambda

------

```lisp
((lambda (x y) (+ (* x x) y)) 4 6)
;22

(mapcar ’(lambda (x) (+ x 1)) ’(1 2 3 4 5))
;debugger invoked on a TYPE-ERROR:
;The value (LAMBDA (X) (+ X 1)) is not of type (OR FUNCTION SYMBOL).

(mapcar (function (lambda (x) (+ x 1))) ’(1 2 3 4 (2 3 4 5 6)
```

- Using the function function helps Lisp to understand that this is a lambda function definition

------

### The Function `function` in Lisp

------

- `function` is a built-in function that :

  - takes a lambda function as its argument
  - returns its definition a form used by the Lisp system

  

- In sbcl, `(function arg)` compiles the lambda function given by `arg` and returns an internal representation, ***a closure***, of the compiled code

  ```lisp
  (function (lambda (x) (+ x 1)))
  ```
  
- `function` return  `#<FUNCTION (LAMBDA (X)) {11EAF6E5}>`

  - Information about the lambda function : 
    - parameter of the lambda function,  `(X)`
    - body of the lambda function `{11EAF6E5}`
  - Context. It is needed if there is a global variable in the expression, the context tell what is the value of global variable
    - let say `(+ x y)` instead `(+ x  1)` in above the code block
    - `y` is defined outside function or outside lambda expression (nested expression)

- How to implement a ***closure*** for the case of an interpreter

- Question : why Lisp needs the `function` keyword. Why can't it see that this is a lambda function definition?

------

### `function` vs `funcall` and `apply`

------

- `function` takes as argument a *function* definition and returns an internal representation of that definition. But it does not apply the function.
- `funcall` and `apply` are for *function application*

```lisp
(funcall (function (lambda (x y) (+ (* x x) y))) 4 6)
;22
(apply (function (lambda (x) (+ x 1))) ’(3))
;4
```

------

## The syntax of Lambda Calculus

------

- Formal language with only four concepts:

```
[function] := (lambda (x) [expression])
[application] := ([expression] [expression])
[expression] := [identifiers]
| [application]
| [function]
[identifiers] := a | b | ...
```

- `expression` can be
  -  a `[identifiers]`
  -  a `[application]`
  -  a `[function]`
- `identifiers` corresponds to atoms in Fun or Lisp
- `functions` defines a lambda function
- `application` is a function application. Both function and argument can be any expressions
- `expression` corresponds to s-expression in Lisp.

------

### More Comment

------

- All valid expressions defined by this language are called **lambda expressions**
- The definition is recursive: an application consists of two expressions,
  each of which can again be an application, ...
- Lambda expressions can be nested
- We will see that lambda expressions can represent any computation (!)

------

### Embedded Lambda Calculus in Python

------

```python
def myfunc (n):
	return lambda a: a * n
```

- `myfunc` is a higher function
  - It return a function `lambda a: a * n`, `n` is the argument of `myfun`

- `mydoubler = myfunc(2)`

------

#### Underlying design of lambda calculus in Python

------

- `lambda a : a * n` = `(lambda (a) (* a n))`
- `(lambda (a) (* a n))` is the body of function

```python
def myfunc (n):
	return lambda a: a * n
	
"""
( lambda (n)
	( lambda (a)
		(* a n)
	)
) = myfunc

( lambda (n)
	( lambda (a)
		(* a n)
	)
  2
) => ( lambda (a) (* a 2) )
"""
```

-  ***Function reduction / evaluation***, replace function with its body  (equal to equal) (check Fun Language)



