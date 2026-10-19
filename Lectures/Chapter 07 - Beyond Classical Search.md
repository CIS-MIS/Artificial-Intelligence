# Artificial Intelligence - Chapter 7: Beyond Classical Search

## Lecture Note Slides (20 Slides)

**Source Materials:** AI - Chapter 7 (textbook); AI Lecture Notes 09 (Reinforcement Learning); AI Lecture Notes 06 (Unsupervised Learning)

---

## Slide 1 - Beyond Classical Search

**Beyond Classical Search: Nondeterministic, Partially Observable, and Online Environments**

Chapter 7 - Beyond Classical Search

A scholarly treatment of search and problem solving when actions are uncertain, the environment is only partially observable, and the agent must act while still searching.

---

## Slide 2 - Limitations of Classical Search

Classical search (Chapters 3-6) assumes:

- A fully observable environment: the agent knows its exact state
- A deterministic environment: each action has a single predictable outcome
- A static environment: the world does not change while the agent deliberates
- A single agent: no other intelligent actors interfere
- Offline operation: the agent finds a complete solution before acting, then executes it

These assumptions fail in many real-world settings:

- Robotics: sensors are noisy, actuators slip, the world changes
- Games: opponents act unpredictably
- Driving: other vehicles, pedestrians, weather are uncertain

Chapter 7 relaxes these assumptions, introducing nondeterministic, partially observable, and online search settings.

---

## Slide 3 - Nondeterministic and Partially Observable Environments

Two key relaxations:

**Nondeterministic environments:** An action may lead to multiple possible outcome states. The transition model becomes a function:
RESULT(s, a) → {s₁, s₂, ..., sₙ}
a set of possible successor states rather than one.

**Partially observable environments:** The agent cannot directly observe its state. It receives percepts that give partial information, and must maintain a **belief state** - the set of all states consistent with its percept history.

When combined, the agent operates in a belief-state space where:

- Each belief state is a set of possible physical states
- Actions map belief states to new belief states
- The goal test applies to belief states (e.g., "all possible states are goal states")

This transforms the problem into searching over belief states, which can be enormously larger than the physical state space.

---

## Slide 4 - Belief-State Search

In a partially observable environment, the agent maintains a belief state representing which physical states it might be in.

Search in belief-state space:

1. Initial belief state: all states consistent with the initial percept
2. Actions: applicable if possible in at least one state in the belief state
3. Transition: for each possible outcome, compute the new belief state incorporating the percept
4. Goal test: all states in the belief state satisfy the goal (for a "sure" goal) or at least one does (for a "possible" goal)

