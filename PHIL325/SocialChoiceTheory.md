# Social Choice Theory

## Basic Terminology

---

- ***Social choice problem***: a decision problem faced by a **group**, 
  - in which individual is willing to state at least ***ordinal*** preferences over outcomes.
    - *Individual preference orderings*
    - must satisfy axioms of completeness, asymmetry and transitivity.
- ***Social preference ordering*** is formed by combine the individual preference ordering.
  - It reflects the preferences of the group.
- ***Social state***: the state of the world that includes **everything** that individuals are **care** about.
  - Example, choosing a tax level among high, moderate and low,
  - each tax level corresponds to a social state.
- ***Social welfare function*** refers to any decision rule that 
  - **aggregates** a **set** of individual preference orderings over ***social states*** into
  -  a ***social preference ordering*** over those states.

------

### Mathematic Notation

------

- An individual preference ordering is a vector / a list of ordered objects.
  - $I=[a,b,c,d,\{e,f\},g,h,...]$.
  - If some objects are equi-preferred, put them into a set and include that set into the vector.
- All individual preference orderings in society is a set of vectors.
  - $G=\{I,K,L,...\}$.
- The aim of social choice theory is to analyze if and how $G$ can be aggregated in a systematic manner into a social preference ordering $S$.
  - Given an arbitrary set $G$, which ***SWF*** would produce the best $S$.
- S is another vector that lists the group's preference ordering over the objects its individuals hold preferences over.
- ***SWF***: $G\to S$ 

------

## Voting Paradox

------

- **Majority rule** might end up with a cyclic preference ordering.
  - A: x > y > z
  - B: y > z > x
  - C: z > x > y
  - A and C => x > y 
  - A and B => y > z
  - B and C => z > x
  - In summary, x > y > z > x.

------

## Four Axioms

------

- Every normatively reasonable **SWF** should be *nondictatorial*.
  - It must not be the case that $S$ *always* coincides with the preference orderings of a particular individual.
  - No individual should be allowed to be a dictator.

------

### Decisiveness

------

- The ability to make decisions quickly and confidently.
- A group of people D (which may be a single-member group), which is part of the group of all individuals G,
  - $D\in G$
- is **decisive with respect to** the ordered pair of social states (a, b)
- **if and only if** state a is socially preferred to b whenever **everyone in D** prefers to a to b
- A group that is decisive with respect to all pairs of social states is simply **decisive**.

------

- **Nondictatorship** (**Condition D**): No single individual (no single-member group D) of the group G is decisive.
  - Majority rule meets this condition.
  - No individual will be a dictator as long as the majority rule is accepted.
- **Ordering** (**Condition U**): For <u>every</u> possible combination of individual preference orderings,
  - the social preference ordering must be complete, asymmetric, and transitive.
  - Majority rule is ruled out by this condition because of cyclic.
  - ***unrestricted domain***
- **Pareto** (**Condition P**): The **group** of **all individuals** in society is decisive.
  - Remark: it's the group being decisive but not all individuals.
  - i.e, if everyone in the group prefers $a$ to $b$, then the group should prefer $a$ to $b$.
- **Independence of irrelevant alternatives** (**Condition I**)
  - If all individuals have the same preference between $a$ and $b$
  - in two different set of individual preference orderings $G$ and $G'$
  - ,then society's preference between $a$ and $b$ must be same in $G$ and $G'$
- The problem is that it effectively excludes all **SWF**s 
  - that are sensitive to relational properties of the individual preference orderings.

------

#### Example of Independence of Irrelevant Alternatives

------

- $a$ and $b$ should depend only on individual preferences over **that** pair of social states (a, b).
- The social ranking of *a* and *b* must **not** depend on how some third (**irrelevant**) social state *c* is ranked by the individuals.
- In the old society, society preferred $a$ to $b$, simply because 
  - Old A - a > b > c
  - Old B - c > a > b
- In the new society, things are different, but the only difference that object c is ranked differently:
  - New A - c > a > b
  - New B - a > c > b
- Since New A and New B still agree that *a* is better than *b*, the new society must also prefer *a* to *b*.
- How *c* is ranked is ***irrelevant*** when it comes to determining the social preference between *a* and *b*.

------

### Violation of Four Axioms

------

- An aggregation procedure in which the group preference ordering **always mimics** 

  - the preference ordering of a certain individual or that of a certain subgroup violates the **condition D**.

- The pairwise comparisons method (often referred to as ***majority rule***) violates the **condition U**.

- **The Borda count** method violates the **condition I**.

  | 1    | 2    | 2    |
  | ---- | ---- | ---- |
  | A    | A    | B    |
  | B    | C    | C    |
  | C    | B    | A    |

  ------

  | 1    | 2    | 2    |
  | ---- | ---- | ---- |
  | D    | A    | B    |
  | A    | C    | C    |
  | B    | B    | D    |
  | C    | D    | A    |

------

## Arrow's Impossibility Theorem

------

- No ***social welfare function*** satisfies the four conditions, namely, 
  - **non-dictatorship**,
  - **ordering**,
  - **Pareto**,
  - **independence of irrelevant alternatives**,
- unless the group has **just one member** or the **number of social states is fewer than three**. 
- Some proposals to avoid the theorem's implications:
  - To defend the **majority rule** by rejecting the **condition U**
  - To defend the **Borda count** method by rejecting the **condition I**

