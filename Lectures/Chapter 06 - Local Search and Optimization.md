# Artificial Intelligence - Chapter 6: Local Search and Optimization

## Lecture Note Slides (20 Slides)

**Source Materials:** AI - Chapter 6 (textbook); AI Lecture Notes 06 (Unsupervised Learning, K-Means, Representation Learning); AI Lecture Notes 13 (Building a Game-Playing AI with Neural Networks and Genetic Algorithms)

---

## Slide 1 - Local Search and Optimization

**Local Search and Optimization: Hill Climbing, Simulated Annealing, Genetic Algorithms, and Beyond**

Chapter 6 - Local Search and Optimization

A scholarly treatment of optimization methods that operate in the space of complete states rather than paths, including local search, stochastic methods, and evolutionary computation.

---

## Slide 2 - From Path Search to State-Space Optimization

Chapters 3-5 treated search as finding a path from an initial state to a goal state. Chapter 6 shifts perspective:

**Path search (Chapters 3-5):** The path to the goal matters; the algorithm explores a tree/graph of partial solutions.

**Local search (Chapter 6):** The path is irrelevant; only the final state matters. The algorithm operates on complete states, moving from one state to a neighboring state in a local neighborhood.

This shift is appropriate for optimization problems:

- VLSI layout: arrange components on a chip to minimize wire length
- Airline scheduling: assign crews and planes to flights to minimize cost
- Network design: configure routers to minimize latency

For such problems, any solution state is acceptable; the objective is to find the best state according to an objective function.

Local search advantages:

- Constant memory: only the current state and a few neighbors need storing
- Applicable to enormous or continuous state spaces where tree search is impossible
- Often finds good (if not optimal) solutions quickly

---

## Slide 3 - The Local Search Landscape

Local search operates on a **state space landscape** where:

- Each point is a complete state
- Elevation is the value of an objective function (higher = better for maximization, lower = better for minimization)
- The algorithm moves between neighboring states

Key concepts:

- **Neighborhood:** The set of states reachable from a state by one application of an operator
- **Objective function:** The function being optimized (also called the evaluation function or fitness function)
- **Global maximum/minimum:** The best state in the entire landscape
- **Local maximum/minimum:** A state better than all its neighbors but not globally optimal
- **Plateau / flat region:** A region where many neighboring states have equal objective value
- **Ridge:** A narrow path of high-quality states leading to a peak

The landscape metaphor explains why local search can fail: an algorithm on a hill may reach a local peak and be unable to discover a higher peak elsewhere.

---

## Slide 4 - Hill Climbing

Hill climbing is the simplest local search algorithm:

1. Start from a randomly generated state
2. Repeatedly move to the best neighboring state (steepest-ascent hill climbing) or any better neighbor (first-choice hill climbing)
3. Stop when no neighbor improves the objective

Variants:

- **Steepest-ascent:** Evaluate all neighbors; move to the best one
- **First-choice:** Generate neighbors randomly; move to the first one better than current
- **Random-restart:** Run hill climbing from many random starting points; keep the best result found

Properties:

- **Complete:** No - may get stuck at local maxima, plateaus, or ridges
- **Optimal:** No - finds a local optimum, not necessarily global
- **Time:** Depends on landscape and starting point
- **Space:** O(1) - constant, only stores current state

Hill climbing is often described as "climbing Everest in a fog with amnesia": you know whether a step goes up, but not where the highest peak is or where you've been.

---

## Slide 5 - Limitations of Hill Climbing

Hill climbing fails in three landscape conditions:

**Local Maxima:** A peak higher than all neighbors but lower than the global peak. The algorithm stops because no neighbor improves, even though better states exist elsewhere.

**Plateaus:** Flat regions where all neighbors have equal value. The algorithm has no direction to move and may wander aimlessly.

**Ridges:** Narrow sequences of high states where movement requires two steps in sequence (e.g., north then east), but neither individual step improves the objective. Hill climbing sees no improving move and stops.

Random-restart hill climbing mitigates local maxima by trying multiple starting points, but plateaus and ridges remain problematic without more sophisticated mechanisms.

