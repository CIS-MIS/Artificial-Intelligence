# Artificial Intelligence - Chapter 1: Introduction to Artificial Intelligence

## Lecture Note Slides (20 Slides)

**Source Materials:** AI - Chapter 1 (textbook); AI Lecture Notes 01 (Introduction to AI); AI Lecture Notes 18 (Algorithmic Bias); AI Lecture Notes 20 (The Future of AI)

---

## Slide 1 - Introduction to Artificial Intelligence

**Artificial Intelligence: Foundations, History, and Scope**

Chapter 1 - Introduction to Artificial Intelligence

A comprehensive scholarly overview of what AI is, how it emerged, where it stands today, and the questions it raises.

---

## Slide 2 - What Is Artificial Intelligence?

Artificial Intelligence (AI) is the field of creating computer systems capable of performing tasks associated with intelligent behavior.

Key dimensions of intelligence that AI attempts to replicate:

- Perceiving and interpreting information from the environment
- Reasoning, planning, and problem-solving
- Learning from experience and data
- Understanding and generating language
- Acting autonomously in physical or virtual environments

Text Note 01 emphasizes that AI is not a single technology but a collection of approaches-from rule-based symbolic systems to data-driven neural networks-united by the goal of building systems that can act intelligently.

Chapter 1 reinforces that AI systems differ from ordinary software because they are designed to handle uncertainty, adapt to new situations, and operate without exhaustive pre-programming of every possible contingency.

---

## Slide 3 - The Turing Test and the Imitation Game

Proposed by Alan Turing in 1950, the Turing Test (originally called the "imitation game") offers an operational criterion for machine intelligence.

Setup:

- A human interrogator communicates via text with two entities: one human, one machine
- The interrogator must determine which is which
- If the machine can convince the interrogator it is human, it is said to pass the test

Scholarly significance:

- Shifts the question from "Can machines think?" (too vague) to "Can machines behave indistinguishably from humans?"
- Focuses on external behavior rather than internal consciousness
- Avoids requiring a definition of "thinking"

Limitations noted in both sources:

- Passing the test does not imply understanding, consciousness, or genuine intelligence
- A system could succeed through deception or pattern-matching without comprehension
- The test is behavioral, not epistemic

Text Note 01 connects this to the "Chinese Room" argument: a system may manipulate symbols correctly without understanding their meaning.

---

## Slide 4 - Foundations of AI

AI draws on multiple disciplines:

**Philosophy** - Questions about mind, knowledge, rationality, and the nature of intelligence
**Mathematics** - Logic, probability, computation theory, and algorithms
**Economics** - Decision theory, utility, and rational choice under uncertainty
**Neuroscience** - How biological brains produce intelligence
**Psychology** - Human cognition, perception, and learning
**Computer Engineering** - Hardware, computation, and systems design
**Linguistics** - Language structure, meaning, and processing
**Control Theory** - Feedback, stability, and autonomous systems

Chapter 1 traces how these foundations converge: philosophy asks what intelligence is, mathematics provides formal tools, computer engineering builds the machines, and psychology and neuroscience offer models of biological intelligence.

Text Note 01 adds that modern AI is increasingly interdisciplinary, combining statistical learning with insights from cognitive science and domain-specific knowledge.

---

## Slide 5 - A Brief History of AI

Major milestones in AI development:

**1940s–1950s: Origins**

- McCulloch-Pitts neuron (1943)
- Turing's "Computing Machinery and Intelligence" (1950)
- Dartmouth Conference (1956): the term "Artificial Intelligence" is coined

**1950s–1960s: Early Optimism**

- General Problem Solver (Newell, Simon, Shaw)
- Early game-playing programs (checkers, chess)
- ELIZA (early natural language system)

**1970s–1980s: First AI Winter**

- Limitations of early approaches become apparent
- Funding and enthusiasm decline

**1980s–1990s: Expert Systems and Renewed Interest**

- Knowledge-based systems for specialized domains
- Revival of neural networks (backpropagation)

**2000s–Present: The AI Revolution**

- Big data, powerful computing (GPUs), and deep learning
- Breakthroughs in vision, language, and game playing

Text Note 01 describes the "AI Revolution" as driven by three factors: large datasets, effective model architectures, and sufficient computing power.

---

## Slide 6 - The State of the Art Today

Contemporary AI capabilities include:

- Image recognition at or beyond human levels in narrow domains
- Natural language understanding and generation (translation, summarization, dialogue)
- Game playing surpassing human experts (chess, Go, poker, real-time strategy)
- Speech recognition and synthesis
- Autonomous vehicles and robotics
- Medical diagnosis support and scientific discovery assistance

Chapter 1 cautions that these capabilities are narrow: systems excel at specific tasks but do not possess general human-like intelligence.

Text Note 01 notes that modern AI systems can produce fluent, convincing output without necessarily understanding the underlying concepts-a distinction central to evaluating AI claims.

---

## Slide 7 - Types of AI: Narrow, General, and Superintelligent

**Artificial Narrow Intelligence (ANI):** Systems designed for specific tasks (e.g., image classification, language translation, game playing). All current AI systems are narrow.

