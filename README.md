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
#### Problem

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

[https://hal.archives-ouvertes.fr/hal-00607277/file/OpeningPrediction.pdf](https://hal.archives-ouvertes.fr/hal-00607277/file/OpeningPrediction.pdf "Enemy Strategy Prediction Algorithm")

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

#### Possible AI Approaches

A possible AI approach to this problem is creating a neural network to learn
relationships between all the units created during different periods of the
game.
A neural network would not only allow us to find linear relationships, but also
more complex higher order relationships between units.
However, creating a neural network wouldn’t be feasible for this project
because of the large data sets and extensive training they require.
Another problem with using a neural network is its “black box” nature, where
it’s unclear how and why a prediction was determined given certain input,
making the logic hard to follow and evaluate.
Another solution is creating a Bayesian network where each node, which in this
case would be unit type, would have a probability associated with it depending
on how far into the game the player was, to determine what units were most
likely to be created next.
This method would work better than the neural network, as they are less
sensitive to smaller data sets and are more resistant to overfitting the data,
therefore making them more efficient in rapidly changing environments such as
StarCraft II.
However, a Bayesian network would also be a difficult approach for our project
because determining the conditional probabilities between nodes requires a
large amount of training and computational power, neither of which we can
accurately do within our timeframe.

#### Design and Technical Approach

We propose using Linear Regression or some other statistical model to predict
the amounts of complementing units over time.
For instance, Mutalisks and Zerglings are commonly used together, so we will
form a regression model which predicts their exact correlation.
In addition, we plan to use another model to dynamically predict the enemy’s
army composition from the available data (obtained by scouting).
In general, Linear Regression is effective for highly correlated data members.
Thus, we believe using it for selected complementary units would result in
accurate predictions of future unit builds.
However, it may fall short in dynamic army prediction, since game unit
compositions vary more widely during the later parts of the game.
For instance, predicting based on buildings would be ineffective because both
players are likely to have all of the buildings; late game scenarios diverge
from generic build orders, creating a much larger problem space.
As later in the game, a single model’s accuracy would decrease significantly,
we propose using several separately calibrated models for the different
partitions of game time.
For example, minute 0-10, 10-20, 20-30 would have their own unique linear
regression models for each unit pair.
The partition boundaries may vary as we experiment with different partition
sizes.

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