---

## Slide 6 - Simulated Annealing

Simulated annealing (SA) escapes local maxima by occasionally accepting worse moves. Inspired by annealing in metallurgy (heating metal then slowly cooling to reduce defects):

1. Start from a random state and a high "temperature" T
2. Repeatedly:
   - Pick a random neighbor
   - If the neighbor improves the objective, move to it
   - If the neighbor is worse, move to it with probability e^(ΔE/T), where ΔE is the objective change (negative for worse moves) and T is current temperature
3. Gradually reduce T according to a cooling schedule
4. Stop when T is near zero

Properties:

- **Complete:** Yes, with an appropriate slow cooling schedule (theoretically)
- **Optimal:** Yes, asymptotically, with sufficiently slow cooling
- In practice: T must decrease slowly enough to allow exploration but fast enough to terminate in reasonable time

At high T, the algorithm behaves like a random walk (exploration). At low T, it behaves like hill climbing (exploitation). The gradual cooling balances both.

---

## Slide 7 - Exploration vs. Exploitation in Local Search

The exploration-exploitation tension, central to local search:

**Exploitation:** Refine the current good solution by making small improving moves. Hill climbing is pure exploitation.

**Exploration:** Try unfamiliar states that may be worse in the short term but lead to better regions. Simulated annealing's uphill moves and random restarts are exploration.

Text Note 09 (Reinforcement Learning) frames this identically for RL agents:

- Exploitation: use known successful strategies for immediate reward
- Exploration: try unfamiliar actions to discover better strategies
- Balance determines long-term performance

Text Note 13 (Genetic Algorithms) frames it as mutation vs. selection:

- Selection preserves successful behaviors (exploitation)
- Mutation introduces variation to explore new configurations (exploration)

The right balance depends on landscape structure, time budget, and solution quality requirements.

---

## Slide 8 - Local Beam Search

Local beam search runs k parallel hill-climbing searches from k different starting states:

1. Generate k random initial states
2. At each step, generate all successors of all k states
3. Select the k best successors (by objective value) as the new set
4. Repeat until a goal is found or no improvement

Unlike random-restart hill climbing (independent searches), beam search shares information: the best k states across all searches survive, focusing computation on promising regions.

**Stochastic beam search** adds randomness: successors are chosen with probability proportional to their objective value, preventing the population from collapsing onto a single state too quickly.

Properties:

- More memory than hill climbing (O(k)) but explores multiple regions
- Can still miss the global optimum if all k beams start in poor regions
- Related to population-based methods in evolutionary computation

---

## Slide 9 - Genetic Algorithms

Genetic algorithms (GAs) are population-based optimization methods inspired by biological evolution. A GA operates on a population of candidate solutions (individuals), each encoded as a string (chromosome) of values (genes).

**Basic GA cycle:**

1. **Initialize** a population of random individuals
2. **Evaluate** each individual's fitness using a fitness function
3. **Select** the fittest individuals for reproduction
4. **Recombine (crossover)** pairs of individuals to create offspring
5. **Mutate** offspring by randomly altering some genes
6. **Replace** the population with offspring (optionally retaining elites)
7. Repeat until a termination condition

Key terms:

- **Population:** Set of candidate solutions
- **Fitness:** Objective value measuring solution quality
- **Selection:** Choosing fitter individuals to reproduce
- **Crossover:** Combining genes from two parents
- **Mutation:** Randomly altering genes to introduce variation
- **Generation:** One cycle of evaluation and reproduction
- **Elitism:** Preserving the best individuals unchanged across generations

Text Note 13 (TrashBlaster) provides a concrete GA application: evolving neural network weights for a game-playing AI.

---

## Slide 10 - Genetic Algorithm Example: TrashBlaster Fitness Function

Text Note 13 describes a game-playing AI (TrashBlaster) evolved via GA:

**Fitness function:**
Fitness = (1 × Seconds Alive) + (10 × Trash Destroyed) - (2 × Blasts Fired)

**GA configuration:**

