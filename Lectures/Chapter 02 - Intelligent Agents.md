# Artificial Intelligence - Chapter 2: Intelligent Agents

## Lecture Note Slides (20 Slides)

**Source Materials:** AI - Chapter 2 (textbook); AI Lecture Notes 01 (Introduction to AI); AI Lecture Notes 09 (Reinforcement Learning); AI Lecture Notes 11 (Robotics)

---

## Slide 1 - Intelligent Agents

**Intelligent Agents: Perception, Action, and Rationality**

Chapter 2 - Intelligent Agents

A scholarly treatment of agents, environments, PEAS, agent architectures, and the foundations of rational decision-making in AI.

---

## Slide 2 - What Is an Agent?

An agent is anything that can be viewed as perceiving its environment through sensors and acting upon that environment through actuators.

**Human agents:** Eyes, ears, and other organs as sensors; hands, legs, vocal tract as actuators
**Robotic agents:** Cameras, LiDAR, and infrared sensors as sensors; motors and grippers as actuators
**Software agents:** Keystrokes, file contents, and network packets as sensors; screen output and network messages as actuators

The agent function maps percept histories to actions:
f: P* → A

where P* is the set of all possible percept sequences and A is the set of possible actions.

Chapter 2 establishes the agent as the fundamental unit of analysis in AI: rather than asking "what is intelligence?" in the abstract, we ask how a situated system should act to achieve its objectives.

---

## Slide 3 - The PEAS Framework

To specify an agent design, we must define its task environment using PEAS:

**P - Performance Measure:** The criterion for success. For a taxi: safe, timely, legal, comfortable, profitable trips.
**E - Environment:** The world the agent operates in. For a taxi: roads, traffic, pedestrians, weather, other drivers.
**A - Actuators:** How the agent acts. For a taxi: steering, accelerator, brake, turn signal, horn, display.
**S - Sensors:** What the agent perceives. For a taxi: cameras, LiDAR, radar, GPS, speedometer, accelerometer, sonar.

Text Note 01 (Slide 8 of Chapter 1) introduces PEAS and applies it to an autonomous taxi. Chapter 2 systematizes the framework across many domains.

The PEAS description must be precise enough to guide agent design but abstract enough to capture the essential structure of the task.

---

## Slide 4 - Rational Agents and Rationality

A rational agent selects the action expected to maximize its performance measure, given:

- The evidence provided by the percept sequence
- Whatever built-in knowledge the agent possesses

Rationality is not the same as omniscience:

- **Omniscience** would require knowing the actual outcome of every possible action before acting - impossible in a complex, uncertain world
- **Rationality** requires maximizing expected performance based on available information

A rational agent may make a decision that turns out badly due to bad luck or incomplete information; what matters is that the decision was the best one supported by the evidence at the time.

Rationality depends on four factors:

1. The performance measure defining success
2. The agent's prior knowledge of the environment
3. The set of actions the agent can perform
4. The agent's percept sequence to date

---

## Slide 5 - Omniscience vs. Rationality: A Critical Distinction

Consider an agent deciding whether to cross a street:

- An omniscient agent would know exactly whether a car is coming around the blind corner
- A rational agent looks both ways, listens, and crosses when the available evidence suggests it is safe

The omniscient standard is unattainable. Rationality is the appropriate standard for AI because agents must operate under uncertainty with bounded computational resources.

This distinction shapes every agent design in this course: we build agents that make good decisions given their limitations, not agents that know everything.

Text Note 09 (Reinforcement Learning) connects rationality to expected value: an agent estimates the long-term usefulness of states and acts to maximize cumulative reward.

---

## Slide 6 - Agent Architectures

Chapter 2 presents four agent types in increasing order of sophistication:

**1. Simple Reflex Agents**

- Select actions based on the current percept only, using condition-action rules (if-then)
- Example: A vacuum cleaner that sucks when it detects dirt and moves randomly when the floor is clean
- Limitation: Cannot handle partial observability; may enter infinite loops

**2. Model-Based Reflex Agents**

- Maintain an internal model of how the world works and track aspects not currently visible
- Example: A robot vacuum that remembers which rooms it has already cleaned
- Handles partial observability by maintaining state

**3. Goal-Based Agents**

- Act to achieve specific goals, not just respond to immediate percepts
- Use search and planning to evaluate action sequences
- Example: A navigation agent that plans a route to a destination

**4. Utility-Based Agents**

- Choose actions that maximize a utility function representing preferences over states
- Handle trade-offs between competing objectives (speed vs. safety vs. cost)
- Example: A taxi agent that balances arrival time, passenger comfort, and fuel efficiency

---

## Slide 7 - Learning Agents

A learning agent improves its performance over time through experience. It consists of four conceptual components:

**1. Learning Element:** Responsible for making improvements; modifies the performance element based on feedback
**2. Performance Element:** Selects external actions based on current knowledge
**3. Critic:** Provides feedback on how well the agent is doing relative to a performance standard
**4. Problem Generator:** Suggests exploratory actions that lead to new experiences

