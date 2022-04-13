# Game Theory II

## The Nash Equilibrium

------

- Prisoner's dilemma and Stag hunting are examples of nonzero-sum game
  - symmetric game
  - loss or gain made by each player is not the exact opposite of that made by the other player.
- *an **equilibrium point** is [a set of strategies] such that each player’s ... strategy **maximizes** his pay-off **if** the **strategies** of the **others** are held **fixed**. Thus **each** player’s strategy is **optimal** against those of the others*

------

### Nash's basic idea

------

- **Rational** players will do whatever they can to **insure** that they do no feel **unnecessarily unhappy** about their decision.
- If a rational player knows that he could **do something better**, given that his **assumptions** about the **opponent** are held **fixed**.
- Then the player will **not choose** the **nonoptimal strategy**.
- Hence, rational players will always play strategies that constitute ***Nash equilibriums***.

------

- Many nonzero-sum games have >= 1 one ***Nash equilibrium***

  - Stag hunt

  - |               | C1: Hunt stag | c2: hunt hare |
    | ------------- | ------------- | ------------- |
    | R1: HUNT STAG | 25, 25*       | 0,5           |
    | R2: HUNT HARE | 5,0           | 5,5*          |

  - (R1, C1) and (R2, C2) are ***Nash equilibria***.

  - Detail explanation (Page. 265)

- **Nash's equilibrium** concept eliminates those strategies that will not be played.

------

### Decision Under Risk

------

- It seems reasonable to look at game like stag hunt as a decision under risk.
- Row assign a subjective probability $p$ to the state in which 
  - Col plays C1 given that Row play R1,
- and probability 1 - $p$ to the state in which
  - Col plays C2 given that Row play R1.
- Furthermore, Row assign a probability $q$ to the state in which
  - Col plays C1 given that Row play R2
- and probability 1 - $q$ to the state in which 
  - Col plays C2 given that Row play R1
- Choose R1 over R2 ***if and only if***  $25p+0(1-p)>5q+5(1-q)$
  - p > 1/5
- This mean Row's subjective probability is higher than 1/5 that Col will hunt for stag given that you do so, then you should also hunt for stag.
- Furthermore, Col should reason in the exactly the same way since the game is symmetric.
- This give us two clear and unambiguous recommendations, which may of course be applied to similar situations ***mutatis mutandis***

- A decision maker who is **risk averse** to a **sufficiently** high degree will **always** hunt for hare since that will give him 5 kg of meat for sure.
  - what is best for each (risk-averse) individual may no be best for group as a whole
- In order to reach the outcome that is **best for a group** playing stag hunt, we have to insure that the players are prepared to take at least **moderate risks**.
  - **Balance** between **risk aversion** and **mutual trust**
  - Importance of promoting trust in a society and insuring that people are not too risk averse.

------

## Pareto Efficiency

------

- A state is ***pareto efficient*** (optimal) **if and only if** no one's utility level can be increased unless the utility level for someone else is decreased.
- In stag hunt, (R2, C2) is not a ***pareto efficient*** state, but (R1, C1) is.
- The idea is that all states are not ***Pareto efficient*** should be avoided.
- As explained above, individual rationality does not by any means guarantee that society will reach a ***Pareto efficient*** state.

------

## Tit for Tat

------

- A strategy defines the following : 
  - always **cooperate** in the first round, 
  - and thereafter **adjust** your behavior to **whatever** your opponent did in the previous round.
- Thus, in the second round you should cooperate if and only if the opponent cooperated in the first round.
- It can be modified by introducing probabilistic conditions.

---

## Grim Trigger Strategy

---

- A version of tit for tat.
- Each player **cooperates** in the **inital round** of the game as well as in every future round as long as the other player cooperates.
- As soon as the other player defects, the player will defect in all future rounds of the game, no matter what the other players does.

------

## Straightforward vs. Constrained Maximizers

------

- *Straightforward maximizers* always play the dominant strategy, and refuse to cooperate.
- *Constrained maximizers* cooperate with others *constrained maximizers* but  not with *straightforward maximizers*.
- Gauthier argues that it's rational to be a *constrained maximizer* rather than a *straightforward maximizer*.
- Self-interested rational constrained utility maximizers will come to agree on certain "moral" rules.
