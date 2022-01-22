# Accumulating Parameters
## Example 1

------

- Reversing a list 
- `x` is the given list and `y` holds the **intermediate** and **final** reversed list
  - assign `null` to `y` initially
  - `y` collect the result one by one in each recursive call and at the end will be the result
  - The procedure is **outside** of the recursive call
- The key is not about what you pass result in the each recursive call to form the final result. 
  - The result is formed by collecting the result **return** from recursive call.
  - The final result is formed (completed) at the first recursive call.

- The key is about find result **formed accumulatively** from **each recursive call**.
  - The final result is formed (completed) at the last recursive call.
  - The final result is then return from last recursive call without any modification (not always the case ?).



```lisp
; (rev '(1 2 3)) => (3 2 1)

(defun rev (x y)
	(if (null x)
        y ; Return the final result
        (rev (cdr x) (cons (car x) y)) 
        ; Accumulate first of x into y
    )    
)

(defun reverse (x)
	(rev x nil)    
)

; Notes y, as the result, is formed accumulatively in 
; each recursive call
; (rev (1 2 3) nil) 
; (rev (2 3) (1)) 
; (rev (3) (2 1)) 
; (rev nil (3 2 1)) 
```

------

## Example 2

------

- This example shows how more than one result may be accumulated
  - multiple accumulators
- Given a list L of integers, generate a pair (A B) where A is the sum of integers in L and B the product

```lisp
(defun smprod(L)
	(sp L 0 1) ; second and third param. are accumulators
)

(defun sp (L S P)
	(if (null L)
    	(cons S (cons P nil))
        (sp (cdr L) (+ (car L) S) (* (car L) P))
    )    
)
```

------

## Example 3

------

- In general, one can always place the selected results, from a given list, to a resulting list by accumulation. 

```lisp
;(select '(3 6 8 4) 4) => (6 8 4)

;Standard definition
(defun select (L N)  
    (if (null L)
         nil
        (if (>= (car L) N)
            (cons (car L) (select (cdr L) N))
            (select (cdr L) N)
        )
    )
)  
```

```lisp
(defun select0 (L N)  
      (xselect L N nil)
)

(defun xselect (L N AC)    ; AC is an accumulator
     (if (null L)
         AC
         (if (>= (car L) N)
             ; Add (car L) in AC if (>= (car L) N)
             (xselect (cdr L) N (cons (car L) AC))
             (xselect (cdr L) N AC)
         )
     )
)
```

- Hint for Assignment 1 Question 6
  -  Whenever reach a website, include the website in the accumulator
  - At the end, return the accumulator

------