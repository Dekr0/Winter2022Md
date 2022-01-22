# Deal With Nested Lists

## 	Example  #1

------

- Given a nested list of numbers, computer the sum of all numbers (including the nested one)

```lisp
; First Approach
; (xsum '(1 2 (3 4) (((2)))) => 12

(defun xsum (L)
    (cond
        ; Base case - empty list
        ((null L) 0)
        ; Case 1 - first of L is an atom
        ((atom (car L)) (+ (car L) (xsum (cdr L))))
        ; Case 2 - first of L is an list, find the sum of 
        ; first of L
        (t (+ xsum(car L) xsum(cdr L)))
    )
)
```

```lisp
; Second Approach
; This simplified Case 1 in First Approach 
; Execute xsum(car L) regardless (car L) returns an atom or
; a list because Base case 2 handle it
(defun xsum (L)
    (cond
        ; Base case 1 - empty list
        ((null L) 0)
        
        ; Base case 2 - first of L is an atom
        ; This can also mean first of L is an atom in 
        ; previous call of xsum()
        ((atom L) L)
        
        ; Case 2 - first of L is an list, find the sum of 
        ; first of L
        (t (+ xsum(car L) xsum(cdr L)))
    )
)
```

------

## Example 2

------

- Given a nested list L, replace any atom E by R

```lisp
;(xreplace '(((x p) (x) x q t)) 'x 5)  
; => 
; (((5 p) (5) 5 q t))
(defun xreplace (L E R)
    (cond
     	((null L) nil) ; Base case 1 - L is empty
        ((atom L) (if (eq L E) R L)) ; Base case 2 - L is an atom
        (t (cons (xreplace (car L) E R) 
                 (xreplace (cdr L) E R)))
        ; Reduced Case
     )
)
```

- `xreplace` is useful in the next assignment. 
  - It can replace all the function expressions with the function definitions. 
  - It can replace all the arguments in the function definitions with the actual values.


------

## Example 3

------

- Further to Example 2, apply a substitution to a given (possibly nested) list. (if a function contains multiple arguments)

```lisp
; (sub '((x y) z 5 9 (4 (y))) '((x 1) (y 2) (z 3)))
;       ==> ((1 2) 3 5 9 (4 (2)))

; Approach :
; Use xreplace to replace each pair in each recursive call
(defun sub (L S)
	(cond
    	((null S) L)
        (t (sub (xreplace (caar S) (cadar S)) (cdr S)))
    )
)
```

------

## Tips

------

- Set alias for testing

  ```lisp
  (setq t1 (xsum '(1 2 (3 4) (((2))))
  ```

