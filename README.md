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

## Introduction
### Problem

StarCraft II is a RTS game where players gather resources and strategically
spend them on units, buildings, and research in order to achieve the ultimate
goal of overpowering the opponent and winning.
Because this game relies heavily on choosing the right strategy early in the
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
Our objective is to create an algorithm that predicts the enemy’s army
composition given the information that’s been gathered by scouts, including
construction units, buildings, and current army formation.
We call this _Dynamic Army Prediction_.

There are currently many algorithms that predict the strategy the enemy will
utilize based on their army composition and information gathered from the
scouts; however, there are no algorithms specifically aiming to predict what
the enemy will build next based on the units they already possess, thus making
our solution to the problem of army prediction unique.

One such algorithm that predicts the enemy’s overall strategy rather than
immediate builds is a Bayesian Model for Opening Prediction.
This project predicts the enemy’s opening strategy and its possible technology
trees; however, it differs from our approach in two main ways.

First, the model predicts a strategy, whereas we focus on current army
composition and, ultimately, future army composition.

Secondly, it predicts the strategy at the beginning of the game, whereas as our
solution is a dynamic/real time implementation.

Another similar project is Combat Prediction based upon the Lanchester
Attribution Laws.

This project uses the above mentioned model to hypothesize about the enemy
army’s combat strategies, technology, and resources.

It addresses a much wider scope than our solution, and, unlike the previously
stated project, Combat Prediction aims to work in real time.

Link to enemy strategy prediction algorithm:

https://hal.archives-ouvertes.fr/hal-00607277/file/OpeningPrediction.pdf(https://hal.archives-ouvertes.fr/hal-00607277/file/OpeningPrediction.pdf "Enemy Strategy Prediction Algorithm")

Dynamic army prediction is a very interesting problem to solve because, to our
knowledge, not many attempts have already been made to solve this specifically.

Most prediction models focus on the overall strategy the enemy will utilize
based on their opening build order, while we want to focus on immediate builds
at any point during the game.

This problem is also technically interesting because it is difficult to
determine the relationships between every unit created as well determine how
these relationships evolve as time progresses within the game.

This requires a large amount of training and implementing approaches, such as
linear regression.

---

## Aspiration

A dynamic army prediction algorithm could ultimately be utilized by gameplay
bots in real games. Since the algorithm was built to observe general features
in StarCraft, instead of being given the tech tree for a specific faction
first, it can be easily trained to predict the actions of opponents in
different factions.


## Plan

To make our methods understandable and approachable, we mainly use linear
regression as a statistical approach to analyze the relationship between every
pair of two units; in order to predict a specific unit, we use its relationship
with all the others. The initial model is less effective as the game
progresses, so we partition the game into ten minute sections that each get
their own linear regression model. We compare this to a Bayesian Model
predicting the opponent’s opening build to determine how our prediction
accuracy compares to other models.

