# Artificial Intelligence - Chapter 3: Solving Problems by Searching

## Lecture Note Slides (20 Slides)

**Source Materials:** AI - Chapter 3 (textbook); AI Lecture Notes 12 (AI and Game Playing); AI Lecture Notes 17 (Search Engines and Knowledge Bases)

---

## Slide 1 - Solving Problems by Searching

**Solving Problems by Searching: Problem Formulation, State Spaces, and Search Strategies**

Chapter 3 - Solving Problems by Searching

A scholarly treatment of how intelligent agents formulate problems, explore state spaces, and find goal-reaching action sequences.

---

## Slide 2 - Problem-Solving Agents

A problem-solving agent is a goal-based agent that decides what to do by finding sequences of actions that lead to desirable states.

The agent operates in a cycle:

1. **Goal formulation:** Define what the agent wants to achieve
2. **Problem formulation:** Decide which actions and states to consider
3. **Search:** Determine the best sequence of actions
4. **Execution:** Carry out the actions one at a time

**Key principle:** The agent does not act until it has found a solution. This is "offline" problem solving - thinking before acting - as opposed to online problem solving where the agent acts while searching.

Problem formulation is the most important and most creative step. A poor formulation makes an easy problem intractable; a good formulation makes a hard problem solvable.

---

## Slide 3 - Problem Formulation

A problem is defined by five components:

1. **Initial state:** The state from which the agent starts
2. **Actions:** The set of possible actions available in each state
3. **Transition model:** A function that specifies the result of each action in each state (successor function)
4. **Goal test:** A predicate that determines whether a state is a goal state
5. **Path cost:** A function that assigns a numeric cost to each path

A **solution** is a sequence of actions from the initial state to a goal state. An **optimal solution** has the lowest path cost among all solutions.

Example: Road-trip planning from Arad to Bucharest

- Initial state: at(Arad)
- Actions: drive between connected cities
- Transition model: driving from city X to city Y results in being at city Y
- Goal test: at(Bucharest)
- Path cost: sum of distances traveled

---

## Slide 4 - States, State Spaces, and Search Trees

A **state** represents a configuration of the world relevant to the problem. The **state space** is the set of all states reachable from the initial state.

A **search tree** is a rooted tree whose nodes are states and whose edges are actions. The root is the initial state. Children of a node are states reachable by applying each applicable action.

Key terms:

- **Node:** A state in the search tree
- **Edge:** An action transitioning from one state to another
- **Branch:** A possible action sequence from a state
- **Terminal state:** A state where the problem ends (goal reached or no actions available)
- **Path:** A sequence of nodes connected by edges

The search tree can grow enormous. Chapters 3-7 focus on strategies for exploring it efficiently without examining every node.

Text Note 12 (AI and Game Playing) uses the same tree representation for game states: board configurations as nodes, moves as edges, terminal states as win/loss/draw.

---

## Slide 5 - Example: The Romania Road Map

The classic Romania problem: drive from Arad to Bucharest using a map of connected cities with known distances.

States: The 20 cities in Romania
Initial state: Arad
Goal test: state = Bucharest
Actions: Drive from one city to an adjacent city
Transition model: Driving from city X to adjacent city Y results in being at Y
Path cost: Total distance in kilometers

Example path: Arad - Sibiu - Fagaras - Bucharest, with cost 118 + 99 + 211 = 428 km

This example illustrates:

- A finite, fully observable, deterministic, static environment
- A single-agent problem
- A small enough state space that exhaustive search is feasible
- Multiple solutions exist; the agent seeks an optimal (shortest) one

---

## Slide 6 - Example: The Vacuum World

A simplified vacuum world problem:

States: Agent location (A or B) x dirt status of each square
Initial state: One of eight possible configurations
Actions: Left, Right, Suck, NoOp
Transition model: Suck cleans the current square; Left/Right move the agent
Goal test: All squares are clean
Path cost: Number of actions taken

This demonstrates:

- A small state space (8 states for 2 locations)
- Fully observable variant: agent knows dirt status everywhere
- Partially observable variant: agent knows only current square's dirt status

The vacuum world is used throughout the text to illustrate reflex vs. planning agents and the effects of observability on problem difficulty.

---

## Slide 7 - Example: The 8-Puzzle

The 8-puzzle is a 3x3 board with 8 numbered tiles and one blank space.

