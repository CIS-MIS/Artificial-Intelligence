# Homework 05: Adversarial Search and Game Playing

**Chapter:** 8 (Adversarial Search)
**Related background:** Chapters 2 (utility-based agents), 5 (heuristic evaluation), 7 (beyond classical search)
**Estimated time:** 2–3 hours
**Total points:** 100

---

## Instructions

Answer all questions thoroughly. For minimax and alpha-beta traces, show the backed-up values at each node and clearly indicate which branches are pruned. Submissions should be typed, with question numbers clearly labeled.

---

## Question 1: Games as Adversarial Search (15 points)

(a) Explain why games are natural adversarial search problems. Define the roles of MAX and MIN, and state the zero-sum assumption. (6 points)

(b) List four reasons why games are valuable AI research domains (e.g., clear objectives, measurable results). (6 points)

(c) Name one game in which AI has achieved superhuman performance, and state approximately when this occurred (e.g., Deep Blue vs. Kasparov, 1997; AlphaGo vs. Lee Sedol, 2016). (3 points)

---

## Question 2: Game Trees (15 points)

(a) Define the following terms in the context of a game tree: state, action (move), branch, node, terminal state. (5 points)

(b) Draw (or describe) a two-ply game tree for a simple game: MAX at the root has two moves (A and B). After move A, MIN has two responses leading to terminal values +1 and 0. After move B, MIN has two responses leading to terminal values −1 and 0. Label all nodes and terminal values. (5 points)

(c) Given the tree in part (b), what is the minimax value at the root, and which move should MAX choose? (5 points)

---

## Question 3: Minimax (20 points)

(a) Describe the minimax algorithm recursively: how values are computed at MAX nodes, MIN nodes, and terminal nodes. (8 points)

(b) State the time and space complexity of minimax in terms of branching factor b and depth m (number of plies). (4 points)

(c) Why is minimax optimal but impractical for games like chess and Go? Give approximate state-space sizes for chess and Go. (6 points)

(d) What does it mean for a game to be "solved"? Is tic-tac-toe solved, and if so, what is the outcome with optimal play by both sides? (6 points)

---

## Question 4: Minimax Trace (10 points)

Consider a three-level tree: MAX at root (level 0), MIN at level 1, MAX at level 2, terminal values at level 3.

- Root MAX has two children: N1 and N2
- N1 (MIN) has children with terminal values: 3, 5
- N2 (MIN) has children with terminal values: 2, 9

Compute the minimax value at the root using bottom-up propagation. Show the value at each node and the final move MAX should choose. (10 points)

---

## Question 5: Alpha-Beta Pruning (20 points)

(a) Explain how alpha-beta pruning works. Define alpha (α) and beta (β), and state the pruning rule at MIN nodes and at MAX nodes. (8 points)

(b) Does alpha-beta pruning change the minimax value at the root? Explain why or why not. (4 points)

(c) How does move ordering affect the effectiveness of alpha-beta pruning? Contrast ideal ordering with worst ordering. (4 points)

(d) In the best case (ideal move ordering), what is the effective branching factor of alpha-beta, and what does this mean for search depth? (4 points)

---

## Question 6: Heuristic Evaluation and Cutoff Search (10 points)

(a) For complex games, exhaustive search to terminal states is infeasible. What is cutoff search, and what role does a heuristic evaluation function play? (5 points)

(b) Give an example of a heuristic evaluation function for chess (e.g., material count plus positional factors). (5 points)

---

## Question 7: Monte Carlo Tree Search (10 points)

(a) Describe the four phases of Monte Carlo Tree Search (MCTS): selection, expansion, simulation, backpropagation. (6 points)

(b) How does MCTS differ from minimax? In particular, does MCTS require a heuristic evaluation function? Explain. (4 points)

---

## Question 8: AlphaGo and Learning + Search (10 points)

(a) Briefly describe how AlphaGo combined neural networks with MCTS. What did the policy network estimate, and what did the value network estimate? (6 points)

(b) Name one limitation of minimax when applied to games with imperfect information (e.g., poker), and name one method used to address imperfect-information games. (4 points)

---

## Grading Rubric

| Question        | Points        |
| --------------- | ------------- |
| 1               | 15            |
| 2               | 15            |
| 3               | 20            |
| 4               | 10            |
| 5               | 20            |
| 6               | 10            |
| 7               | 10            |
| 8               | 10            |
| **Total** | **100** |

---

## Suggested Length

A complete submission is approximately 5–7 pages, including game-tree diagrams and traces.
