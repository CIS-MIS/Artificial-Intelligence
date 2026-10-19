# Homework 04: Local Search and Optimization

**Chapter:** 6 (Local Search and Optimization)
**Related background:** Chapter 2 (utility-based agents), Chapter 9 (learning context)
**Estimated time:** 2–3 hours
**Total points:** 100

---

## Instructions

Answer all questions thoroughly. For trace questions, show the current state, neighbor evaluations, and decisions at each step. For essay questions, use complete sentences and justify your claims. Submissions should be typed, with question numbers clearly labeled.

---

## Question 1: Local Search vs. Path Search (15 points)

(a) Explain the fundamental difference between local search (Chapter 6) and path-finding search (Chapters 3–5). In particular, state what matters in each approach: the path, the final state, or both. (6 points)

(b) Give two examples of optimization problems for which local search is appropriate, and explain why path-finding search would be unnatural or infeasible for each. (6 points)

(c) List three advantages of local search over tree/graph search. (3 points)

---

## Question 2: The State-Space Landscape (15 points)

Define each of the following terms in the context of a state-space landscape: (i) global maximum, (ii) local maximum, (iii) plateau (flat region), (iv) ridge. For each, give a one-sentence example of how it could arise in a real optimization problem (e.g., VLSI layout, scheduling, neural network training). (15 points)

---

## Question 3: Hill Climbing (20 points)

(a) Describe the hill-climbing algorithm. Distinguish between steepest-ascent hill climbing and first-choice hill climbing. (8 points)

(b) Hill climbing can fail because of local maxima, plateaus, and ridges. For each failure mode, explain (i) what it is and (ii) why hill climbing stops or struggles. (9 points)

(c) How does random-restart hill climbing address local maxima? What limitation of random-restart hill climbing remains with respect to plateaus and ridges? (3 points)

---

## Question 4: Simulated Annealing (20 points)

(a) Describe simulated annealing. Include the acceptance rule for a worse neighbor: if ΔE is the change in the objective (negative for worse moves) and T is temperature, with what probability is a worse move accepted? (7 points)

(b) Explain the role of temperature T and the cooling schedule. What happens at high T? At low T? Why must T decrease slowly enough for the algorithm to be asymptotically optimal? (8 points)

(c) Compare simulated annealing to hill climbing in terms of exploration versus exploitation. (5 points)

---

## Question 5: Local Beam Search and Genetic Algorithms (15 points)

(a) Describe local beam search. How does it differ from random-restart hill climbing? (6 points)

(b) Describe the genetic algorithm cycle: initialization, evaluation, selection, crossover, mutation, replacement. Define each term. (6 points)

(c) What is elitism in a genetic algorithm, and why might it be used? (3 points)

---

## Question 6: Fitness Function Design (10 points)

The fitness function defines exactly what a genetic algorithm optimizes. Consider the TrashBlaster example from the lecture notes:

Fitness = (1 × Seconds Alive) + (10 × Trash Destroyed) − (2 × Blasts Fired)

(a) What behavior does each term of this fitness function encourage? (5 points)

(b) Suppose you removed the "− (2 × Blasts Fired)" term. How might the AI's behavior change, and why might this be undesirable? (5 points)

---

## Question 7: Limitations of Genetic Algorithms (10 points)

List and briefly explain four limitations of genetic algorithms (e.g., randomness, computational cost, large search spaces, premature convergence, fitness-function problems, inconsistent performance). For one limitation of your choice, suggest a possible mitigation. (10 points)

---

## Question 8: Local Search in Machine Learning (5 points)

Explain how gradient descent is a form of local search in continuous weight space. Why is gradient descent more effective than blind perturbation (random mutation) for training neural networks? (5 points)

---

## Grading Rubric

| Question        | Points        |
| --------------- | ------------- |
| 1               | 15            |
| 2               | 15            |
| 3               | 20            |
| 4               | 20            |
| 5               | 15            |
| 6               | 10            |
| 7               | 10            |
| 8               | 5             |
| **Total** | **100** |

---

## Suggested Length

A complete submission is approximately 4–6 pages, depending on formatting and whether traces are included.
