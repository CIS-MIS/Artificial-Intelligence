# Artificial Intelligence - Chapter 4: Uninformed Search Strategies

## Lecture Note Slides (20 Slides)

**Source Materials:** AI - Chapter 4 (textbook); AI Lecture Notes 17 (Search Engines and Knowledge Bases)

---

## Slide 1 - Uninformed Search Strategies

**Uninformed Search Strategies: Breadth-First, Uniform-Cost, Depth-First, and Beyond**

Chapter 4 - Uninformed Search Strategies

A scholarly treatment of blind search methods that explore state spaces using only problem definitions, without domain-specific heuristics.

---

## Slide 2 - What Is Uninformed Search?

Uninformed (or blind) search strategies have no additional information about states beyond the problem definition itself. They can distinguish a goal state from a non-goal state but have no guidance about which non-goal states are more promising.

Available information:

- The initial state
- The set of legal actions and the transition model
- The goal test
- The path cost function

Uninformed strategies differ only in **which node to expand next** from the frontier. They are universally applicable but can be inefficient on large state spaces.

Chapter 4 covers six strategies:

1. Breadth-First Search (BFS)
2. Uniform-Cost Search (UCS)
3. Depth-First Search (DFS)
4. Depth-Limited Search (DLS)
5. Iterative Deepening Depth-First Search (IDDFS)
6. Bidirectional Search

---

## Slide 3 - Breadth-First Search (BFS)

BFS expands the shallowest unexpanded node first. The frontier is implemented as a FIFO (first-in, first-out) queue.

Properties:

- **Complete:** Yes (if branching factor b is finite)
- **Optimal:** Yes, if all step costs are equal (finds shallowest goal)
- **Time complexity:** O(b^(d+1)) where d is the depth of the shallowest goal
- **Space complexity:** O(b^(d+1)) - must store all nodes at the current depth

BFS is optimal for uniform step costs because it explores all nodes at depth k before any node at depth k+1, so the first goal found is at minimum depth.

Space is usually the limiting factor: BFS must keep an entire level of the tree in memory.

---

## Slide 4 - Uniform-Cost Search (UCS)

UCS generalizes BFS to handle varying step costs. It expands the node with the lowest path cost g(n) from the root. The frontier is a priority queue ordered by g(n).

Properties:

- **Complete:** Yes, if step costs are bounded below by some positive constant ε > 0
- **Optimal:** Yes - finds the lowest-cost solution regardless of step cost variation
- **Time complexity:** O(b^(1 + C*/ε)) where C* is the optimal solution cost
- **Space complexity:** O(b^(1 + C*/ε))

UCS explores nodes in order of increasing path cost, like spreading ripples in all directions equally. When the goal is popped from the frontier, its path cost is guaranteed minimal.

UCS reduces to BFS when all step costs are equal.

---

## Slide 5 - Depth-First Search (DFS)

DFS always expands the deepest unexpanded node first. The frontier is a LIFO (last-in, first-out) stack. DFS follows one branch to its maximum depth before backtracking.

Properties:

- **Complete:** No - fails in infinite-depth state spaces or spaces with loops (can cycle indefinitely)
- **Optimal:** No - finds the first goal it encounters, not necessarily the shallowest or cheapest
- **Time complexity:** O(b^m) where m is the maximum depth of the search space
- **Space complexity:** O(b×m) - linear in depth, only needs to store the path from root to current node plus siblings

DFS is memory-efficient but can get lost in deep or infinite branches. It is suitable when solutions are likely deep and memory is constrained.

---

## Slide 6 - Depth-Limited Search (DLS)

DLS is DFS with a depth limit l. Nodes at depth l are treated as though they have no successors (failure is returned for cutoff nodes).

Properties:

- **Complete:** Yes, if the solution is at depth ≤ l
- **Optimal:** No
- **Time complexity:** O(b^l)
- **Space complexity:** O(b×l)

The depth limit prevents infinite exploration in deep spaces but introduces incompleteness if the shallowest goal lies beyond l. Choosing l is difficult: too small and goals are missed; too large and efficiency is lost.

DLS is useful when prior knowledge bounds solution depth.

---

## Slide 7 - Iterative Deepening Depth-First Search (IDDFS)

IDDFS runs DLS repeatedly with increasing depth limits: l = 0, 1, 2, ... until a goal is found. It combines DFS's space efficiency with BFS's completeness and optimality (for uniform costs).

Properties:

- **Complete:** Yes
- **Optimal:** Yes, if step costs are uniform
- **Time complexity:** O(b^d) - asymptotically optimal despite repeated expansions
- **Space complexity:** O(b×d) - linear in depth