**Artificial General Intelligence (AGI):** Hypothetical systems with human-level intelligence across the full range of cognitive tasks. Does not yet exist.

**Artificial Superintelligence (ASI):** Hypothetical systems exceeding human intelligence in virtually all domains. Speculative and the subject of significant debate.

Scholarly note: The boundaries between these categories are not sharp, and progress on narrow AI does not automatically imply progress toward AGI.

Text Note 20 discusses the future trajectory of AI, emphasizing that predictions about AGI timelines are highly uncertain and depend on unresolved technical and conceptual challenges.

---

## Slide 8 - Symbolic AI vs. Connectionist AI

Two dominant approaches to building intelligent systems:

**Symbolic AI (GOFAI - "Good Old-Fashioned AI"):**

- Represents knowledge using explicit symbols, facts, and logical rules
- Uses formal reasoning to draw conclusions
- Transparent and explainable
- Struggles with perception, uncertainty, and common-sense knowledge

**Connectionist AI (Neural Networks / Deep Learning):**

- Learns patterns from data by adjusting numerical parameters (weights)
- Operates on distributed, sub-symbolic representations
- Effective for perception (vision, speech, language)
- Often difficult to interpret ("black box" problem)

Text Note 10 provides extensive detail on symbolic systems: knowledge bases, propositional logic, inference, and expert systems.

Text Notes 03–05 detail connectionist approaches: neural network architecture, training, backpropagation, and evaluation.

Modern systems increasingly combine both (neuro-symbolic AI).

---

## Slide 9 - Intelligent Agents: The Unifying Concept

An intelligent agent is a system that perceives its environment through sensors and acts upon that environment through actuators to achieve its goals.

**PEAS framework** for describing an agent:

- **P**erformance measure: What defines success?
- **E**nvironment: What world does the agent operate in?
- **A**ctuators: What actions can the agent take?
- **S**ensors: What does the agent perceive?

Example: An autonomous taxi

- Performance: Safe, fast, legal, comfortable rides
- Environment: Roads, traffic, pedestrians, weather
- Actuators: Steering, accelerator, brake, signals
- Sensors: Cameras, LiDAR, GPS, speedometer

Chapter 2 develops this concept fully; Chapter 1 introduces the agent perspective as the organizing principle for the rest of the course.

---

## Slide 10 - Rational Agents and Rationality

A rational agent acts to achieve the best expected outcome given its knowledge and constraints.

Rationality ≠ omniscience: A rational agent makes the best decision it can based on the information available, not necessarily the correct decision in hindsight.

Key distinction:

- **Omniscience** would require knowing the actual outcome of every action-impossible in practice
- **Rationality** requires maximizing expected performance based on available percepts

Rationality depends on:

- The performance measure
- The agent's prior knowledge of the environment
- The actions available
- The agent's percept sequence to date

Text Note 01 connects rationality to goal-directed behavior: an intelligent system pursues objectives and selects actions likely to achieve them.

---

## Slide 11 - Agent Architectures

Chapter 1 outlines four agent types in increasing order of sophistication:

**1. Simple Reflex Agents**

- Select actions based on the current percept only
- Use condition-action rules
- Fail in partially observable environments

**2. Model-Based Reflex Agents**

- Maintain an internal model of the world
- Track aspects of the world not currently visible
- Handle partial observability better

**3. Goal-Based Agents**

- Act to achieve specific goals
- Consider future consequences of actions
- Use search and planning

**4. Utility-Based Agents**

- Choose actions that maximize a utility function
- Handle trade-offs between competing objectives
- Represent preferences over states quantitatively

Text Note 09 discusses utility and value in the context of reinforcement learning, extending the agent framework to learning from reward.

---

## Slide 12 - Task Environments: Properties and Classification

Environments differ along several dimensions that determine appropriate agent design:

- **Fully vs. partially observable:** Are all relevant aspects of the state visible?
- **Deterministic vs. stochastic:** Is the next state determined by current state and action?
- **Static vs. dynamic:** Does the environment change while the agent is deciding?
- **Discrete vs. continuous:** Are states, actions, and time distinct points or continua?
- **Single-agent vs. multi-agent:** Are other intelligent agents present?

Example contrasts:

- Crossword puzzle: single-agent, deterministic, static, discrete, fully observable
- Taxi driving: multi-agent, stochastic, dynamic, continuous, partially observable

The environment type dictates which agent architecture and algorithms are appropriate.

---

## Slide 13 - AI Applications in Practice

Real-world domains where AI is deployed:

**Healthcare:** Medical image analysis, diagnostic support, drug discovery, personalized treatment
**Finance:** Fraud detection, algorithmic trading, credit scoring, risk assessment
**Transportation:** Autonomous vehicles, route optimization, traffic management
**Entertainment:** Recommendation systems, content generation, game AI
**Manufacturing:** Predictive maintenance, robotic assembly, quality control
**Education:** Intelligent tutoring, adaptive learning, automated assessment
**Science:** Protein folding, materials discovery, climate modeling

Text Notes 03–05 document neural network applications in image recognition, healthcare, banking, and voice assistants.

