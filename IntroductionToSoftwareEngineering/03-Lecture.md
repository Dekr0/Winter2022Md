## UML
---
- When reading a UML diagram, think of a container as an object
---
## Encapsulation
---
- `private` modifier does not guarantee that an member is guarantee
---
## Decomposition
---
- Search an detailed and clear explanation from documentation and specification for UML association, aggregation, composition
- When start on planning, an method is to start with weak relationship and add constraints as needed.
---
### Relationship and Aggregation
---
- weak "has-a" relationship
	- E.g., `class Section` and `class Student`
		- A section can have multiples of student
		- A student can belong to different sections or A student can only belong to one section
- strong "has-a" relationship
	- E.g., `class Person` and `class Brain`
		- a person die and that person's brain must also be die (i.e., an `Brain` object must be destoryed)
---
