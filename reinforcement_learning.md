# An Introduction to Reinforcement Learning
Speaker: Jessica Forde
(NOTE TO SELF: WATCH THE VIDEO OF THIS, LATER)
(missed the first few minutes b/c I was in the wrong hall)

## A code example: Markov Decision Processes
Dynamic progremming (the Belmont? equation)

Navigating a maze (grid), w/ reward values on each grid cell.

There's a matrix showing transition probabilities b/w cells.

Uses value iteration to solve for the optimal policy.  Tensor of 3 dimensions: rows, columns, number of actions.

State vs. action

Something about a Q function (I think this is the reward function)

(Aside: this looks like a heat diffusion situation.  Maybe it's just the way this particular problem is formulated-- on a grid.)

### What if you can't do dynamic programming?

How can you estimate Q(s,a) without a modelof those transitions?

SARSA is both model-free and on-policy:
State, Action, Reward, Start, Action

Q = expected value of taking a given action (a) given a specific state (s).

There's an epsilon parameter in here that you exponentially decay over subsequent iterations. (Aside: again, this really sounds like simulated annealing)

Tabular RL problems: lookup table representation, easy to store and interpret, fast at test time.

`OpenAI Gym` <-- this is a package I should look up.
Speaker suggests starting with `cartpole` or `frozen lake` projects/games.

Also: `Universe` <-- can interface with websites

`ParlAI` <-- written in 'dialog`, which is apparently, something that AI people are starting to get excited about.

## Can you solve _your_ problem with reinforcement learning?
+ You must take an action
+ that effects the environment
+ that has reward/hazard associated with it
+ some other thing I missed
^^^ If so, then RL is a good fit.

General tips:
+ parameter setting matters
+ evaluate results across multiple runs

## Resources:
+ Sutton and Barto book
+ Mnih et al


## Audience Questions
Q: Is there a copy of the notebooks you showed on GitHub

A: Yes! (Unreadible from where I sat)

Q: Are there python libraries that doo this?

A: Yes! Look at RL Lab.

Q: How is RL different from agent-based modeling, and when would you use one vs the other?

A: I think it's just a nomenclature difference, actually.  They're basically the same.  There's a lot of overlap.

Q: What happens when the environment doesn't immediately issue a reward?

A: Long term planning is an important problem, and we're still figuring out the best way to do it.  It's still an open question.

