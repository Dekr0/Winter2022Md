# Game Theory I

## A taxonomy of games

------

### Zero-sum games vs. nonzero-sum games

------

- In a ***zero-sum game***, a player wins **exactly** as much as the opponent **lost**.
- In a ***nonzero-sum game***, games don't satisfy the above criterion.

------

### Non-cooperative vs. cooperative games

------

- In a ***non-cooperative game***, players are **not able to form binding agreements**.
- Sometimes it is rational for rational decision makers to cooperate even when no binding agreement has been made or could have been made
- In a *cooperative game*, players **can agree on binding contracts** 
  - that forces them to respect whatever they have agreed on.

------

### Simultaneous-move vs sequential-move games

------

- In ***simultaneous game***, each player decides on her strategy **without knowing other's decisions** (Rock, paper, scissors)
- In ***sequential games***, the players **have some (or full) information**
  -  about the **strategies** played by the other players in earlier rounds
  - Ex: Chess (perfect information)

------

### Perfect information vs. Imperfect information

------

- Both are subset of ***sequential games***
- In games with ***perfect information*** the players have full information about the strategies played by the other players

------

### Symmetric vs. non-symmetric games

------

- In a symmetric game, all players face the same strategies and outcomes
- ![SYM vs ASYM](SymmetricGame.png)
- Leftmost is symmetric, rightmost is asymmetric

------

### Two person vs. n-person games

------

- ***Two person game*** is a game that is played by exactly two players.
  - what matters is the number of players
- An $n$***-person game*** is a game played by an arbitrary number of players.
  - Difficult to analyze

------

### Non-iterated games vs. iterated games

------

- A ***non-iterated game*** is played only once, no matter how many strategies it comprises.
- An ***iterated game*** is played several times.

------

### Pure strategies vs. mixed strategies

------

- To play a ***pure strategy*** is just to choose a strategy among others
- To play a ***mixed strategy*** is to choose pure strategies with **probabilities**.
  - if A and B are two pure strategies, 
    - then to do A with the probability p
    - and B with probability (1-p) is a mixed strategy.

------

## Prisoner's Dilemma

------

### Description

------

- Police have caught two persons, Row and Col.
- They are kept separately and cannot communicate.
- The officer says to each of them that:
  - If both confess, each of them will get 10 years in prison.
  - If one confesses and the other doesn't,
    - one who confesses get only 1 year
    - the other 20 years
  - If both deny, each of them will get 2 years.
