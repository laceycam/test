# StarCraft Project: Tactical Path Planning for Reconnaissance

---

| Group Member     | Email Address            | SID       |
| ---------------- | ------------------------ | --------- |
| Jiehong Jiang    | jjhjiang@ucdavis.edu     | 914974552 |
| Colin Beardshear | crbeardshear@ucdavis.edu | 914385840 |
| Malini Pathakota | mmpathakota@ucdavis.edu  | 913241367 |
| Hoseung Lee      | hoslee@ucdavis.edu       | 914001975 |
| Lacey Campbell   | lbcampbell@ucdavis.edu   | 912170808 |
| Sri Kavya Dindu  | sdindu@ucdavis.edu       | 650804061 |

---

### Introduction

StarCraft II is a RTS game where players gather resources and strategically
spend them on units, buildings, and research in order to achieve the ultimate
goal of overpowering the opponent and winning.
Because this game relies heavily on choosinf the right strategy early in the
game, being able to predict the enemy's army formation becomes a very valuable
skill.
Current army prediction algorithms learn from data gathered from gameplays on
build orders, amount of resources, and current army formation to predict which
strategy the enemy is using.
However, in addition to determining the strategy the enemy is using, being able
to predict every specific build the enemy makes during certain periods of time
during the game drastically increases the player’s chance of victory.
If the player can correctly predict the exact units that are coming for them at
specific times during the game, they can make better decisions on how to
counter the enemy.
Our objective is to create an algorithm that predicts the the enemy’s army
composition given the information that’s been gathered by scouts, including
construction units, buildings, and current army formation.
We call this Dynamic Army Prediction.


### Aspiration

A dynamic army prediction algorithm could ultimately be utilized by gameplay
bots in real games. Since the algorithm was built to observe general features
in StarCraft, instead of being given the tech tree for a specific faction
first, it can be easily trained to predict the actions of opponents in
different factions.


### Plan

To make our methods understandable and approachable, we mainly use linear
regression as a statistical approach to analyze the relationship between every
pair of two units; in order to predict a specific unit, we use its relationship
with all the others. The initial model is less effective as the game
progresses, so we partition the game into ten minute sections that each get
their own linear regression model. We compare this to a Bayesian Model
predicting the opponent’s opening build to determine how our prediction
accuracy compares to other models.

