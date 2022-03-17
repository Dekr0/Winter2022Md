# Context and Closure Interpreter

- Delay replacement (substitution) until it needs to evaluate the variables instead of equal to equal directly (no direct substitution until evaluation)
- The value of free (global) variables (are not passed through as arguments) are provided from context

------

## Language 

------

- `eval` : evaluate the s-expression, S in the current context, CT
  - If S is a function, it needs to generate a closure, [S, CT], and evaluate this closure

- Use `let` to pass arguments `e1, e2, e3` into lambda function's parameter `x1, x2, x3`
  - Use dotted notation
  - Do not support recursion

------

## Context

------

- Context is not unique in the entire expression. Different function calls in the expression can have different corresponding contexts.

------

## Closure

------

- Provide all the information to apply a function, `f` to evaluated argument
  - parameter list of the function `f` (can also be used for extension of current context)
  - body of the function `f`
  - current context when this function `f` is applied (can also be used for extension of current context)

------

## Evaluation Process

------

- First, it begins with some context CT0.
  - It can be empty or not if CT0 is during the middle of an evaluation
- Second, evaluate the arguments with context CT0
- Third, evaluate the arguments with functional part with context CT0 (Evaluate Function in the Context)
- Extend the context CT0 to CT1
- Return the result as well as updated context if necessary
- If both function and arguments are functions, 
  - they need to be turned into closure first.
  - after that, it will have a function application
  - evaluate the function application

------

### Function Application in the Context (Evaluate a function in the Context)

------

- Generate a closure `[f, CT]`
- Evaluate `[f, CT]`
  - apply function `f` from closure `[f, CT]` to the evaluated arguments
    - body of the function `f` and parameter names / lists of `f` are from closure `[f, CT]`
  - bind parameter names of `f` to the evaluated arguments
  - add these binding to current context `CT` to form the next context `CT'`
  - evaluate the body of the function `f` in the extended context `CT'`
- Repeat the above steps until there are no more functions call
- Return the result, the result can be :
  - another closure `[g, CT_g]`
  - function application