States: Arrangements of tiles on the board
Initial state: Any starting arrangement
Goal test: Tiles in order (1-8 with blank at bottom-right)
Actions: Move the blank up, down, left, or right (if possible)
Transition model: Sliding a tile into the blank space
Path cost: Number of moves (each costs 1)

The 8-puzzle has 9!/2 = 181,440 reachable states - small enough for complete search but large enough to illustrate search efficiency differences.

The 15-puzzle (4x4 board) has roughly 10^13 states - too large for exhaustive search, requiring intelligent search strategies.

---

## Slide 8 - Example: The 8-Queens Problem

Place 8 queens on an 8x8 chessboard so no two queens attack each other.

**Incremental formulation (inefficient):**
States: All placements of 8 queens (64 choose 8 approx 4.4 billion)
Actions: Add a queen to any square
Path cost: 0 (all solutions equal)

**Complete-state formulation (efficient):**
States: Arrangements with one queen per column (8^8 approx 16.7 million)
Actions: Move a queen within its column
Goal test: No queens attack each other

This illustrates a crucial lesson: **problem formulation determines search difficulty**. A good formulation reduces the state space dramatically and makes search feasible.

---

## Slide 9 - Tree Search vs. Graph Search

**Tree Search:** Explores the search tree by expanding nodes. It may revisit the same state via different paths, leading to redundant work. In spaces with loops (e.g., Romania map), tree search can fail to terminate.

**Graph Search:** Tree search augmented with an explored set - a record of states already visited. When a newly generated state matches one in the explored set, it is discarded. This prevents redundant exploration and guarantees termination in finite state spaces.

Trade-off:

- Tree search uses less memory (no explored set to store)
- Graph search avoids redundant work and handles loops correctly

Most practical implementations use graph search, with the explored set implemented as a hash table for O(1) lookups.

---

## Slide 10 - Search Strategy Evaluation Criteria

Search strategies are compared along four dimensions:

**Completeness:** Is the strategy guaranteed to find a solution if one exists?
**Optimality:** Does the strategy find the lowest-cost solution?
**Time complexity:** How long does search take as a function of the state space?
**Space complexity:** How much memory does search require?

Key parameters:

- **b:** Branching factor (maximum number of successors per node)
- **d:** Depth of the shallowest goal node
- **m:** Maximum depth of the state space (may be infinite)
- **l:** Depth limit imposed on search

These criteria guide the choice among uninformed search (Chapter 4), informed search (Chapter 5), local search (Chapter 6), and beyond-classical search (Chapter 7).

---

## Slide 11 - Data Structures for Search

Search algorithms require two key data structures:

**1. Frontier (Open List):** The set of nodes generated but not yet expanded. Different implementations define different search strategies:

- Queue (FIFO) Breadth-First Search
- Stack (LIFO) Depth-First Search
- Priority queue ordered by path cost Uniform-Cost Search
- Priority queue ordered by heuristic A* search

**2. Explored Set (Closed List):** States already expanded, used in graph search to avoid revisiting.

A node stores: state, parent node, action applied, path cost, and depth. Efficient node representation and frontier management are critical for search performance.

---

## Slide 12 - Search Algorithms: General Formulation

All search algorithms follow the same skeleton:

```
function GENERAL-SEARCH(problem, strategy) returns solution or failure
    initialize frontier using initial state of problem
    initialize explored set to empty
    loop do
        if frontier is empty then return failure
        choose a leaf node from frontier according to strategy
        if node contains a goal state then return corresponding solution
        add node to explored set
        expand the chosen node, adding resulting nodes to frontier
```

The only difference among strategies is **which node to expand next** - the choice function. This choice determines completeness, optimality, and complexity.

---

## Slide 13 - Uninformed vs. Informed Search

**Uninformed (Blind) Search:** No additional information about states beyond the problem definition. Strategies include breadth-first, uniform-cost, depth-first, depth-limited, iterative deepening, and bidirectional search.

**Informed (Heuristic) Search:** Uses problem-specific knowledge (a heuristic function) to guide search toward promising states. Strategies include greedy best-first search and A* search.

Chapters 4 and 5 develop these in detail. The distinction matters because informed search can be dramatically faster when a good heuristic is available, but uninformed search is universally applicable without domain engineering.

---

## Slide 14 - Search in Games and Real-Time Systems

