# Project 02: Search Algorithm Comparison on Route Planning

**Chapters applied:** 3–7 (Problem Solving, Uninformed Search, Informed Search, Local Search, Beyond Classical Search)
**Estimated effort:** ~3 pages of written work plus experimental results
**Format:** Written report with experimental results (tables/charts)
**Total points:** 100

---

## 1. Project Overview

In this project you will compare multiple search algorithms on a route-planning problem: finding a path through a weighted graph (e.g., a road map) from a start location to a goal location. You will implement or simulate at least four search strategies, measure their performance (solution cost, nodes expanded, memory, runtime), and analyze the trade-offs among them.

You may implement the algorithms in a programming language of your choice (Python recommended) or simulate them by hand on a provided graph. The deliverable is a written report (approximately three pages) describing the experimental setup, results, and analysis.

---

## 2. Learning Objectives

By completing this project, you will be able to:

- Implement and compare uninformed and informed search strategies.
- Measure and interpret search performance metrics (completeness, optimality, nodes expanded, time, memory).
- Construct and evaluate admissible heuristics.
- Analyze when each search strategy is preferable.

---

## 3. Detailed Instructions

### 3.1 Problem Domain

Use a weighted, undirected graph representing a road network:

- Nodes = cities or intersections.
- Edges = road segments with positive weights (distance or travel time).
- One start node S and one goal node G.

You may use the Romania road-map example (Arad to Bucharest) or construct your own graph with at least 15 nodes and 25 edges. Provide the graph (adjacency list with weights) in an appendix.

### 3.2 Algorithms to Compare

Implement or simulate at least four of the following:

1. Breadth-First Search (BFS) - treats all edges as unit cost.
2. Uniform-Cost Search (UCS) / Dijkstra - accounts for edge weights.
3. Depth-First Search (DFS) - with cycle checking.
4. Iterative Deepening Search (IDS) / IDDFS.
5. Greedy Best-First Search - uses a heuristic.
6. A* Search - uses g(n) + h(n) with an admissible heuristic.
7. (Optional) Hill Climbing or Simulated Annealing - treating route planning as optimization.

You must include at least one uninformed method (BFS, UCS, DFS, or IDS) and at least one informed method (Greedy or A*).

### 3.3 Heuristic

For informed methods, define an admissible heuristic h(n) = straight-line (Euclidean) distance from node n to the goal G. Justify admissibility: no road can be shorter than the straight-line distance between two points.

---

## 4. Step-by-Step Implementation Guide

### Step 1: Build the Graph (approximately 0.5 page)

Define your graph explicitly. For example:

```
Nodes: {A, B, C, D, E, F, G, ...}
Edges with weights:
  A-B: 75, A-S: 140, ...
```

Include a small diagram or adjacency list. Specify S and G.

### Step 2: Implement Each Search Algorithm (approximately 0.75 page)

For each algorithm, provide pseudo-code or actual code. Key implementation notes:

- **Frontier:** queue (BFS), priority queue ordered by path cost (UCS/A*), stack (DFS).
- **Explored set:** hash table of visited states to avoid re-expansion.
- **Node representation:** state, parent, action, path cost g(n), depth, f(n) = g(n) + h(n) for informed methods.

If implementing in Python, you may use `heapq` for priority queues and `collections.deque` for FIFO/LIFO frontiers.

### Step 3: Define Performance Metrics (approximately 0.25 page)

For each run, record:

- **Solution found?** (yes/no)
- **Solution cost:** sum of edge weights along the path.
- **Solution path:** sequence of nodes from S to G.
- **Nodes expanded:** number of nodes removed from the frontier and expanded.
- **Nodes generated:** total nodes created.
- **Maximum frontier size:** peak memory usage.
- **Runtime:** wall-clock time (optional, in milliseconds).

### Step 4: Run Experiments and Collect Data (approximately 0.75 page)

Run each algorithm on the same graph from S to G. Record results in a table like:

| Algorithm | Solution Cost | Path | Nodes Expanded | Nodes Generated | Max Frontier | Time (ms) | Optimal? |
| --------- | ------------- | ---- | -------------- | --------------- | ------------ | --------- | -------- |
| BFS       |               |      |                |                 |              |           |          |
| UCS       |               |      |                |                 |              |           |          |
| DFS       |               |      |                |                 |              |           |          |
| Greedy    |               |      |                |                 |              |           |          |
| A*        |               |      |                |                 |              |           |          |

Note: BFS solution cost is measured in number of edges (treat as unit cost); UCS/A*/Greedy use edge weights.

### Step 5: Analyze the Results (approximately 1 page)

Write an analysis addressing:

- Which algorithm found the optimal (minimum-cost) solution? Did A* and UCS agree?
- Which algorithm expanded the fewest nodes? Was this expected?
- How did memory usage (max frontier size) compare between BFS/UCS and DFS/IDS?
- Did Greedy Best-First find a suboptimal solution? If so, show the path and its cost versus the optimal cost.
- How did the heuristic affect A*'s performance relative to UCS?

Use the data from your table to support each claim.

### Step 6: Discussion and Conclusion (approximately 0.5 page)

Summarize:

- When to prefer uninformed vs. informed search.
- The role of heuristic quality (admissibility, dominance).
- Limitations of your experiment (single graph, single start/goal pair).
- How the results would change with a larger graph, different heuristic, or dynamic edge weights.

---

## 5. Deliverables and Formatting

Submit:

1. A written report (~3 pages, single-spaced, 11–12 point font) containing:
   - Graph definition (nodes, edges, weights).
   - Algorithm descriptions (pseudo-code or code).
   - Results table.
   - Analysis and conclusion.
2. (Optional but encouraged) Source code as a separate file or appendix.
3. A short bibliography citing the course text (AI, Chapters 3–7) and lecture notes.

---

## 6. Grading Rubric

| Component                                                   | Points        |
| ----------------------------------------------------------- | ------------- |
| Graph definition and problem setup                          | 15            |
| Algorithm implementations (correctness, completeness)       | 30            |
| Performance metrics and results table                       | 20            |
| Analysis of trade-offs (optimality, nodes expanded, memory) | 20            |
| Discussion and conclusion                                   | 10            |
| Clarity, formatting, citations                              | 5             |
| **Total**                                             | **100** |

---

## 7. Optional Extensions (for extra credit)

- Compare IDA* (memory-bounded A*) with standard A* on a larger graph.
- Test with an inadmissible heuristic and show that A* may return a suboptimal solution.
- Run experiments on multiple start–goal pairs and report averages.
- Implement hill climbing or simulated annealing to optimize a route under a different objective (e.g., minimize number of turns).