The learning element modifies the performance element; the critic evaluates performance; the problem generator ensures the agent does not stagnate by only repeating known-good actions.

Text Note 09 (Reinforcement Learning) elaborates on how agents learn from reward signals, update value functions, and improve policies through trial and error.

---

## Slide 8 - Task Environments: Properties and Classification

Environments differ along key dimensions that determine appropriate agent design:

**Fully vs. Partially Observable:** Can the agent sense all aspects of the state relevant to its decisions?

- Fully observable: Chess board (all pieces visible)
- Partially observable: Poker (opponent cards hidden)

**Deterministic vs. Stochastic:** Is the next state fully determined by current state and action?

- Deterministic: A logic puzzle
- Stochastic: Backgammon (dice rolls), robotics (sensor noise, slippage)

**Static vs. Dynamic:** Does the environment change while the agent is deliberating?

- Static: Crossword puzzle
- Dynamic: Taxi driving (traffic changes during route planning)

**Discrete vs. Continuous:** Are states, actions, and time distinct or continuous?

- Discrete: Chess (distinct board positions)
- Continuous: Driving (steering angle, speed vary continuously)

**Single-Agent vs. Multi-Agent:** Are other intelligent agents present whose actions affect outcomes?

- Single-agent: Solitaire
- Multi-agent: Chess, poker, autonomous driving with other vehicles

---

## Slide 9 - Environment Types and Examples

| Environment           | Observable   | Deterministic | Static  | Discrete   | Agents |
| --------------------- | ------------ | ------------- | ------- | ---------- | ------ |
| Crossword puzzle      | Full         | Yes           | Static  | Discrete   | Single |
| Chess                 | Full         | Yes           | Static  | Discrete   | Multi  |
| Poker                 | Partial      | Stochastic    | Static  | Discrete   | Multi  |
| Taxi driving          | Partial      | Stochastic    | Dynamic | Continuous | Multi  |
| Robot soccer          | Partial      | Stochastic    | Dynamic | Continuous | Multi  |
| Vacuum world (simple) | Full/Partial | Deterministic | Static  | Discrete   | Single |

The environment classification directly constrains which algorithms are suitable. A static, fully observable, deterministic environment admits exhaustive search; a dynamic, stochastic, multi-agent environment requires reactive and probabilistic methods.

---

## Slide 10 - The Vacuum World: A Minimal Agent Environment

The vacuum world is a classic toy environment used throughout AI to illustrate agent concepts:

- Two locations (A and B), each possibly dirty or clean
- The vacuum agent can: move left, move right, suck up dirt, or do nothing
- Percepts: location and whether dirt is present at that location

**Simple reflex agent behavior:**

- If current location is dirty → suck
- If current location is clean and at A → move right
- If current location is clean and at B → move left

This agent is rational for the simple vacuum world but demonstrates limitations: it has no memory and cannot plan ahead.

A model-based reflex agent would track which locations have been cleaned and avoid revisiting them unnecessarily, improving efficiency.

---

## Slide 11 - Reflex Agents vs. Model-Based Agents

**Simple Reflex Agents:**

- Act solely on current percept
- Cannot handle partial observability (aliased percepts)
- May loop indefinitely (e.g., moving back and forth between two clean squares)
- Suitable only for fully observable, simple environments

**Model-Based Reflex Agents:**

- Maintain internal state representing unobserved aspects of the world
- Update state based on percepts and action effects
- Choose actions based on state, not just current percept
- Can operate in partially observable environments if the model is adequate

The model-based approach introduces the key idea that intelligent action often requires remembering the past and inferring the present from incomplete observations.

---

## Slide 12 - Goal-Based Agents and Deliberation

Goal-based agents go beyond reflexive response by considering future consequences:

- They know their goal state(s)
- They use search to find action sequences leading to goal states
- They can choose among multiple paths to the same goal
- Goals provide flexibility: new goals can be specified without reprogramming action rules

**Limitation:** Goals are binary (achieved or not). They cannot express preferences among different goal-achieving outcomes or trade-offs between competing objectives.

Example: A navigation agent with goal "reach the airport" might choose any route that gets there, even one that is dangerous or expensive, because the goal does not encode quality preferences.

---

## Slide 13 - Utility-Based Agents and Preferences

Utility-based agents address the limitation of goal-based agents by using a utility function:

U: S → ℝ

where S is the set of states and ℝ is the real numbers. Utility represents the agent's preference over states.

The agent selects the action expected to maximize utility. This allows:

- Trade-offs between conflicting objectives (e.g., speed vs. safety vs. cost)
- Reasoning under uncertainty: maximize expected utility rather than guaranteed outcomes
- Fine-grained preferences (state A is better than state B, but both are acceptable)

Text Note 09 (Reinforcement Learning) connects utility to value functions: V(s) estimates the expected long-term reward from state s, guiding action selection.

---

## Slide 14 - Agent Environment Interaction Loop

The fundamental cycle of an intelligent agent:

