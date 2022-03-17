# SQL

## Views

------

- Why
  - Code reuse
    - Once definition of the view is defined, it remains in there 
  - Privacy and security 
    - hiding sensitive data
    - prevent providing access to the entire table
  - Data Independent (Three layer structures)
    - Application see **view** as a table
- **View** is a query that return a table but it can be treated as a **table**
  - It is different from temporary table. 
    - A temporary table is an actual table that physically exists in the database where **view** is a **definition**.
    - A temporary table can be updated where **view** can only be updated in some situations.

------

## Subqueries

------

- Subqueries can be used in (purpose / use, check textbook)
  - `from`
  - `where`
  - `having`

------

## NULL

------

- `IS NULL` and `IS NOT NULL`
- simple predicates
  - example : `city = 'Edmonton'` is evaluated to `UNKNOWN` if `city` is `null`
  - example : `city` <> `edmonton` is evaluated to `UNKNOWN` if `city` is `null` 
  - In these similar cases, DBMS doesn't evaluate them to `true` 
    - Since they aren't `true`, DBMS doesn't return those records with `null`
    - This **doesn't** mean it's `false` (**3-valued** logic)
- SQL uses **3-valued** logic :
  - `true`, 1
  - `false`, 0
  - `unknown`, $\frac{1}{2}$
- Arithmetic expression :
  - example : `balance + 100` : `null` if balance is `null`

- Grouping
  - `null` values are grouped together
- Complex predicates
  - example : `city='Edmonton and balance > 2000'`
    - `eval( a and b ) = min( eval(a), eval(b) )`
    - `eval( a or b ) = max( eval(a), eval(b) )`
    - `eval( not a ) = 1 - eval(a)`
  - SQL uses **3-value logic** 
  - In `select ... from ... where C`, a tuple `<r1, ..., rn>` is going to be in the output if `C(<t1 , ..., tn>)` evaluates to `1`
- `ifnull()`
  - example : `ifnull(city, '') = 'Edmonton'`
    - if `city` is null, replace with empty string `''`

------

### Aggregation

------

- `null` is counted in `COUNT(*)` and is ignored in **all other forms of aggregation**
  - example : `coun(city)`, `avg(balance)`
- `count` applied to a table with no rows returns `0`
- `sum, avg, max, min` applied to a table query with no rows returns `null`

------

## Constraints (Assertion)

------

- **ER Modelling** example : Every project has one or more grad working on it.

- Tables : 

  - `grade( sin, ... )`
  - `project( pid, ... )`
  - `worksgp( sin, pid, ... )`

- Every `pid` need to present in `worksgp`

- ```sql
  CREATE ASSERTION prj_work_part CHECK
  (NOT EXISTS (SELECT pid 
  			FROM project 
  			EXCEPT SELECT pid 
  			FROM works_gp)
  )
  ```

- One issue is that how to insert data in these type of tables ?

  - If a record need to be inserted into project, assertion constraint is violated
  - If a record need to be inserted into worksgp to prevent violating assertion, foreign key is violated
  - Solved by transaction, dropping constraint temporarily 

------

## Constraints (Trigger)

------

- A trigger activates if an action happen (before / after / instead of) to a table, and the specified condition meets

  - run statement `BEGIN ... END` block
  - useful for logging information when actions happen
  - useful for updating views
  - `new` and `old` keyword to distinguish the record being insert / update / delete

- Exercise crate a trigger that prevents the insertion of a new loan if the customer has already two loans

  - ```sql
    CREATE TRIGGER has-loan
    	BEFORE INSERT ON loan
    	WHEN (EXISTS 
    			(SELECT bname, cname 
                 FROM loan
                 GROUP BY cname
                 HAVING COUNT(*) > 2
    			)
    		  )
    	BEGIN 
    		RAISE(ABORT, 'This customer already has two loans');
        END;
    ```

    

  