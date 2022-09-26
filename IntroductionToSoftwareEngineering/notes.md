## UML
---
- When reading a UML diagram, think of a container as an object
---
## Encapsulation
---
- `private` modifier does not guarantee that an member is guarantee

- Keep in mind when creating getters and setters
- If every class or a class has a getter and setter for every member in the class,
  - then it deviates the concept of encapsuation since clients now can chnage all the members of a class with available getters and setters
  - There's no encapsulation even all members are private
---
## Decomposition
---
- Search an detailed and clear explanation from documentation and specification for UML association, aggregation, composition
- When start on planning, an method is to start with weak relationship and add constraints as needed.
---
## Relationship and Aggregation
---
- weak "has-a" relationship
	- E.g., `class Section` and `class Student`
		- A section can have multiples of student
		- A student can belong to different sections or A student can only belong to one section
- strong "has-a" relationship
	- E.g., `class Person` and `class Brain`
		- a person die and that person's brain must also be die (i.e., an `Brain` object must be destoryed)
---
## Generalization Principles
---
- "is-a" test is not bidirectional
  - It does not provide enough details about inheritance relationship.
  - Although an "is-a" test is passed, it does not guarante that the design is logical sounded / correct
    - for example, locking up implementation, inhertting unecessary members, context situation under super class type
- ***Liskov substitution princle*** $\rightarrow$ a more reilable test
  - should be ***substitutable*** anywhere a reference to a superclass is used
- Think about
  - long term
  - issues using inheritance

- When you are trying to solve a problem in an akward way and need some inconventional work around
  - This is a good implication you are doing something wrong, or something wrong is within the design
- When you are entrust clients to use the class properly instead of enforce the rule during the design and implenment stage
  - this will be not reliable design 
- Looking a quick fix and quick work around during the class implementation can be a long term problem
  - The more workaround and quick fixes one have, it most likely implies that there are issues within the design.
  - "Fixing it later" most likely imply that living with issues
  - Thinking a better design is more reliable solution
- Imapproiate design will lead to a design become difficulty adapt changes.
---
### Example
---
```Java
public class Dog {
	public void bark() {

	}

	public void fetch() {

	}
}


public class Cat extends Dog {

}
```

- Cat "is a" Dog $\rightarrow$ not logical correct

```Java
public class Window {
	public void show() {

	}

	public void move() {

	}

	public void resize() {

	}
}

public class FixSizeWindow extends Window {

}
```

- FixedSizeWindow "is a" Window but the design is not sounded because it inherits methods that should not apply to the behaviors of `FixedSizeWindow`

- A class `ProjectTeam` extends `ArrayList`. Issues :
  - What if a project team require a different type of data structure to model it in the future?
    - The original design under `extends ArrayList` cannnot resist the future change.
    - Flexibility is not persevered
---
## UML and OOA&D
---
### Object-Oriented Analysis
---
- The followings are not always true:
  - nouns may lead to classes and attributes
  - verbs may laed to relationships and methods
    - or verbs might behave as a nouns
- Be careful verbs and nouns might not be turned out to be what they suppose to be in the real implmenetation
  - verbs might not be a method / relationship or should not be a method / relationship due to design problem
  - same concept applys to verbs
---
### Discover Objects
---
- Entity objects
  - least techs dependent
  - "data structure"
  - as pure as possible
    - i.e., involves only essential techs to represent the entity
- Boundary objects 
  - Objects that requires interface for the users
  - Its usage is at the edge of boundary 
- Control objects and Boundary objects are easily to change since it's heavyily tech dependent (framework, platform, etc.)
---
### CRC Cards
---
- Role play to checkout whether the design make sense and sound
### Evaluation
---
- is it necessary create a class to encapsulate a simple thing
- need of decomposition or composition
---
### Guidelines
---
- Ask a question for a problem
  - simplify the complexity due to clarification
- Assumptions
  - Make and clear it
- Elements within modularity usually cnanot satisfy together
  - they are conflict each other
    - reduce coupling $\rightarrow$ increase responsibility $\rightarrow$ reduce conhesion
    - same for cohesion but in another way around
  - find a balance point
  - OOP try to make a class more cohesion but the coupling can be complicate