1. **Perceive:** Receive percepts from sensors
2. **Update state:** Incorporate new information into internal model
3. **Deliberate:** Select an action using the agent program (reflex rules, search, planning, or learning)
4. **Act:** Send commands to actuators
5. **Observe result:** Environment changes; new percepts become available
6. **Repeat:** Continue the cycle

This loop runs continuously for embodied agents (robots, autonomous vehicles) and at discrete intervals for software agents.

Text Note 11 (Robotics) describes this loop in physical systems: perception → localization → mapping → planning → manipulation → control, with closed-loop feedback.

---

## Slide 15 - Reinforcement Learning Agents

Text Note 09 extends the agent framework to learning through interaction. A reinforcement learning agent:

- Interacts with an environment through actions
- Receives reward signals as feedback
- Learns a policy (mapping from states to actions) that maximizes cumulative reward
- Balances exploration (trying new actions) with exploitation (using known-good actions)

Key RL concepts:

- **Agent:** The learner/decision-maker
- **Environment:** The world in which the agent acts
- **State:** Information about the current situation
- **Action:** A choice available to the agent
- **Reward:** Numerical feedback on outcome desirability
- **Value:** Estimated long-term usefulness of a state
- **Policy:** The strategy for choosing actions
- **Credit Assignment:** Determining which actions contributed to an outcome

RL agents are particularly useful when correct actions cannot be demonstrated in advance (no labeled data) but can be discovered through trial and error.

---

## Slide 16 - Agents in Robotics

Text Note 11 (Robotics) applies the agent framework to physical systems:

**Perception:** Cameras, stereoscopic vision, infrared depth cameras, LiDAR gather environmental information
**Localization:** The agent estimates where it is (SLAM - simultaneous localization and mapping)
**Planning:** The agent selects action sequences to achieve goals, using symbolic representations of preconditions and effects
**Manipulation:** The agent physically interacts with objects using mechanical components
**Control:** Closed-loop control uses sensor feedback to correct errors; open-loop control does not
**Proprioception:** The agent senses its own body position and movement

A robot delivering a snack must integrate localization, mapping, planning, symbolic reasoning, manipulation, control, and possibly natural language processing - demonstrating that agent intelligence requires coordination of multiple subsystems.

---

## Slide 17 - Agents and Bounded Rationality

Real agents face computational and informational constraints:

- Limited time to make decisions
- Limited memory and processing power
- Incomplete or noisy sensors
- Uncertain or changing environments

Bounded rationality means making the best decision possible within these constraints rather than computing the mathematically optimal solution.

Practical implications:

- An agent may use heuristics rather than exhaustive search
- An agent may satisfice (choose a good-enough option) rather than optimize
- An agent may act reactively when deliberation is too slow

Chapter 2 sets the stage for search algorithms (Chapters 3–7) as methods for deliberate action selection within bounded resources.

---

## Slide 18 - Multi-Agent Environments

When other intelligent agents are present, the environment becomes multi-agent. Key challenges:

- Other agents' actions affect outcomes and are themselves strategic
- Agents may cooperate, compete, or have mixed motives
- An agent must anticipate others' behavior (theory of mind, game theory)
- Equilibrium concepts (e.g., Nash equilibrium) describe stable outcomes where no agent benefits from unilaterally changing strategy

Chapter 8 (Adversarial Search) extends the agent framework to competitive settings using minimax and alpha-beta search.

Text Note 12 (AI and Game Playing) documents how agents play games against human and computer opponents, from chess to real-time strategy games.

---

## Slide 19 - Summary: Key Takeaways

1. An agent perceives through sensors and acts through actuators; the agent function maps percept histories to actions
2. PEAS (Performance, Environment, Actuators, Sensors) specifies a task environment
3. Rational agents maximize expected performance given available information; rationality ≠ omniscience
4. Agent architectures range from simple reflex to model-based, goal-based, and utility-based
5. Learning agents improve through experience using learning elements, critics, and problem generators
6. Environment properties (observable/deterministic/static/discrete/single-agent) determine appropriate algorithms
7. The vacuum world illustrates reflex and model-based agent behavior in a minimal setting
8. Utility-based agents handle trade-offs and uncertainty better than goal-based agents
9. The perception-deliberation-action loop is the core agent cycle
10. Reinforcement learning agents learn policies from reward through exploration and exploitation

---

## Slide 20 - Review Questions

1. What is an agent, and how does the agent function relate percept histories to actions?
2. What does PEAS stand for? Apply PEAS to a robotic vacuum cleaner.
3. How does rationality differ from omniscience, and why is rationality the appropriate standard for AI agents?
4. Compare simple reflex, model-based reflex, goal-based, and utility-based agents. Give an example domain for each.
5. What are the four components of a learning agent, and what does each do?
6. Name five task-environment properties and explain how each affects agent design.
7. In the vacuum world, why might a simple reflex agent loop indefinitely?
8. Why can a goal-based agent fail to choose the best among multiple goal-achieving paths?
9. How does a utility-based agent handle uncertainty differently from a goal-based agent?
10. What is the exploration-exploitation trade-off, and why is it central to reinforcement learning agents?