- The decision matrix
- ![Decision Matrix of Prisoner's Dilemma](DecisionMatrixPD.png)

------

### Analysis

------

- Both players are **rational** leads them to an outcome which is **not optimal** for them as **a group**.
- What is **optimal** for **each individual** need **not coincide** with what is **optimal** for the **group**.
- The best strategy for them as group, they would deny the charge. 
- The assumption that the **opponents acts rationally** does **not matter**.
  - Even if Row knows that Col is going to deny the charge,
  - the **rational choice** for Row is to **confess**.
  - Even if Row and Col can
    - **communicate** and coordinate their strategies
    - ***promise*** each other to deny the charge,
  - the result remains the same.
    - The **rational choice** for Row is to confess

------

## Common Knowledge and Dominance Reasoning

------

- Many games can in fact be solved by just applying the ***dominance principle*** in a clever way.

------

### A number of technical assumptions

------

- *All players are rational*.
  - They try to play strategies that **best promote** the objective they consider to be **important**.
  - This not mean that all players must be selfish.
- *All players know that other players are rational*.
  - $n$th-order common knowledge of rationality
- ***Dominance principle** is a valid principle of rationality*.
  - Recall ***dominance principle*** in ***Decisions Under Ignorance***

- It makes sense to accept this principle only in cases where
  - one thinks the players' strategies are causally independent of each other.

------

### Dominance Principle

------

- Notice, there are two ways to apply ***Dominance principle***

- First way (***minimax principle*** ?)

  1. find the minimum for each row

  2. select the maximum minimum from step i
  3. find the maximum for each column
  4. select the minimum maximum from step iii
  5. The result will be the equilibrium point
  6. Does not work if minimums for all rows have an opposite sign compared to maximums for all columns

- Second way: (matrix reduction, suit better in zero-sum game)

- Eliminating rows (or columns) which are dominated by other rows (or columns) respectively

  1. Dominance property for rows:
     1. x <= y (x is dominate by y)
     2. If all the entries in a row should be less tan or equal to the corresponding entries of another row, then that row can be deleted
  2. Dominance property for columns:
     1. x >= y (x is dominate by y)
     2. If all the entries in a column should be greater than or equal to the corresponding entries of another column, then that column can be deleted
  3. Keep repeating the above process until find the equilibrium point

------

#### Example

------

- |      | c1   | C2   | C3        |
  | ---- | ---- | ---- | --------- |
  | R1   | 1,3  | 2,2  | 1,0       |
  | R2   | 3,2  | 3,3  | ***2,7*** |
  | R3   | 1,1  | 8,2  | 1,4       |

- Row won't play R1 since it's dominated by R2

- No matter which Col decides on, Row will be better off if Row plays R2 rather than R1

- Therefore, both players know for sure Row will play either R2 or R3.

- Given that Row won't play R1, C3 dominates C2 and C1.

- Hence, both players can conclude that Col will play C3.

- Furthermore, since, Col will play C3, Row will be better off playing R2.

------

### Drawback

------

- |      | c1   | C2   | C3   |
  | ---- | ---- | ---- | ---- |
  | R1   | 1,3  | 2,4  | 1,0  |
  | R2   | 3,3  | 3,3  | 0,1  |
  | R3   | 4,2  | 2,0  | 1,3  |

- ***Dominance principle*** doesn't always directed us toward clear, unambiguous and uncontroversial conclusions.

- There are also cases in which ***dominance reasoning*** lead to unacceptable conclusions

  - ***Centipede game***
  - Only irrational people can get more money

------

##  Two-Person Zero-sum Games

------

- It's always played by only two players
- Whatever amount of utility is gained by one player is lost by the other.
  - If the utility of an outcome for Row is 4, it's -4 for Col
- Two-person zero-sum games can be presented by listing only the outcome for *one player*
  - By convention, **list Row**'s outcomes
  - **knowing** what the **outcome for Row** will be, then automatically **know** the outcome for **Col**.
- Naturally, Row **seeks** to maximize the numbers in the matrix, whereas Col tries to keep the **number as low as possible**

------

### Nash Equilibrium

------

- A pair of strategies is in equilibrium **if and only if** 
  - it holds that once this pair of strategies is chosen, 
  - **none** of the players **could reach** a **better outcome** by **unilaterally** switching to another strategy.

------

#### Example

------

- |      | C1   | C2   | C3   |
  | ---- | ---- | ---- | ---- |
  | R1   | 3    | -3   | 7    |
  | R2   | 4*   | 5    | 6    |
  | R3   | 2    | 7    | -1   |

- No strategy is dominated by the others.
- It's easy to figure out what rational players will do.
- Consider (R2, C1)
- If Col *knew* that Row was going to play R2, 
- then Col would not wish to play any other strategy, 
  - since Col tries to keep the numbers down.
- Furthermore, if Row *knew* that Col was going to play strategy C1, Row would have no reason to choose any other strategy.
- Hence, if that pair of strategies is played, 
- no player would have any good reason to switch to another, as long as the opponent sticks with his strategy.

------

- ***Minimax condition***: A pair of strategies are in equilibrium if (but not only if) 
  - the outcome determined by the strategies equals 
    - the **minimal** value of **row**
    - the **maximal** value of the **column**
- It has been proved that if there are more than one equilibrium point
  - then all of them are either on the same row or in the same column.

------

### Mixed Strategies 

------

- ***Minimax criterion*** is not sufficient for solving every two-person zero-sum game.

  - |      | C1   | C2   | C3   |
    | ---- | ---- | ---- | ---- |
    | R1   | 0    | -100 | +100 |
    | R2   | +100 | 0    | -100 |
    | R3   | -100 | +100 | 0    |

------

#### The minimax theorem

------

- Every two-person zero-sum game has a solution
- If there is no solution for a two-person zero-sum game using pure strategy, it must involve mixed strategy.
- i.e. there is **always** a **pair** of strategies that are in ***equilibrium***
- if there is **more than one pair** they all have the **same expected utility**.

