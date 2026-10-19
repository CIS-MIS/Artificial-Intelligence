# Homework 03: Informed (Heuristic) Search

**Chapter:** 5 (Informed Search Strategies)
**Related background:** Chapters 3–4 (problem formulation, uninformed search)
**Estimated time:** 2–3 hours
**Total points:** 100

---

## Instructions

Answer all questions thoroughly. For proofs and derivations, show each step. For search-trace questions, show frontier contents and f(n) = g(n) + h(n) values. Submissions should be typed, with question numbers clearly labeled.

---

## Question 1: Heuristic Functions (15 points)

(a) Define a heuristic function h(n) for a search problem. What must be true of h(n) when n is a goal state? (5 points)

(b) Explain the difference between informed search and uninformed search. Give one example of a domain where a good heuristic is readily available and one where it is difficult to construct. (5 points)

(c) Define the effective branching factor b*. If A* expands 1,000 nodes to find a goal at depth d = 8, approximately what is b*? (You may solve numerically or by trial and error.) Show your work. (5 points)

---

## Question 2: Greedy Best-First vs. A* (15 points)

(a) Write the evaluation functions for greedy best-first search and for A* search. Explain the role of each term (g(n), h(n), f(n)). (5 points)

(b) Is greedy best-first search complete? Is it optimal? Justify each answer with a one-sentence explanation or a counterexample. (5 points)

(c) Construct a tiny example (3–4 nodes) in which greedy best-first search chooses a different first move than A*, and briefly explain why. (5 points)

---

## Question 3: Admissibility and Consistency (20 points)

(a) State the admissibility condition for a heuristic. Explain why an admissible heuristic guarantees that A* is optimal. (6 points)

(b) State the consistency (monotonicity) condition. Explain how consistency is stronger than admissibility: every consistent heuristic is admissible, but not vice versa. (6 points)

(c) What implementation benefit does a consistent heuristic provide for A* using graph search? (4 points)

(d) Is it possible for a heuristic to be admissible but not consistent? If yes, give a brief conceptual example; if no, explain why not. (4 points)

---

## Question 4: Dominance of Heuristics (10 points)

Suppose h₁ and h₂ are both admissible heuristics for the same problem, and h₂(n) ≥ h₁(n) for all nodes n.

(a) What does it mean to say that h₂ dominates h₁? (3 points)

(b) If h₂ dominates h₁ and both are admissible, which heuristic causes A* to expand fewer nodes (typically), and why? (4 points)

(c) Is dominance alone sufficient to guarantee that h₂ is admissible? Explain. (3 points)

---

## Question 5: Constructing Admissible Heuristics (15 points)

(a) Explain the relaxed-problem method for constructing admissible heuristics. Why is the optimal cost of a relaxed problem an admissible heuristic for the original problem? (6 points)

(b) For the 8-puzzle, compare two heuristics: (i) number of misplaced tiles, and (ii) Manhattan distance. Show that Manhattan distance dominates misplaced tiles by explaining how each misplaced tile contributes to both measures. (6 points)

(c) Describe how pattern databases are used to build strong heuristics for the 15-puzzle. (3 points)

---

## Question 6: A* Trace (15 points)

Consider the following search space. The initial state is S, the goal is G. Edge costs are shown; heuristic values h(n) are shown in parentheses next to each node.

- S (h=8): neighbors A (cost 2, h=6), B (cost 4, h=4)
- A (h=6): neighbors C (cost 3, h=4), D (cost 2, h=5)
- B (h=4): neighbors D (cost 1, h=5), E (cost 5, h=0) [E is goal]
- C (h=4): neighbor G (cost 4, h=0) [G is goal]
- D (h=5): neighbor G (cost 1, h=0) [G is goal]
- E is goal; G is goal

Trace A* search step by step. For each expansion, show:

- The node selected from the frontier
- Its f(n) = g(n) + h(n)
- The successor nodes added to the frontier with their g, h, and f values

Stop when a goal node is selected for expansion (i.e., popped from the frontier). Which goal is found, and what is the total cost of the solution path? Is it optimal? (15 points)

---

## Question 7: Memory-Bounded Variants (10 points)

(a) Why does standard A* require O(b^d) space, and why can this be prohibitive? (5 points)

(b) Briefly describe how Iterative Deepening A* (IDA*) bounds memory. What is the trade-off compared to standard A*? (5 points)

---

## Question 8: Limitations of Heuristic Search (5 points)

Name two limitations of heuristic search (beyond "heuristics are hard to design"). For each, give a one-sentence example of a situation in which the limitation arises. (5 points)

---

## Grading Rubric

| Question        | Points        |
| --------------- | ------------- |
| 1               | 15            |
| 2               | 15            |
| 3               | 20            |
| 4               | 10            |
| 5               | 15            |
| 6               | 15            |
| 7               | 10            |
| 8               | 5             |
| **Total** | **100** |

---

## Suggested Length

A complete submission is approximately 5–7 pages, including search traces and derivations.
