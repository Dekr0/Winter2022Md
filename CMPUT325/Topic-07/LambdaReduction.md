# Lambda Reduction

- Goal :  reduce lambda expression to its simplest possible form.
- It is called “operational semantics” of lambda calculus.
- In lambda calculus, computation is the process of reductions from one expression to another expression.

#### Comment on Built-in Function

------

- In lambda calculus it does not need any built-in, or primitive functions such as +, -, *, null, eq and more.
- All these functions can be defined in pure lambda calculus.
  - can even represent numbers such as 0,1,2,3,... by lambda expressions

------

## Beta-Reduction

------

- $\rightarrow^\beta$ to indicate such a reduction
- Rule : given an expression `( ( lambda (x) body ) a )`, an application
- Reduce it to body (the expression in the body is the result of the expression), but :
- Replace all occurrences of `x` in body by `a`
- Example : `( ( lambda (x) ( x (x 1) ) ) 5 )`
  - body of `( lambda (x) ... )` is `( x (x 1) )`
  - replace `x` with argument `5`
  - $\rightarrow^\beta$ `( 5 ( 5 1 ) )`

------

### Comment

------

- The expression being reduced could be a **sub-expression nested** within some complex expression
- Complications may arise when replacing, due to name conflicts
- Sometimes, the result after a reduction is actually **more complex than before**
  - Imagine a function body where x occurs many times, and gets substituted by some complex expression each time
  - The term of simple form does not means actual simple
- How to implement primitive in lambda calculus ?
- How recursion is performed in lambda calculus if there is no naming ?

------

#### Example

------

- `( (lambda (x) (x 2) ) (lambda (z) (+ z 1) ) )`
- The body is `(x 2)`
- The `x` gets replaced by the argument given `(lambda (z) (+ z 1) )`
- The result of this beta-reduction is `((lambda (z) (+ z 1) ) 2)`
  - The body is `(+ z 1)`
  - `(+ 2 1)`
  - this can continue if pure lambda calculus definition of `+`

------

## Alpha-Reduction

------

-  means renaming variables

- changing the name of local variables in a function does not change the meaning

- Lisp example : all three are the same:

  ```lisp
  (defun f (x y) (- x y))
  (defun f (y z) (- y z))
  (defun f (y x) (- y x))
  ```

- However, it should not produce a “name conflict”:

  -  `(defun f (x x) (- x x))`

- A ***bound variable*** can be **replaced** by another if the latter doesn’t cause any name conflict
- It is always safe if you use **a new name**, that **does not occur anywhere else** in the **whole lambda expression**
- Example: `(lambda (x) (+ x y))`
- `x` is **bound** in the scope of `(lambda (x) ...)`
- `y` is **free**
- `x` can be renamed to anything, except `y` (name conflict)
- `y` cannot be rename because it would change the result
  - y is not **bound**
  - a **free** variable cannot be renamed

------

### Free vs Bound Variables

------

- Free and bound are **not absolute concepts**, they **depend on the scope**.
- Example `(lambda (z) (lambda (x) (+ x z)))`
- `z` is free in the scope of `(lambda (x) (+ x z))`
- `z` is bound in the scope of `(lambda (z) ...)`
- When looking for where a variable is defined, you **never** look **inner** (block) definition. You look for the **outer** (block) definition and the definition is the first occurrence.

------

### When Direct Substitution Goes Wrong

------

- Blindly do beta-reduction can lead to name conflict 
- `( ( lambda (x) ( lambda (z) (x z) ) ) z)`
- This lambda expression applies :
  - A function of x,
  - with body `(lambda (z) (x z) )`
  - to the argument `z`
- Replace `x` by `z` in body gives : `(lambda (z) (z z) )`
  - The former **free** (within scope) `x` got changed into `z`, but in this scope `z` is bound variable
- There is a name conflict btw
  - the z **bound** in `(lambda (z) (x z) )`
  - the **free** argument `z` in `((lambda (x) ...) z)`

------

#### Example of Alpha-reduction

------

- `( ( lambda (x) ( lambda (z) (x z) ) ) z)`
- Do alpha-reduction first
- Which `z` can we rename ? Only the one in `( lambda (z) ... )` since it is **bound** in the scope of `( lambda (z) ... )`
- Rename that `z` to `u` in the whole scope of this function :
  - `( ( lambda (x) ( lambda (u) (x u) ) ) z)`
- Now, the **bound variable** is called `u` and will not conflict with the argument `z`. With beta-reduction it now get the answer
  - `( lambda (u) (z u) )`
- Difference with and without alpha reduction
  - `(lambda (z) (z z))`
  - `(lambda (u) (z u))`
- Apply them to the same argument
  - `((lambda (z) (z z)) a)` $\rightarrow^\beta$ `(a a)`
  - `((lambda (z) (z u)) a)` $\rightarrow^\beta$ `(z a)`

------

## Summary

------

- Correct beta reductions can always can be achieved by
  - renaming ($\alpha$-reduction), if needed
  - followed by a beta-reduction using direct substitution

------

## Normal Form

------

- A lambda expression that **cannot be reduce** further (by beta-reduction) is called a ***normal form***
- If a lambda expression `E` can be reduced to a normal form, then say that E has a ***normal form***
- In general, a lambda expression **may not** have a ***normal form***

------

### Lambda Expression without a Normal Form

------

- `( (lambda (x) (x x) ) (lambda (z) (z z) ) )`
  - Body `(x x)`
  - Given argument `(lambda (z) (z z) )`
  - $\beta$-reduction : Substitute given arg. for `x` in body :
  - `((lambda (z) (z z)) (lambda (z) (z z))))`
  - α-reduction: rename first `z` to `x`
  - `( (lambda (x) (x x) ) (lambda (z) (z z) ) )`
  - Again ...
- This is **one step of reduction** (plus **renaming**) has led to an identical lambda expression
- This can be reduced this again and again, infinitely often
- This can **never reach** a ***normal form*** that can no longer be reduced
- This proves that not all lambda expressions have a ***normal form***
- There are other examples, where the expression just grows and grows with each "reduction"