Text Note 12 (AI and Game Playing) applies search trees to game playing:

- Game states are nodes; legal moves are edges
- Minimax explores the tree assuming optimal opponents
- Combinatorial explosion (10^20 checkers, 10^50 chess, 10^170 Go states) makes exhaustive search impossible for complex games
- Monte Carlo Tree Search uses simulations to focus on promising branches
- Modern systems combine neural networks (to estimate move quality) with search (to examine consequences)

Text Note 17 (Search Engines) applies similar principles to information retrieval: crawlers gather pages, inverted indexes organize them, and ranking algorithms order results - a form of search over a massive, dynamic state space.

---

## Slide 15 - Beyond State-Space Search: Problem Structure

Not all problems are best modeled as state-space search. Chapter 3 introduces alternative formulations:

**Constraint Satisfaction Problems (CSPs):** States defined by variable assignments; goal is to satisfy constraints (e.g., map coloring, scheduling). Solved with constraint propagation and backtracking rather than path search.

**Optimization Problems:** Find the best state according to an objective function, where the path to the state is irrelevant. Solved with local search (hill climbing, simulated annealing, genetic algorithms - Chapter 6).

**Adversarial Problems:** Opponents act against the agent. Solved with minimax and alpha-beta pruning (Chapter 8).

---

## Slide 16 - Problem Formulation as a Creative Act

There is no unique correct formulation of a problem. The designer must choose:

- What level of detail to represent in states
- Which actions to include
- How to measure cost
- What constitutes a goal

Trade-offs:

- More detailed states larger state space but more precise modeling
- More actions greater flexibility but higher branching factor
- Abstraction smaller state space but potentially suboptimal solutions

Text Note 12 emphasizes that games succeed as AI testbeds precisely because they have clear objectives, measurable results, and controlled environments - properties that make problem formulation tractable.

---

## Slide 17 - When Search Is and Is Not Sufficient

Search is sufficient when the state space is finite, the goal is well-defined, and the cost of exploration is acceptable. Search is not sufficient when:

- The state space is continuous or effectively infinite
- The environment changes while the agent deliberates (dynamic worlds)
- The agent cannot observe the full state (partial observability)
- An intelligent opponent acts against the agent (adversarial settings)

In these cases, AI must supplement search with heuristics, local optimization, learning, or reactive control rather than relying on complete offline planning.

---

## Slide 18 - Search in Robotics and Real-World Agents

Text Note 11 (Robotics) shows how search fits into a larger agent loop: perception, localization, mapping, planning, manipulation, and control. Search determines the route, but the robot must also sense obstacles, localize itself, and adjust in real time via closed-loop feedback.

A robot retrieving a snack uses search to plan the path to the kitchen, but relies on localization to know where it is, manipulation to pick up the snack, and closed-loop control to correct errors during execution. Search alone does not produce intelligent physical action.

---

## Slide 19 - Summary: Key Takeaways

1. Problem-solving agents find action sequences to reach goal states through offline search before acting
2. A problem is defined by initial state, actions, transition model, goal test, and path cost
3. States form a state space; search explores it as a tree or graph
4. Problem formulation critically affects search difficulty (8-queens example)
5. Graph search avoids redundant exploration via an explored set; tree search may not terminate in loopy spaces
6. Search strategies are evaluated by completeness, optimality, time, and space complexity
7. The frontier data structure determines which node is expanded next - this is the essence of search strategy
8. Uninformed search uses no domain knowledge; informed search uses heuristics
9. Search underlies game playing, route planning, puzzle solving, and information retrieval
10. Problem formulation is a creative engineering act involving abstraction and trade-offs

---

## Slide 20 - Review Questions

1. What are the five components of a problem definition, and what role does each play?
2. What is the difference between a state, a state space, and a search tree?
3. Why is problem formulation considered the most important step in problem solving?
4. How does graph search differ from tree search, and why is an explored set necessary?
5. Define completeness, optimality, time complexity, and space complexity for search strategies.
6. What are b, d, m, and l in search complexity analysis?
7. Describe the general search algorithm skeleton and explain where strategies differ.
8. Contrast uninformed search with informed search.
9. How is the Romania road-map problem formulated as a search problem?
10. Why does the 8-puzzle have 181,440 reachable states, and why does formulation matter for the 8-queens problem?
