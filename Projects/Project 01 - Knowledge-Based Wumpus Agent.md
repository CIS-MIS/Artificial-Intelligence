# Project 01: Knowledge-Based Wumpus World Agent

**Chapters applied:** 1–3, 9–12 (Agents, Problem Formulation, Propositional Logic, First-Order Logic)
**Estimated effort:** ~3 pages of written work plus design artifacts
**Format:** Individual written report with optional pseudo-code or code snippets
**Total points:** 100

---

## 1. Project Overview

In this project you will design a knowledge-based agent for the Wumpus World, a classic 4x4 grid environment in which an agent must navigate to retrieve gold while avoiding pits and a Wumpus. Your agent will maintain a knowledge base (KB), receive percepts, use logical inference to derive safe moves, and act accordingly.

You are **not required to run code**, though you may. The deliverable is a rigorous written design report (approximately three pages) that specifies the knowledge representation, the inference mechanism, the agent's perception-action cycle, and a worked example trace. The emphasis is on conceptual correctness and scholarly depth, not on a working implementation.

---

## 2. Learning Objectives

By completing this project, you will be able to:

- Formalize an agent environment using the PEAS framework.
- Represent environment knowledge in propositional logic (and optionally first-order logic).
- Apply inference rules (Modus Ponens, Resolution) to derive new facts from percepts.
- Design a perception–deliberation–action loop for a knowledge-based agent.
- Analyze the scalability and limitations of propositional-logic agents.

---

## 3. Detailed Instructions

### 3.1 Environment Specification

Use the standard 4x4 Wumpus World:

- Grid coordinates [1,1] through [4,4]; the agent starts at [1,1] facing right.
- One Wumpus lives in a single square; entering it is fatal.
- Pits live in some squares; entering one is fatal.
- Exactly one square contains gold; grabbing it and exiting at [1,1] wins.
- Percepts: Stench (adjacent to Wumpus), Breeze (adjacent to pit), Glitter (gold in current square), Bump (walked into a wall), Scream (Wumpus killed).
- Actions: TurnLeft, TurnRight, Forward, Shoot, Grab, Climb.

### 3.2 Required Components of Your Report

Your report must contain the following sections, each clearly labeled:

1. **PEAS Specification** - Define Performance, Environment, Actuators, Sensors for this agent.
2. **Knowledge Representation** - Propositional symbols and logical rules (CNF) encoding the Wumpus domain.
3. **Inference Mechanism** - Resolution (or forward/backward chaining) used to derive conclusions.
4. **Agent Algorithm** - The perception–deliberation–action loop in pseudo-code or structured English.
5. **Worked Example Trace** - A step-by-step trace from initial percepts to a safe action.
6. **Limitations and Extensions** - Scalability issues, the frame problem, uncertainty, and how first-order logic or probabilistic methods would help.

---

## 4. Step-by-Step Implementation Guide

### Step 1: Define PEAS (approximately 0.5 page)

Write a concise PEAS description:

- **Performance measure:** +1000 for grabbing gold and exiting, −1000 for dying, −1 per action, −10 for using an arrow.
- **Environment:** 4x4 grid, one Wumpus, pits, gold, stochastic arrow (may miss).
- **Actuators:** TurnLeft, TurnRight, Forward, Shoot, Grab, Climb.
- **Sensors:** Stench, Breeze, Glitter, Bump, Scream.

Justify each component. Note which PEAS dimensions make this a partially observable, deterministic (mostly), static, single-agent environment.

### Step 2: Choose a Knowledge Representation (approximately 0.75 page)

Define propositional symbols for every relevant fact. For example:

- P[i,j]: there is a pit in [i,j]
- W[i,j]: there is a Wumpus in [i,j]
- B[i,j]: there is a breeze in [i,j]
- S[i,j]: there is a stench in [i,j]
- OK[i,j]: [i,j] is safe
- FacingRight, FacingLeft, FacingUp, FacingDown: agent orientation

Write the domain rules in CNF. The key rules are:

- Breeze rule: B[i,j] ↔ (P[i-1,j] ∨ P[i+1,j] ∨ P[i,j-1] ∨ P[i,j+1])
- Stench rule: S[i,j] ↔ (W[i-1,j] ∨ W[i+1,j] ∨ W[i,j-1] ∨ W[i,j+1])
- Safety: OK[i,j] ↔ ¬P[i,j] ∧ ¬W[i,j]

Show at least two rules fully converted to CNF, including the elimination of ↔ and → and distribution of ∨ over ∧.

### Step 3: Specify the Inference Mechanism (approximately 0.5 page)

Decide whether your agent uses resolution-based theorem proving or forward chaining over Horn clauses.

- If resolution: explain proof by contradiction - to ask "is [2,1] safe?", add ¬OK[2,1] to the KB and try to derive the empty clause.
- If forward chaining: explain how new percepts trigger rule firings and how conclusions (safe squares) are added to the KB.

State whether your inference is sound and complete, and under what conditions (e.g., Horn clauses for linear-time forward chaining).

### Step 4: Design the Agent Loop (approximately 0.5 page)

Write the agent program in structured English or pseudo-code:

```
function WUMPUS-AGENT(percept) returns action
   add percept to KB
   add action consequences to KB (update location, orientation)
   ask KB: which neighboring squares are safe (OK)?
   if gold in current square then return Grab
   if at [1,1] with gold then return Climb
   if a safe unvisited square exists then return move toward it
   if Wumpus location known and have arrow then return Shoot
   else return random safe move / backtrack
```

Explain how the KB is updated with each percept and each executed action (including the frame problem: what stays the same after moving).

### Step 5: Worked Example Trace (approximately 0.75 page)

Trace a short sequence. Start with the initial percept at [1,1]: Breeze, no Stench, no Glitter.

1. Tell KB: B[1,1], ¬S[1,1], ¬Glitter[1,1], ¬P[1,1], OK[1,1].
2. Infer: B[1,1] means P[1,2] ∨ P[2,1]. Since ¬B[2,1] (after moving or by assumption), neighbors of [2,1] are pit-free, so ¬P[2,1]. Therefore P[1,2] must hold. Thus [2,1] is safe.
3. Ask KB: Is [2,1] safe? Yes → move Forward to [2,1].
4. At [2,1], perceive new stench/breeze. Update KB and repeat.

Show the KB contents and the derived conclusion at each step. Indicate which inference rule was applied.

### Step 6: Limitations and Extensions (approximately 0.5 page)

Discuss:

- **Scalability:** Propositional logic needs one symbol per square per property; a 4x4 grid is manageable, but a larger world explodes.
- **The frame problem:** representing everything that does not change when the agent moves.
- **Uncertainty:** classical logic is true/false; real sensors are noisy. Mention how Bayesian networks (Chapters 13–14) or first-order logic (Chapters 11–12) address these.

---

## 5. Deliverables and Formatting

Submit a single document (PDF or Markdown) containing:

- A title page with your name, course, and project title.
- Sections 1–6 as above.
- Any pseudo-code, logical formulas, and the trace clearly formatted.
- A short bibliography citing the course text (AI, Chapters 1–3, 9–12) and lecture notes.

Target length: approximately three pages of substantive content (excluding title page and bibliography), single-spaced, 11–12 point font.

---

## 6. Grading Rubric

| Component                                      | Points        |
| ---------------------------------------------- | ------------- |
| PEAS specification                             | 15            |
| Knowledge representation (symbols + CNF rules) | 25            |
| Inference mechanism (resolution / chaining)    | 20            |
| Agent algorithm (perception–action loop)      | 15            |
| Worked example trace                           | 15            |
| Limitations and extensions                     | 10            |
| Clarity, formatting, citations                 | 5             |
| **Total**                                | **100** |

---

## 7. Optional Extensions (for extra credit)

- Extend the representation to first-order logic using ∀, ∃, and functions (e.g., East(x), West(x)), showing how one rule covers all squares instead of one per square.
- Implement the agent in Python and include a short transcript of a complete game.
- Add probabilistic reasoning: replace certain pit/Wumpus facts with probability distributions and compute P(safe | percepts) using Bayes' rule.