Example: Vacuum world with partial observability (agent knows only current square's dirt status). The belief state tracks all possible combinations of location and dirt configuration consistent with percepts.

Belief-state search can find **sensorless plans** - sequences of actions guaranteed to achieve the goal regardless of actual state, as long as the initial belief is correct.

---

## Slide 5 - Sensorless Vacuum World Example

Vacuum world: two locations A and B, each possibly dirty or clean. 8 physical states. The agent has no sensors (sensorless): it only knows its actions, not percepts.

Initial belief state: all 8 states
Actions: Left, Right, Suck

The action sequence [Suck, Right, Suck] guarantees all squares clean:

- Suck cleans current square
- Right moves to the other square
- Suck cleans that square

Regardless of starting location and dirt status, this sequence ends with both squares clean. This is a **conformant plan** - a solution that works under all possible initial states consistent with the belief state.

Belief-state search finds such plans by searching over sets of physical states.

---

## Slide 6 - Contingency Problems and AND-OR Search

In partially observable environments with sensing, outcomes depend on both the agent's actions and the environment's responses. A single action sequence may not suffice; the agent needs a **contingency plan** - a strategy that specifies what to do under different possible outcomes.

**AND-OR search** represents contingency plans as AND-OR trees:

- **OR nodes:** The agent chooses among actions (at least one branch must succeed)
- **AND nodes:** The environment chooses among outcomes; all branches must succeed (the plan must handle every possible outcome)

A solution is a subtree where:

- Every OR node has at least one selected action
- Every AND node has all outcome branches covered
- All leaves are goal states

Example: Vacuum world with sensing. The agent senses dirt at current location. If dirty → Suck; if clean → move to other location. The plan branches on percepts.

AND-OR search handles environments where the agent cannot predict exact outcomes but can observe and react.

---

## Slide 7 - Online Search Problems

So far, search has been offline: the agent computes a complete solution before acting. In **online search**, the agent must act while still searching - it cannot wait to compute a full plan.

Online search is necessary when:

- The environment is dynamic (changes during deliberation)
- The state space is too large to explore offline
- The agent learns about the environment only by acting

Online agents interleave computation and action:

1. Observe current state
2. Perform a limited local search
3. Take one action
4. Observe the result
5. Repeat

Online search cannot guarantee optimality or even completeness in general. The goal is to act well enough given computational and time constraints.

---

## Slide 8 - Online Search Algorithms

**Online DFS:** Explores depth-first but must return to previously visited states when stuck. Can fail in cyclic environments without memory.

**Learning Real-Time A* (LRTA*):** An online version of A* that:

- Maintains a table of estimated costs h(s) for visited states
- After each action, updates h(s) for the state just left based on the cost of the best successor
- Chooses the action minimizing f(s) = g(s) + h(s) greedily
- Converges to optimal behavior in deterministic, fully observable environments with sufficient experience

LRTA* demonstrates that an agent can learn a good policy through local exploration without ever computing a complete plan offline.

Text Note 09 (Reinforcement Learning) describes exactly this online learning paradigm: the agent acts, receives reward, and updates value estimates - learning from interaction rather than offline planning.

---

## Slide 9 - Nondeterministic Environments: And-Or Graphs and Contingency

When actions have multiple possible outcomes, the agent cannot guarantee reaching a goal with a fixed action sequence. It needs a policy - a mapping from states (or belief states) to actions.

**Contingency planning** constructs policies that branch on observations:

- If percept P₁ is received, take action A₁
- If percept P₂ is received, take action A₂

This is closely related to:

- **Reinforcement learning (Text Note 09):** learns a policy from reward feedback through trial and error
- **Markov Decision Processes:** formal framework for decision-making under uncertainty (foundation of RL)

The contingency plan is an AND-OR tree where OR nodes represent agent choices and AND nodes represent environmental uncertainty over outcomes.

---

## Slide 10 - The Agent-Environment Interaction Loop Revisited

Classical search assumes a clean separation: plan offline, then execute. Beyond classical search, the loop is interleaved:

1. **Perceive:** Receive partial, noisy information
2. **Update belief:** Revise the belief state based on percepts and actions
3. **Deliberate:** Choose an action using limited search or learned policy
4. **Act:** Execute the action
5. **Environment transitions:** Possibly nondeterministically
6. **Repeat**

This loop is the foundation of robotics (Text Note 11) and reinforcement learning (Text Note 09), where perception, planning, and action are tightly coupled.

---

## Slide 11 - From Belief States to Reinforcement Learning

Text Note 09 (Reinforcement Learning) extends beyond classical search by addressing environments where:

- Correct actions cannot be demonstrated in advance (no labeled data)
- Rewards arrive only after sequences of actions (credit assignment problem)
- The agent must balance exploration and exploitation

RL formalizes the beyond-classical-search setting:

- **Agent** acts in an **environment**
- Receives **states** and **rewards**
- Learns a **policy** mapping states to actions
- Uses **value functions** to estimate long-term reward

Where belief-state search computes plans from a known model, RL learns policies from experience when the model is unknown or too large to enumerate.

---

## Slide 12 - Partially Observable MDPs (POMDPs)

A Partially Observable Markov Decision Process (POMDP) is the formal model combining:

- Markov transitions (stochastic, state-dependent dynamics)
- Partial observations (agent receives imperfect percepts)
- Rewards (objective to maximize)

Solving a POMDP optimally is intractable for large spaces, but approximate methods exist:

- Point-based value iteration
- Monte Carlo tree search in belief space (POMCP)
- Deep RL with recurrent policies (memory networks)

POMDPs unify belief-state search, reinforcement learning, and planning under uncertainty - the full beyond-classical-search setting.

---

## Slide 13 - Belief-State Search in Robotics

Text Note 11 (Robotics) shows how belief-state reasoning enters physical agents. A mobile robot does not know its exact pose; wheel encoders drift and cameras give noisy views. The robot maintains a belief distribution over possible locations and updates it with each sensor reading (localization).

Simultaneous Localization and Mapping (SLAM) extends this: the robot must simultaneously build a map (unknown landmarks) and track its position within it. Both the map and the pose are uncertain, so the belief state is over joint map-pose configurations. Search and planning then operate within this belief space, choosing actions that reduce uncertainty as well as make progress toward the goal.

---

## Slide 14 - Online Search in Dynamic and Real-Time Settings

Online search is essential when the world changes faster than the agent can recompute a full plan. A self-driving car cannot replan its entire route every time a pedestrian steps into the street; it must react immediately while continuing to refine its longer-term plan.

This motivates **anytime algorithms**: methods that return a valid (if not optimal) answer at any time they are interrupted, and improve the answer the longer they run. LRTA* and real-time heuristic search are anytime in spirit - they act after a bounded local computation and improve their value estimates with experience.

The trade-off is clear: less computation per action means faster reaction but potentially lower solution quality. The agent must balance deliberation and execution based on the time-criticality of the domain.

---

## Slide 15 - Exploration and Exploitation Beyond Search

Beyond classical search, exploration is not just a search heuristic - it is a core objective. In reinforcement learning (Text Note 09), the agent must deliberately try suboptimal actions to discover whether they lead to better long-term reward. This exploration-exploitation dilemma has no analogue in classical offline search, where the model is known and the optimal plan can be computed without trying anything.

Methods for managing exploration include epsilon-greedy (sometimes act randomly), optimistic initialization (assume unseen states are valuable), and uncertainty-directed exploration (act where the model is most uncertain). These ideas bridge search, learning, and decision theory.

---

## Slide 16 - From Offline Planning to Lifelong Learning

Classical search delivers a one-shot solution: compute, then act. Beyond classical search delivers a **lifelong process**: act, observe, update the model or value estimates, and act again. The agent never finishes learning; its policy improves continuously as it accumulates experience.

This shift has profound implications for AI system design. Systems must be built to operate safely while still learning, to handle distribution shift (the world changes after deployment), and to expose their uncertainty so humans can intervene when needed. Beyond classical search is therefore not just a technical extension but a reorientation of what an intelligent agent does.

---

## Slide 17 - Comparing Search Paradigms

Classical, informed, local, and beyond-classical search form a spectrum rather than unrelated techniques:

- **Classical uninformed/informed search (Chapters 3-5):** Offline, deterministic, fully observable, known model; computes a complete plan before acting.
- **Local search (Chapter 6):** Optimizes a complete state; no path matters; good for landscapes where any good state suffices.
- **Beyond-classical search (Chapter 7):** Nondeterministic, partially observable, online; interleaves planning, sensing, and action.

No single paradigm dominates. A delivery robot might use A* (informed search) for route planning, simulated annealing (local search) to schedule deliveries, and belief-state search (Chapter 7) to handle uncertain sensor readings. Choosing the right paradigm for each subproblem is a central systems-design skill.

---

## Slide 18 - Safety, Uncertainty, and Human Oversight

When search and learning operate under uncertainty, safety becomes a first-class concern. A plan computed under a wrong model can fail catastrophically when executed. Beyond-classical search methods mitigate this by:

- Maintaining belief states that represent uncertainty explicitly
- Replanning online as new percepts arrive
- Learning value functions that estimate long-term risk, not just immediate reward

Still, no automated method guarantees safety. Human oversight, verification, conservative fallback behaviors, and clear operational limits remain essential, especially in robotics, healthcare, and autonomous vehicles (Text Notes 11, 14).

---

## Slide 19 - Summary: Key Takeaways

1. Classical search assumes full observability, determinism, static environments, single agents, and offline operation - assumptions that fail in many real settings
2. Nondeterministic environments have actions with multiple possible outcomes; partially observable environments hide the true state from the agent
3. Belief states represent sets of possible physical states consistent with percept history; search over belief states finds conformant and contingency plans
4. The sensorless vacuum world shows how action sequences can guarantee goals without any sensing
5. AND-OR search represents contingency plans: OR nodes for agent choices, AND nodes for environmental outcomes
6. Online search interleaves computation and action; LRTA* learns cost estimates through local exploration
7. Reinforcement learning (Text Note 09) addresses the same setting through trial-and-error policy learning
8. POMDPs formally model decision-making under stochasticity and partial observability
9. The perception-deliberation-action loop is central to robotics and RL agents
10. Beyond classical search shifts from "compute a plan then act" to "act, observe, learn, and adapt continuously"

---

## Slide 20 - Review Questions

1. List the assumptions of classical search and explain why each fails in at least one real-world domain.
2. What is a belief state, and how does belief-state search differ from physical-state search?
3. Trace how the action sequence [Suck, Right, Suck] solves the sensorless vacuum world from any initial state.
4. Contrast OR nodes and AND nodes in an AND-OR search tree. What does a solution subtree look like?
5. Why can't classical offline search guarantee optimality in online search settings?
6. How does LRTA* update its heuristic table, and what does it converge to?
7. What is the credit assignment problem, and why does it arise in nondeterministic environments?
8. How does reinforcement learning (Text Note 09) address environments where correct actions cannot be demonstrated in advance?
9. What is a POMDP, and why is optimal POMDP solving intractable for large spaces?
10. Compare belief-state search and reinforcement learning: when would you prefer each approach?
