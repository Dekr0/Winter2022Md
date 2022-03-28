# Recursion in Prolog

- Predicates can be defined recursively.
- Roughly speaking, a predicate is recursively defined if one or more rules in its definition **refers to itself**.

------

## Declarative

------

- About the logical meaning of Prolog knowledge bases

- The **declarative** meaning of a Prolog knowledge base is simply "what it says", or "what it means, if we read it as collection of logical statements".

- ```
  is_digesting(X,Y)  :-  just_ate(X,Y). %1
  is_digesting(X,Y)  :- %2
                     just_ate(X,Z),
                     is_digesting(Z,Y).
  ```

  - Declarative meaning : 
    - First clause : If X has just eaten Y, then X is now digesting Y
    - Second clause : If X has just eaten Z and Z is digesting Y, then X is digesting Z.

------

## Hint for Writting Recursion

------

- Base cases first. They are usually facts.

------

### Recursive Case

------

- The same rule should have have multiple definitions to act as `if ... else`

- The way to distinguish when a rule with same name but multiple definitions

  - accept same number of arguments but in different forms
  - accept different number of arguments
  - body for each definition is difference

- Try to think about writing a predicate that proofs a head of rule and its **output** is **true** 

  - instead of computing the output along the fly
  - because Prolog search for answer based on a query instead of computing the answer

- Procedure in Prolog is backtracking.

  - This mean procedures actually occur when return from base case

  - This mean data processing can happen each time a recursive call return

  - The returning result should reflect / assign on one of the argument in a predicate

  - ```
    incre([], E1, [[E1, 1]]).
    
    incre([[E1, C1]|R1], E1, [[E1, C2]|R1]) :- 
        C2 is C1 + 1.
    
    incre([[E, C]|R1], M, [[E, C]|R2]) :-
        E1 \== M, 
        incre(R1, M, R2).
    
    countAll([], []).
    countAll([F|L], N) :- 
        countAll(L, R),
        incre(R, F, N).
    
    ```

    - Searching a answer for N
    - The result of N is instantiated when recursion reaches the base case.
      - Notice that base case is first assigned to R
      - Base case requires some processing before assign to N
    - `incre` can process N when returning each recursion

- Try not think arguments as inputs of a predicate

  - They can be treated as both input and output.
