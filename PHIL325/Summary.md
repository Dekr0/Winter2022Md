# Summary

## Dominance Principle

------

- Dominated acts must not chosen.

- Dominated acts
  - whose all outcomes under every state are **at least as rational as** other outcomes of other acts under every state
  - **and** there are some outcomes under some states are **less rational** than outcomes of other acts under those states

- Let $v(a_i, s_j)$ be the **value of the outcome** corresponding to the act $a_i$ and the state $s_j$.

------

### Weak Dominance

------

- ***Weak Dominance*** : $a_i$ ≽ $a_j$ if and only if $v(a_i, s) \geq v(a_j, s)$ for every state s. 

------

### Strong Dominance

------

- ***Strong Dominance*** : $a_i \succ a_j$ if and only if v($a_i$, $s_m$) $\geq$ v($a_j$, $s_m$ ) for every state $s_m$, and there is some state $s_n$ such that v($a_i$, $s_n$) > v($a_j$, $s_n$).

------

## Maximin Principle

------

- The maximin principle focuses on the ***worst*** possible outcome of each act.
- One should ***maximize*** the ***minimal*** value obtainable with each act.
- If the **worst possible outcome** of an act is **better than** the **worst possible outcome** of another act, the **first** act should be chosen.

- Formally speaking : $a_i \succeq a_j$ if an only if min($a_i$) $\geq$ min($a_j$).
- If the minimum value corresponding to the outcomes of two or more acts are the same, the maximin principle ranks the acts as equally rational.

------

##  Leximin Rule

------

- Extended version of *Maximin Principle*
- Let $min^1(a_i)$  be the value of the worst outcome of act $a_i$,
- $min^2(a_i)$ be the value of its second worst outcome,
- In general,$min^n(a_i)$ be the value of its n-th worst outcome

- $a_i$  $a_j$ if and only if there is some positive integer n such that
  - $min^n(a_i) > min^n(a_j)$
  - regardless $min^m(a_i) = min^m(a_j)$ for all m < n

------

## Maximax principle

------

- The maximax principle focuses on the best outcomes.
- Rationality requires us to prefer alternatives in which the best possible outcome is as good as possible.
- You should maximize the maximal value obtainable with an act.

------

## Optimism-pessimism principle

------

- A decision maker’s degree of optimism can be represented by a **real number** α between 0 and 1.

- α = 1: maximal optimism

- α = 0: maximal pessimism

- max ( $a_i$ ) : the best outcome of act $a_i$

- min ( $a_i$ ) : the worst outcome of act $a_i$

  

- The value of act $a_i$ = [α · max($a_i$)] + [(1 - α ) · min($a_i$)]

  - $\alpha \cdot max(a_i)$ is optimism part on act $a_i$
  - $(1-\alpha) \cdot min(a_i)$ is pessimism part on act $a_i$

- α is a subjective interpretation



- α : an agent’s optimism index
- [α · max($a_i$)] + [(1 - α ) · min($a_i$)] : an act's α-index (subjective)



- Principle definition : $a_i > a_j$ if and only if α-index ($a_i$) > α-index ($a_j$)
  $$
  [\alpha \cdot(a_i)] + [(1-\alpha)\cdot min(a_i)] > [\alpha \cdot(a_j)] + [(1-\alpha)\cdot min(a_j)]
  $$

- If $\alpha=1$, evaluate $\alpha$-index  $\rightarrow max(a_i)$ which means the optimism pessimism rule
  collapses to the maximax rule.

- If $\alpha=0$, evaluate $\alpha$-index $\rightarrow min(a_i)$ which means the optimism pessimism rule collapses to the maximin rule.



- Note that, in order for this rule to work, the value of outcomes should be measured on an interval scale.



- Is it rational to focus just on the best and the worst cases?

- Determine a series of $\alpha$, $\alpha_1$, $\alpha_2$, ..., $\alpha_n$, such that $\alpha_1+\alpha_2+...+\alpha_n=1$, then define $\alpha$-index of an act $a_i$ as
  $$
  \alpha_1 \cdot(a_1,s_1) + \alpha_2 \cdot (a_1, s_2) + ... + \alpha_n \cdot (a_1,s_n) = \alpha(a_1)
  $$

- then choose the act with the **greatest** $\alpha$-index



- Note that $\alpha_1$, $\alpha_2$, ..., $\alpha_n$ are ***not probabilities***
  - similar to (subjective) **probabilities**
  - but not ***equivalent to*** **probabilities**
- They are chosen only according to how **much importance** the decision maker attaches to the best, the second best, ..., and the worst outcome of each act.
- The **relative importance** of an outcome **doesn’t necessarily** **correspond** to its probability.