- Population: 200 neural networks
- Selection: Top 100 models retained
- Cloning: 100 selected models copied
- Mutation: 5% chance per weight changed by a random amount
- Next generation: 100 unmutated originals + 100 mutated copies
- Parallel evaluation: 200 game simulations run simultaneously

**Fitness design matters:** The AI optimizes exactly what the fitness function rewards:

- Reward only survival → AI hides forever without shooting
- Reward only destruction → AI fires constantly, taking risks
- Balanced fitness → AI survives while destroying trash

This illustrates that optimization methods find the optimum of the given objective - not necessarily the intended behavior.

---

## Slide 11 - Genetic Operators: Crossover and Mutation

**Crossover (recombination):** Combines genetic material from two parents to create offspring. Common forms:

- **One-point crossover:** Choose a crossover point; offspring gets first part from parent A, rest from parent B
- **Two-point crossover:** Swap the middle segment between two points
- **Uniform crossover:** Each gene independently chosen from one of the two parents

Crossover exploits building blocks: if parent A has a good partial solution and parent B has another, crossover may combine them into a superior offspring.

**Mutation:** Randomly alters individual genes with a low probability (e.g., 1-5%). Mutation:

- Introduces new genetic material not present in the population
- Prevents premature convergence (population becoming too similar)
- Acts as a background exploration mechanism

Mutation rate and magnitude must be balanced: too high disrupts good solutions; too low limits exploration.

---

## Slide 12 - Fitness Function Design

The fitness function defines the optimization objective and therefore determines what the GA learns. Design considerations:

1. **Alignment with the true goal:** Fitness should correlate with desired behavior
2. **Multiple objectives:** Combine terms with weights (survival + destruction - shooting penalty)
3. **Gradient:** Fitness should provide useful gradients - small improvements should yield measurable fitness changes
4. **Avoiding deception:** Fitness should not reward behavior that scores well but fails the real objective

Text Note 13 warns: "An AI can only optimize the objective it is given. A poorly designed fitness function can lead to unexpected or undesirable behavior."

This is closely related to reward design in reinforcement learning (Text Note 09) and objective specification in AI safety (Text Note 14).

---

## Slide 13 - Limitations of Genetic Algorithms

GAs are powerful but have well-known limitations:

1. **Randomness:** Mutation is stochastic; no guarantee of improvement in any generation
2. **Computational cost:** Every individual must be evaluated; large populations and generations are expensive
3. **Large search spaces:** As representations grow, the number of possible combinations explodes; random mutation may not find good solutions
4. **Premature convergence:** The population may become too similar, losing diversity needed to discover new strategies
5. **Fitness function problems:** Poorly designed fitness yields unintended behavior
6. **Inconsistent performance:** High fitness in one generation may reflect luck rather than reliable strategy

Possible mitigations: adjust population size, mutation rate/magnitude, preserve diversity, evaluate over multiple games, improve fitness function, use more advanced evolutionary strategies.

---

## Slide 14 - Local Search in Machine Learning Applications

Local search and optimization appear throughout machine learning:

**Neural network training (Text Notes 03-05):**

- Gradient descent is a form of local search in weight space
- Backpropagation computes gradients; gradient descent follows them downward in loss landscape
- Mini-batch training, learning rate schedules, and adaptive optimizers (Adam, RMSprop) address local minima and saddle points

**Clustering (Text Note 06):**

- K-means alternates between assigning points to nearest centroids and recomputing centroids - a local search that monotonically reduces within-cluster variance
- Initial centroids affect results; multiple restarts recommended

**Feature selection:**

- Forward/backward selection searches feature subsets to optimize predictive performance

**Hyperparameter tuning:**

- Grid search, random search, and Bayesian optimization search hyperparameter space

---

## Slide 15 - Continuous vs. Discrete Optimization

Local search naturally handles both:

**Discrete spaces:** States are combinatorial (e.g., 8-puzzle, VLSI layout, feature subsets). Neighbors differ by a small discrete change.

**Continuous spaces:** States are vectors in Rⁿ (e.g., neural network weights, control parameters). Neighborhood is defined by small perturbations (e.g., add Gaussian noise). Gradient-based methods (gradient descent) dominate continuous optimization because they use derivative information to choose descent directions efficiently.