Why is IDDFS efficient despite re-expanding nodes? In a tree with branching factor b, the number of nodes at depth d dominates the total. Nodes at depth d are expanded once, at depth d-1 twice, etc. The geometric series sums to approximately b/(b-1) times the nodes at depth d - a constant factor overhead.

IDDFS is often the preferred uninformed search when solution depth is unknown and memory is limited.

---

## Slide 8 - Bidirectional Search

Bidirectional search runs two simultaneous searches: one forward from the initial state and one backward from the goal, stopping when the frontiers intersect.

Requirements:

- The goal state must be known explicitly (not just a goal test)
- Actions must be reversible (to search backward from the goal)
- Branching factors of both directions must be computable

Properties:

- **Complete:** Yes (with appropriate frontiers)
- **Optimal:** Yes (if both directions use BFS/UCS and meet with appropriate path-cost accounting)
- **Time complexity:** O(b^(d/2)) - dramatically better than O(b^d)
- **Space complexity:** O(b^(d/2))

If both frontiers have branching factor b and meet at depth d/2, each side explores roughly b^(d/2) nodes, for a total of ~2b^(d/2) versus b^d for unidirectional search. This is an exponential improvement.

Bidirectional search is often impractical because the goal may not be a single state or actions may not be reversible.

---

## Slide 9 - Comparing Uninformed Strategies

| Strategy            | Complete         | Optimal            | Time           | Space          |
| ------------------- | ---------------- | ------------------ | -------------- | -------------- |
| Breadth-First       | Yes              | Yes (uniform cost) | O(b^(d+1))     | O(b^(d+1))     |
| Uniform-Cost        | Yes (cost ≥ ε) | Yes                | O(b^(1+C*/ε)) | O(b^(1+C*/ε)) |
| Depth-First         | No               | No                 | O(b^m)         | O(b×m)        |
| Depth-Limited       | Yes (if l ≥ d)  | No                 | O(b^l)         | O(b×l)        |
| Iterative Deepening | Yes              | Yes (uniform cost) | O(b^d)         | O(b×d)        |
| Bidirectional       | Yes              | Yes                | O(b^(d/2))     | O(b^(d/2))     |

Key lessons:

- BFS and UCS guarantee optimality but consume exponential memory
- DFS and DLS are memory-efficient but incomplete/non-optimal
- IDDFS offers the best compromise for uninformed search
- Bidirectional search offers exponential speedup but requires restrictive assumptions

---

## Slide 10 - Avoiding Repeated States

A major source of inefficiency in search is revisiting states via different paths. Three approaches:

1. **Do not return to the state you just came from:** The simplest form of cycle prevention; prevents immediate backtracking.
2. **Do not create paths with cycles:** Track ancestors along the current path; reject any successor already on the path. Prevents infinite loops but allows revisiting states via different paths.
3. **Do not generate any state that was ever generated before:** Maintain a global explored set (graph search). Most effective but requires memory proportional to all visited states.

Graph search (with explored set) is strongly preferred for state spaces with loops. The explored set is typically a hash table keyed by state representation.

---

## Slide 11 - Search in Large State Spaces: A Reality Check

Even IDDFS's O(b^d) time becomes prohibitive for realistic problems:

- Chess: ~10^50 states, b ≈ 35
- Go: ~10^170 states, b ≈ 250
- Rubik's Cube: ~4×10^19 states

Uninformed search cannot enumerate these spaces. This motivates:

- **Informed search** (Chapter 5): Use heuristics to guide expansion order
- **Local search** (Chapter 6): Search in the space of complete states rather than paths
- **Beyond classical search** (Chapter 7): Handle nondeterministic, unobservable, and partially observable environments

Text Note 17 (Search Engines) notes that web search faces a similar scale problem: the web has billions of pages, so search engines use indexes and ranking rather than exhaustive exploration.

---

## Slide 12 - Uninformed Search in Information Retrieval

Text Note 17 connects uninformed search to search engine architecture:

- **Web crawlers** systematically discover pages by following links - a form of breadth-first exploration over the web graph
- **Inverted indexes** organize terms to documents, enabling fast retrieval without scanning every page
- **Ranking algorithms** order candidate results by estimated relevance - an informed process

The crawler's link-following resembles uninformed graph search: it explores reachable pages without knowing which contain relevant content. The index and ranking add informed, knowledge-based pruning and ordering.

This illustrates a broader principle: uninformed methods provide the foundation, but scalable systems require domain-specific structure and heuristics.

---

## Slide 13 - When to Use Uninformed Search

Uninformed search is appropriate when:

- The state space is small enough for exhaustive exploration
- No reliable heuristic is available or domain knowledge is lacking
- Guarantees of completeness or optimality are required
- Memory is sufficient for BFS/UCS, or depth is bounded for DFS/DLS/IDDFS

