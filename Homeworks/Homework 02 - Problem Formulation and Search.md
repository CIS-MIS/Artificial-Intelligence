# Homework 02: Problem Formulation and Uninformed Search

**Chapters:** 3 (Solving Problems by Searching) and 4 (Uninformed Search Strategies)
**Estimated time:** 2–3 hours
**Total points:** 100

---

## Instructions

Answer all questions thoroughly. For search-trace questions, show the frontier contents and node expansions step by step. For complexity questions, define any variables you use (e.g., b, d, m, l). Submissions should be typed, with question numbers clearly labeled.

---

## Question 1: Problem Formulation (20 points)

Formulate each of the following as a search problem by specifying: (i) the initial state, (ii) the set of actions, (iii) the transition model, (iv) the goal test, and (v) the path-cost function. You may make reasonable simplifying assumptions, but state them explicitly.

(a) A robot must navigate from its current room to a charging station in an office building, avoiding occupied rooms. (7 points)

(b) The 8-puzzle (3x3 sliding-tile puzzle) with numbered tiles 1–8 and one blank space. (6 points)

(c) A traveling salesperson must visit five cities and return to the starting city, minimizing total distance. (7 points)

---

## Question 2: State Spaces and Search Trees (15 points)

(a) Explain the difference between a state, a state space, and a search tree. Use a small example (different from the ones in the lecture notes) to illustrate. (7 points)

(b) The 8-puzzle has 9!/2 = 181,440 reachable states. Explain why only half of the 9! possible arrangements are reachable from any given initial state. (8 points)

---

## Question 3: Tree Search vs. Graph Search (15 points)

(a) Describe the difference between tree search and graph search. Why is an explored set (closed list) necessary in graph search? (8 points)

(b) Give an example of a state space containing a loop (a cycle of actions that returns to a previously visited state). Show how tree search could fail to terminate on this space, while graph search would terminate. (7 points)

---

## Question 4: Search Strategy Evaluation (15 points)

Complete the following table for the uninformed search strategies. Use b = branching factor, d = depth of shallowest goal, m = maximum depth, l = depth limit, and C* = cost of optimal solution.

| Strategy            | Complete? | Optimal? | Time Complexity | Space Complexity |
| ------------------- | --------- | -------- | --------------- | ---------------- |
| Breadth-First       |           |          |                 |                  |
| Uniform-Cost        |           |          |                 |                  |
| Depth-First         |           |          |                 |                  |
| Depth-Limited       |           |          |                 |                  |
| Iterative Deepening |           |          |                 |                  |
| Bidirectional       |           |          |                 |                  |

After completing the table, answer: which single strategy offers the best compromise between completeness, optimality, and memory usage when solution depth is unknown? Justify your answer in 2–3 sentences. (15 points total)

---

## Question 5: Breadth-First Search Trace (15 points)

Consider the following small state space. The initial state is A, and the goal is G. Each action has a cost of 1. The branching structure is:

- From A: B, C
- From B: D, E
- From C: F
- From D: G
- From E: G
- From F: (no outgoing edges)
- From G: (goal, no expansion needed)

Trace breadth-first search step by step. For each iteration, show:

- The node selected for expansion
- The nodes added to the frontier
- Whether the goal test succeeds

Stop when the goal is found. Is the solution found by BFS optimal? Why or why not? (15 points)

---

## Question 6: Iterative Deepening Depth-First Search (IDDFS) (10 points)

(a) Why is IDDFS time-efficient despite re-expanding nodes across iterations? Use the geometric-series intuition: nodes at depth d are expanded once, nodes at depth d−1 twice, etc. Show that the total number of node expansions is approximately b/(b−1) times the number of nodes at depth d, where b is the branching factor. (5 points)

(b) What is the space complexity of IDDFS, and why is this an advantage over breadth-first search? (5 points)

---

## Question 7: Bidirectional Search (10 points)

(a) State the three conditions required for bidirectional search to be applicable. (6 points)

(b) If a unidirectional search explores O(b^d) nodes and a bidirectional search meets in the middle, approximately how many nodes does bidirectional search explore (in big-O notation)? Explain the intuition. (4 points)

---

## Grading Rubric

| Question        | Points        |
| --------------- | ------------- |
| 1               | 20            |
| 2               | 15            |
| 3               | 15            |
| 4               | 15            |
| 5               | 15            |
| 6               | 10            |
| 7               | 10            |
| **Total** | **100** |

---

## Suggested Length

A complete submission is approximately 5–7 pages, depending on whether search traces are presented as tables or diagrams.
