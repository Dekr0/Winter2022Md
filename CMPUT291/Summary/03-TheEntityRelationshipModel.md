# The Entity-Relationship Model
- The "world" is described in terms of
  - *entities*
  - *relationships*
  - *attributes*
---
## ER Model Basics
---
### Entity
---
- It is **distinguishable** object

  - person, thing, concept

- *Entity set* is a set of entities of the same *type*.

- Examples

  - students registered at UofA
  - flights offered by Air Canada

- Graphical representation

  ![image-20220113205848969](C:\Users\Dekr0\AppData\Roaming\Typora\typora-user-images\image-20220113205848969.png)
---
### Relationship
---
- It represents the fact that certain *entities* are related to each other.

- *Relationships set* is a set of relationship of *same type*.

- Examples

  - students enrolled in courses
  - cars registered to owners

- Graphical representation

  ![image-20220113205952582](C:\Users\Dekr0\AppData\Roaming\Typora\typora-user-images\image-20220113205952582.png)
---
### Attribute
---
- It describes a property of an *entity* or a *relationship*

- Example

  - student : id, name , major, ...
  - car : VIN, year, model, ...
  - flight : No, source, destination, ...

- **Underscore** to represent key in graphical representation.

- Graphical representation

  ![image-20220113210114590](C:\Users\Dekr0\AppData\Roaming\Typora\typora-user-images\image-20220113210114590.png)
---
### Key
---
- A **minimal** set of attributes that **uniquely identifies** each *entity* in an *entity set*
- Attributes of relationships - example
  - student enrolled in a course : year, semester, grade
  - book on loan : loan date, due date
- A relationship **does not** have a key
---
### Role
---
- The function of an *entity set* in *relationship set*.

- Role labels are needed whenever an *entity* has **multiple functions** in a *relationship set*.

  ![image-20220113210358265](C:\Users\Dekr0\AppData\Roaming\Typora\typora-user-images\image-20220113210358265.png)
---
## Constraints and Complications
---
### Type of lines and Arrow

------

- Normal lines - no constraint
- Thick lines - one entity and more than one entities
- (Normal lines +) Arrow - one entity is mapped into only one entity in another set (the direction of the arrow), or no entity is mapped
- Thick lines + Arrow - **For all** entities in one set, each entity is mapped into **only one** entity in another set (the direction of arrow). **No entity** is not mapped into **only one** entity in another set.

------

### Binary Relationship Types

---
- Many-to-Many : no constraint

![image-20220113211529693](C:\Users\Dekr0\AppData\Roaming\Typora\typora-user-images\image-20220113211529693.png)

- Many-to-One : each entity can only be mapped into at most one entity in another set

  ![image-20220113211620539](C:\Users\Dekr0\AppData\Roaming\Typora\typora-user-images\image-20220113211620539.png)

- One-to-One : each entity in set A is mapped into at most one entity in set B and each entity in set B is mapped into at most one entity in set A

  ![image-20220113211846169](C:\Users\Dekr0\AppData\Roaming\Typora\typora-user-images\image-20220113211846169.png)

---
### Ternary Relationships
---
- Not common, require 3 different set of entities

  ![image-20220113211956632](C:\Users\Dekr0\AppData\Roaming\Typora\typora-user-images\image-20220113211956632.png)

- Supplier **s** supplies part **p** for project **r**
- Ternary Relationships cannot be replaced by binary relationship by establish an relationship between each set. 
  - Binary relationship is not sufficient and cause ambiguity.
- Suppliers **s** does not necessary supply part **p** for project **r**, maybe other thing
- Part **p** is used for project **r** but part **p** is not necessarily supplied by suppliers **s**
---
### Participation Constraints

---
- Example : The participation of Projects in Supervises is said to be *total* (indicated by the thick line)

  - Force each project to have a supervisor

- Every  *pid* value in Projects must be in a "supervises" relationship with a *sin* (not null) of an employee

  ![image-20220113212457506](C:\Users\Dekr0\AppData\Roaming\Typora\typora-user-images\image-20220113212457506.png)

---
### Set-Valued Attributes
---
- Attribute value can be a set (in contrast to relational model)

- Example

  - Each employee can have one or hobby

  ![image-20220113212549903](C:\Users\Dekr0\AppData\Roaming\Typora\typora-user-images\image-20220113212549903.png)
---
### Weak entity
---
- A *weak entity* models an entity which is "part-of" an **owner entity**, and it cannot be uniquely **identified without** the primary key of the owner entity

- Relationship is One-to-Many

- *Weak entity* set has **total participation** in identifying relationship set

- Think about *weak entity* as a attribute that cannot be described by a single value of the **owner entity**

- Dotted underline indicates the keys of *weak entity*
  - Keys of *weak entity* are not unique
  
  ![image-20220113212635680](C:\Users\Dekr0\AppData\Roaming\Typora\typora-user-images\image-20220113212635680.png)
---
### ISA Hierarchy
---
- A new entity set as the *union* of two or more entity sets

- Attributes and relationships common to all lower-level entity sets are moved to the higher-level entity set.
  - Lower-level entity sets inherits the attributes and relationships in the high-level entity set

- Also consider forming a derived entity set by taking a subset of given entity set -> Specialization

  ![image-20220113212735943](C:\Users\Dekr0\AppData\Roaming\Typora\typora-user-images\image-20220113212735943.png)
---
#### Properties of ISA
---
- Inheritance
  - Attribute of super type are attributes of subtype
  - Key of super type is key of subtype
  - Relationships of super type are relationships of subtype

- Transitivity - Hierarchy of ISA
  - Undergrad student is subtype of Student, Student is subtype of Person, so Undergrad student is also a subtype of Person
---
#### ISA Constraints
- Covering constraints
  - Does every Students entity also have to be Graduates or an Undergrads entity ? (default : no)
- Overlap constraints
  - Can Joe be a Graduates as well as an Undergrads entity ? (default : disallowed)
---