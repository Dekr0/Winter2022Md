# Relational Database
## Relations (Tables)
---
- A relation (table) consists of *instance* and *schema*

- A relation consists of a set of rows (tuples)

- A relation has *keys*
---
### Instance
---
- Instance is the table content with rows and columns

- #Rows = cardinality (基数)

- #Fields = degree / arity
---
### Schema
---
- Schema is the table structure with name and *type* of columns
---
#### Type
---
- Type also defines *domain*

- The type (domain) of each field is specified by user / programmer, and enforced by the DBMS

- *Domain* consists of a set of values from which the values of an attribute are drawn
---
## keys
---
- Please distinguish *"key"* and *superkey*
---
### "key"
---
- A set of fields is a key for a relation if it is both (A set of fields can consist of a single field).
  - *unique* : **no two distinct tuples** can have **same** values in **all *key* fields**.
  - *minimal* : no subset of a key is a key.
---
#### Primary Key
---
- A relation can have only one primary key (one defined by DBA - Database Administrator).
  - Use *PRIMARY KEY* to define

  ```sql
  CREATE TABLE Enrolled(
      [sid] char(8), 
      [cid] char(8), 
      [name] char(15), 
      PRIMARY KEY([sid])
  );
  ```

  - Fields need to be *NOT NULL*

---
#### Candidate Key
---
- A relation can have many candidate keys.
  - use *UNIQUE* to define

  ```sql
  CREATE TABLE Students(
      [sid] char(8), 
      [name] char(8), 
      [email] char(32) 
      PRIMARY KEY ([sid]), 
      UNIQUE([name], [email])
  );
  ```

- Primary key can be picked from one candidate key that is most important.
---
#### Foreign Key (FK)
---
- Foreign key is a set of field that 'refers to a tuple in another relation

- Foreign key corresponds to a key (either primary or candidate) of the other relation
---
### Superkey
---
- 1st condition of primary key holds but 2nd condition may not.
  - Example : (sid, cid)
---
## Constraints
---
### Integrity Constraints (ICs)
---
- It is also called domain constraints

- It hold for any instance of the database
  
- A legal instance of a relation is one that satisfies all specified ICs

- When relations are modified or schema is defined, ICs will be checked
---
### Primary Key Constraints
---
### Referential Integrity
---
- All FK constraints are enforced by *actions*
  - no dangling references
---
#### Actions
---
- Only one action is allow for one type of behavior (*INSERT*, *UPDATE*, *DELETE*, etc.
  - Rejection / No action
    - reject an tuple being inserted if it does not have a set of existent values in the set of fields of tuple for that a key
    - *DELETE* request if deletes a set of tuples being reference from other table(s)
  - *CASCADE*
  - *SET NULL* / *SET DEFAULT*
---