Text Note 15 covers recommender systems in streaming, e-commerce, and social media.

Each application raises domain-specific questions about accuracy, safety, fairness, and accountability.

---

## Slide 14 - Ethical Considerations and Algorithmic Bias

AI systems are not neutral. They reflect the data, design choices, and objectives embedded in their development.

**Sources of bias:**

- Unrepresentative training data
- Historical inequalities encoded in data
- Incorrect or subjective labels
- Poorly chosen objectives or reward functions

**Consequences:**

- Unfair treatment of particular groups
- Reinforcement of stereotypes
- Reduced visibility for some populations
- Distorted perceptions of reality

Text Note 18 details algorithmic bias: its sources, impacts, and the need for human oversight. Text Note 19 describes bias detection and reduction methods, including a pet adoption case study.

Ethical AI requires attention to fairness, transparency, accountability, privacy, and human oversight throughout the system lifecycle.

---

## Slide 15 - The Future of AI

Text Note 20 frames the future of AI around several open questions:

- Will AI systems achieve general intelligence, and on what timeline?
- How will AI reshape work, education, and social institutions?
- Can AI be made safe, aligned with human values, and robustly beneficial?
- How should the benefits and risks of AI be distributed across society?

Emerging research directions include:

- Neuro-symbolic systems combining reasoning and learning
- Explainable and interpretable AI
- AI safety and alignment
- Human-AI collaboration and teaming
- Multimodal systems integrating vision, language, and action

The future of AI depends not only on technical progress but on societal choices about governance, deployment, and values.

---

## Slide 16 - Limitations of Current AI

Despite impressive capabilities, current AI systems face fundamental limitations:

**Narrowness:** Systems excel at specific tasks but cannot transfer knowledge broadly
**Data dependence:** Performance is bounded by the quality and scope of training data
**Interpretability:** Complex models (especially deep networks) are difficult to explain
**Robustness:** Systems can fail on inputs that differ slightly from training data
**Reasoning:** Current systems lack reliable common-sense reasoning and causal understanding
**Truthfulness:** Models can generate confident but false statements (hallucinations)

Text Note 07 emphasizes that language models learn statistical patterns without genuine understanding; fluency does not equal truth or comprehension.

Recognizing these limitations is essential for responsible deployment and for identifying where human judgment remains indispensable.

---

## Slide 17 - Human-AI Collaboration

AI does not have to replace humans. It can work alongside people, combining complementary strengths.

**AI strengths:** Processing large data, identifying patterns, rapid calculation, consistent repetition
**Human strengths:** Contextual understanding, creativity, ethical judgment, social awareness, goal-setting

Text Note 14 describes centaur chess (human + computer teams) and collaboration in medicine, engineering, customer service, and robotics.

Effective collaboration requires:

- Clear task allocation based on each party's strengths
- Explainable AI outputs that humans can evaluate
- Human oversight for consequential decisions
- Interfaces that support communication and trust

The goal is not automation for its own sake, but augmented intelligence: humans and machines achieving more together than either could alone.

---

## Slide 18 - Case Study: AI in Decision-Support Systems

Consider a bank using AI to evaluate loan applications.

The system may process thousands of applications, identify patterns associated with repayment risk, and produce risk scores.

Human loan officers must:

- Understand which factors influenced the recommendation
- Assess whether the data is accurate and representative
- Consider circumstances the model cannot capture
- Ensure compliance with law and policy
- Make or review the final decision

This case illustrates:

- Why explainability matters (Slide 14)
- Why human oversight is necessary (Slide 17)
- Why low training error does not guarantee fairness or safety (Slide 16)

Text Note 18 uses similar examples to show how bias can emerge in lending systems and how human review can mitigate it.

---

## Slide 19 - Summary: Key Takeaways

1. AI is the creation of systems that perform tasks associated with intelligent behavior
2. The Turing Test offers a behavioral criterion, not proof of understanding
3. AI draws on philosophy, mathematics, economics, neuroscience, psychology, engineering, and linguistics
4. Current AI is narrow; AGI and ASI remain hypothetical
5. Symbolic and connectionist approaches have complementary strengths and weaknesses
6. The agent perspective (PEAS, rationality, architectures) unifies the field
7. Environment properties determine appropriate agent design
8. AI is already deployed across healthcare, finance, transportation, and more
9. Ethical concerns-bias, transparency, accountability-are central to responsible AI
10. The future of AI depends on both technical advances and societal choices

---

## Slide 20 - Review Questions

1. What distinguishes AI from ordinary software systems?
2. What does the Turing Test evaluate, and what are its limitations?
3. Name three academic disciplines that contribute foundations to AI, and explain how each contributes.
4. What is the difference between narrow AI, general AI, and superintelligent AI?
5. Contrast symbolic AI with connectionist AI. Give one strength and one weakness of each.
6. What does PEAS stand for, and how is it used to describe an agent?
7. What is rationality in the agent framework, and how does it differ from omniscience?
8. Name four task-environment properties and explain why each matters for agent design.
9. What are three sources of algorithmic bias, and why does human oversight matter?
10. Why is it incorrect to equate fluent language generation with genuine understanding?