------

## Sen on Liberalism and the Pareto Principle

------

- Sen argued that the Pareto principle is incompatible with the basic ideals of liberalism.
- **Minimal Liberalism**: There are **at least two individuals** in **society** such that
  - for each of them there is **at least one pair** of **alternatives** with respect to which she is ***decisive***,
  - that is, there is a pair $a$ and $b$, such that if she prefers $a$ to $b$,
  - then society prefers $a$ to $b$
  - (and society prefers $b$ to $a$ if she prefers $b$ to $a$).
- What Sen proved is that no **SWF** satisfies minimal liberalism, Pareto and the ordering condition.
  - ***The paradox of the Paretian Liberal***.

------

### Robert Nozick's View

------

- One of the most well-known proponents of liberalism in recent years,
- His main point is that Sen is **wrong** in constructing liberalism as property of an SWF.
- He claimed that it's better to better to think of liberalism as,
- a ***constraint*** on the set of alternatives that society should be allowed to make decision about.
- Nozick denies a part of the ordering condition known as "unrestricted domain".
- According to him, it's simply **false** that 
  - an ***SWF*** should be a function from **all possible** individual preference orderings 
  - to a social preference ordering over the same set of objects.

------

## Harsanyi's Utilitarian Theorems

------

### Individual Rationality

------

- Harsanyi rejects Arrow's view that individual preference orderings **carry nothing** but **ordinal information**.

  

- On his view, it is reasonable to assume that 

  - rational individual preference orderings can be represented in an ***interval scale***,

  - which satisfy the von Neumann and Morgenstern axioms for preferences over lotters.

    

- This directly implies that rational individual can represent their utility of a social state on an interval state.

  - preferences can be represented by a utility function that measures your utility on an interval scale

  

- ***Individual rationality***: All individual preference orderings satisfy the von Neumann and Morgenstern axioms of preferences over lotteries.

------

### The Chairperson

------

- Imagine an individual (who may or may not be a fellow citizen) who 
  - evaluates all social states from a moral point of view.
  - The ***Chairperson***.
- If the **Chairperson** is a fellow citizen, then he has two separate prefernce orderings
  - one personal preference ordering over all states
    - that reflects his **personal opinion**.
  - a separate preference ordering over the **same set** of social states
    - that reflects the **social preference ordering**. 
- The social preference ordering is the preferences the **Chairperson**,
  - exhibits in those - possibly quite rare - moments
  - when he forces a special impartial and impersonal attitude,
    - a moral attitude
  - upon himself.
- The conditions imposed upon the Chairperson's preference orderings:
  - The rationality condition
  - The moral condition

------

- What can be conclude about the Chairperson's social preference ordering?
  - given that it fulfills certain structural conditions
- **Rationality of a social preferences**: 
  - The **Chairperson**'s social preference ordering satisfies the von Neumann and Morgenstern axioms for preferences over lotteries. 

------

### Pareto

------

- It's the moral condition imposed on the Chairperson
- If $a$ is preferred to $b$ in at least one individual preference ordering,
  - and that there is **no** individual preference ordering in which 
    - $b$ is preferred to $a$
  - then, $a$ is preferred to $b$ in the Chairperson's social preference ordering.
- Furthermore, if all individuals are different, then so is the Chairperson in her social preference ordering.

------

## Harsanyi's First Theorem

------

- The three conditions imply that the Chairpersons' social preference must be
  - a **weighted** <u>sum</u> of the individual preference orderings,
  - in which the **weight**
    - represents its moral importance relative to the others

- From *individual rationality*, it follows that
  - individual preference orderings can be represented by utility functions that measure utility on interval scale.
- From *rationality of a social preferences*, it follows that 
  - the same holds true of social preference ordering.
- Let $u_i(a)$ denote individual $i$'s utility of state $a$
- Let $u_s(a)$ denote the utility of $a$ as reflected in the Chairperson's social preference ordering.
- Let $\alpha$ be a real number between 0 and 1. 
- Individual rationality, rationality of social preferences and Pareto together entail that:
  - $u_s(a)= \sum_{i=1}^{n} \alpha_i \cdot u_i(a)$ with $\alpha_i$ > 0 for i = 1, ..., n.
  - society's utility of state $a$ is weighted sum of all individuals' utility of that state.

------

### Remark

------

- The theorem doesn't guarantee that every individual preference ordering will be assigned the same weight.
  - Another moral constraint is needed.
- Within this theorem it is possible that different weights are assigned to different individuals.
  - Because $\alpha$ is greater than 0, each individual's preference ordering is assigned some weight 
  - but the weights can be unequal.

------

### Equal Treatment of All Individuals

------

- If all individual's utility functions $u_1, ..., u_n$ are expressed in **equal utility units**, 
  - then the Chairperson's social utility function $u_c$ must assign the **same weight** to **all individual** utility functions.

------

## Harsanyi's Second Theorem

------

- Given equal treatment of all individuals, the coefficients in ***Harsanyi's first theorem*** will be equal:
  - $\alpha_1=...=\alpha_n$
- $u_s(a)=u_1(a)+u_2(a)+u_3(a)+...u_n(a)$

------