Uninformed search is inappropriate when:

- The state space is enormous (games, real-world planning)
- A good heuristic can be constructed
- Real-time decisions are required within tight time limits

It serves as a baseline against which informed strategies are measured.

---

## Slide 14 - Step Costs and Optimality

A subtle but critical point: BFS is optimal only when all step costs are equal. When step costs vary:

- BFS finds the shallowest goal, not the cheapest
- UCS finds the cheapest goal regardless of depth

Example: Two paths to a goal

- Path A: 3 steps, each cost 10 → total cost 30
- Path B: 10 steps, each cost 2 → total cost 20

BFS finds Path A (shallower). UCS finds Path B (cheaper). UCS is the correct choice when minimizing total cost matters more than minimizing steps.

When all step costs are equal, UCS and BFS coincide in their expansion order.

---

## Slide 15 - Infinite State Spaces and Failure Modes

Uninformed strategies can fail in infinite state spaces:

- **DFS** may follow an infinite branch and never return to explore other branches - not complete
- **BFS** will eventually find a goal at any finite depth, but may run forever if no goal exists
- **IDDFS** handles infinite spaces gracefully because it systematically increases depth limits; if a goal exists at finite depth, IDDFS finds it

The explored set in graph search may grow without bound in infinite spaces. Practical implementations use memory bounds and pruning.

---

## Slide 16 - Uninformed Search and Agent Design

Uninformed search is most naturally paired with simple reflex or model-based agents operating in fully observable, deterministic, static environments. In such settings, the agent can compute a complete action sequence offline and then execute it without further sensing.

When the environment is only partially observable or nondeterministic, uninformed search over physical states is inadequate: the agent must instead search over belief states or maintain a model that is updated as new percepts arrive. The choice of agent architecture and the choice of search strategy therefore go hand in hand.

---

## Slide 17 - Limitations and the Path to Informed Search

Uninformed search treats every non-goal state as equally promising, which causes it to explore far more of the state space than necessary. It also provides no way to incorporate domain knowledge about which states are likely to lead to the goal.

This limitation motivates informed (heuristic) search, covered in Chapter 5, where a problem-specific heuristic estimates the remaining cost to a goal and orders node expansion accordingly. Informed search can reduce the effective branching factor dramatically, making search feasible in spaces where uninformed search would be intractable.

---

## Slide 18 - Case Study: Uninformed Search in Route Planning

Consider a delivery robot navigating a city grid with known intersections and road segments but no traffic information. Breadth-first search finds the fewest-turn route, while uniform-cost search finds the shortest-distance route if segment lengths are known. Depth-first search might follow a long dead-end street and waste time, illustrating DFS's risk in unknown-depth spaces.

Iterative deepening is often the best practical choice here: it uses little memory (important on a robot) and is guaranteed to find the shortest route in terms of number of segments, matching BFS quality without BFS's memory cost. Bidirectional search could help if both the start and delivery address are fixed, but real deliveries have changing destinations, limiting its use.

---

## Slide 19 - Summary: Key Takeaways

1. Uninformed search uses no domain knowledge beyond the problem definition; strategies differ only in node selection order
2. BFS is complete and optimal for uniform costs but exponential in space
3. UCS handles varying step costs and is optimal, at the cost of priority-queue overhead
4. DFS is memory-efficient (O(b×m)) but incomplete and non-optimal
5. DLS bounds DFS depth to prevent infinite exploration but introduces incompleteness
6. IDDFS combines DFS space efficiency with BFS completeness/optimality at constant-factor time overhead
7. Bidirectional search achieves O(b^(d/2)) time but requires known goals and reversible actions
8. Graph search with an explored set prevents redundant exploration and handles loops
9. Uninformed search scales poorly; real-world problems require informed or local search
10. The choice of strategy depends on state-space size, cost structure, memory limits, and solution-depth knowledge

---

## Slide 20 - Review Questions

1. What information does an uninformed search strategy have available, and what does it lack?
2. Explain why BFS is optimal when step costs are uniform but not when they vary.
3. How does UCS differ from BFS, and what condition guarantees UCS completeness?
4. Why can DFS fail to terminate, and what space advantage does it have over BFS?
5. How does DLS address DFS's non-termination, and what new problem does it introduce?
6. Why is IDDFS time-efficient despite re-expanding nodes across iterations? Show the geometric-series intuition.
7. What three conditions must hold for bidirectional search to be applicable?
8. Compare time and space complexity of unidirectional vs. bidirectional search.
9. What are the three levels of cycle avoidance in search, from weakest to strongest?
10. Why is uninformed search insufficient for chess or Go, and what alternatives does this motivate?