------

## Minimax Regret

------

- The best alternative is one that **minimizes** the **maximum** amount of regret.
- $a_i \succ a_j$ if and only if the maximum regret of $a_i$ is less than the maximum regret of $a_j$, or to put it formally :

$$
max\{(v(a_i, s_1)-max(s_1), (v(a_i, s_2)-max(s_2)), ...\} < max\{(a_j,s_1)-max(s_1),(v(a_j,s_2)-max(s_2)), ...\}
$$

------

### Procedure

------

- The value of regret for each outcome is calculated by subtracting the value of the **best outcome** of **each state** from the value of the
  outcome in question.
  - This obtains the ***regret matrix***
- The act chosen based on Minimax Regret principle is an act whose maximum regret for all states is minimum among other acts for all states.
  - Find the maximum regret for each act.
  - Choose the act with the least maximum regret

------

## The principle Of Insufficient Reason

------

- If one has no reason to think that one state of the world is **more probable than another**, then all states should be assigned **equal** probability.
- By applying the principle of insufficient reason, an initial decision problem under **ignorance** is transformed into a decision problem under **risk**.
- If one advocates the principle of maximizing expected value as the best rule for decisions under risk, then the principle of insufficient reason can be stated as:
- $a_i \succ a_j$ if and only if $\sum_{x=1}^{n}\frac{1}{n}v(a_i,s_x)>\sum_{x=1}^{n}\frac{1}{n}v(a_j,s_x)$

------

## Relationship Properties

------

- $x \succeq y$ if and only if $x \succ y$ or $x \sim y$

- $x \sim y$ if and only if $x \succeq y$ and $y \succeq x$

- $x \succ y$ if and only if $x \succeq y$ and not $x \sim y$

  

- For every x and y, it should hold that : 
- **Completeness** $x \succ y$ or $x \sim y$ or $y \succ x$
- **Asymmetry** If $x \succ y$, then it is *false* that $y \succ x$.
- **Transitivity** If $x \succ y$ and $y \succ z$, then $x \succ z$.
- **Negative Transitivity** If it is *false* that $x \succ y$ and *false* that $y \succ z$, then it is false that $x \succ z$.
  - It implies that indifference is **transitive** (if $x \sim y$ and $y \sim z$, then $x \sim z$).
  - Indifference does not follow form the assumption in **Transitivity**

------

## Neumann and Morgenstern Method

------

- **Z** is a finite set of **basic prizes**
- **L** is a set of lotteries that can be constructed from **Z** by applying the following inductive definition:
  - Every basic prize in **Z** is a lottery
  - If A and B are lotteries, then so is the prospect of getting A with probability p and B with probability (1-p), for every 0 $\leq$ p $\leq$ 1.
  - Nothing else is a lottery.

------

### Detailed Example

------

- Simpson is going to go to a rock concert. Three bands are playing tonight. He thinks A is better than B, which is better than C.
- Two tickets are available :
  - Ticket 1 entitles him to a 70% chance of watching A and a 30% chance of watching C.
  - Ticket 2 entitles him to watch B with 100% certainty.
- Upon reflection, he finds the two tickets equally attractive.
- Suppose we know that Simpson always acts according to the principle of maximizing utility.  
- By reasoning backward, we can find the utilities he attaches to A, B, C. That is have to solve the following equation:

$$
0.7 \cdot u(A) + 0.3 \cdot u(C) = 1.0 \cdot u(B)
$$

- Stipulate that u(A) = 100 and u(C) = 0, then it turns out that u(B) = 70.
  - u(A) and u(C) are picked arbitrary. 

------

## The Mathematics of Probability

------

## Kolmogorov Axioms

------

- $1\geq p(A) \geq 0$, probability of every event lies between 0 and 1.
- $p(S) = 1$, probability of the entire sample space is 1.
- If $A \cap B = \empty$, then $p(A \cup B)=p(A)+p(B)$ (keyword, sample space).

------

- If it is more natural to think the question by counting thinking instead of using probability for proposition, use counting instead.
  - For example, choose one red card and one black card without drawback.
- Notice that condition probability need to consider independency of an event / proposition.
- Conditional Probability :
  - p(~B|A) = 1 - p(B|A)
  - same for p(~A|B) = 1 - p(A|B) 
- To construct inverse conditional probability :
  - Look for what the question is asking about to

------

### Unknown Priors

------

- Prior probability / unconditional probability of B : p(B)
- Probability that are given
  - Probability of A happen n times given not B : p(A|~B) = $x^n$
  - Probability of A happen n times given B : p(A|B) = $x'^n$
- Find probability of B / not B happen given A (posterior): p(B|A) and p(~B|A)