Gradient descent update:
w_new = w_old - η × ∇L(w)

where η is the learning rate and ∇L is the loss gradient. This is local search guided by exact slope information - far more efficient than blind perturbation in high-dimensional continuous spaces.

Text Notes 04-05 detail gradient descent and backpropagation for neural network training.

---

## Slide 16 - Local Search in Robotics and Control

Local search is also central to robotics and control. Text Note 11 (Robotics) describes how a robot uses local optimization to refine its path and grasp: given a planned trajectory, the robot continuously adjusts joint torques and end-effector position based on sensor feedback to minimize tracking error.

This is local search in continuous state space: the current robot configuration is the state, small adjustments are neighbors, and the objective is task success (e.g., grasp the object, follow the path). Closed-loop control is local search executed at high frequency, where the landscape changes as the robot and objects move.

---

## Slide 17 - When Local Search Succeeds and Fails

Local search succeeds when the landscape has few deep local maxima, good heuristics exist for neighbor selection, and a good-enough solution suffices. It works well for VLSI layout, scheduling, and neural network training.

Local search fails when:

- The landscape is riddled with local maxima close in quality to the global optimum
- The global optimum is in a narrow basin hard to stumble upon
- Exact optimality is required (local search gives no guarantees)
- The objective is discontinuous or noisy (no reliable gradient or neighbor ordering)

In such cases, global methods (branch and bound, dynamic programming) or population methods with strong diversity preservation are preferable.

---

## Slide 18 - Local Search and the Bias-Variance Trade-Off

Local search illustrates the bias-variance trade-off in a different form. A greedy hill climber has high bias: it commits quickly to the nearest peak and may miss the global optimum (underfitting the landscape). A random-restart or simulated-annealing search with many restarts has high variance: it explores widely but may never settle, wasting computation (overfitting to noise in the landscape).

The temperature schedule in simulated annealing and the number of restarts in hill climbing are the knobs that control this trade-off. A slow cooling schedule and many restarts reduce bias (more exploration) but increase computation; a fast schedule and few restarts reduce computation but increase the risk of settling for a local optimum. As with supervised learning (Chapter 15), the right setting depends on the problem and the available budget.

---

## Slide 19 - Summary: Key Takeaways

1. Local search optimizes over complete states rather than paths; only the final state matters
2. The state-space landscape has peaks (optima), valleys, plateaus, and ridges that determine algorithm behavior
3. Hill climbing moves to the best neighbor but can get stuck at local maxima, plateaus, and ridges
4. Simulated annealing escapes local optima by probabilistically accepting worse moves, with temperature gradually reduced
5. Exploration (trying new regions) and exploitation (refining current solutions) must be balanced
6. Local beam search maintains k states in parallel, focusing search on promising regions
7. Genetic algorithms evolve populations via selection, crossover, and mutation, inspired by biological evolution
8. The fitness function determines what the GA optimizes - design it carefully to match intended behavior
9. GAs can suffer from randomness, computational cost, large search spaces, premature convergence, and fitness-function problems
10. Local search underlies neural network training (gradient descent), K-means clustering, robotics control, and many ML optimization tasks

---

## Slide 20 - Review Questions

1. How does local search differ from path-finding search (Chapters 3-5)?
2. Draw or describe a state-space landscape with local maximum, plateau, and ridge. Explain why each defeats hill climbing.
3. Trace one iteration of steepest-ascent hill climbing on a small example.
4. How does simulated annealing decide whether to accept a worse neighbor, and what role does temperature play?
5. Contrast exploration and exploitation. Name one local-search mechanism for each.
6. How does local beam search differ from random-restart hill climbing?
7. Describe the genetic algorithm cycle and define: population, fitness, selection, crossover, mutation, elitism.
8. Analyze the TrashBlaster fitness function: what behavior does each term encourage?
9. What could go wrong if the GA mutation rate is too high? Too low?
10. How is gradient descent a form of local search, and why is it more effective than blind perturbation in neural network training?
