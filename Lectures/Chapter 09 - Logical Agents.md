# Artificial Intelligence - Chapter 9: Logical Agents

## Lecture Note Slides (20 Slides)

**Source Materials:** AI - Chapter 9 (textbook); AI Lecture Notes 10 (Symbolic AI, Logic, Knowledge Bases, and Expert Systems); AI Lecture Notes 17 (Search Engines and Knowledge Bases)

---

## Slide 1 - Logical Agents

**Logical Agents: Knowledge Bases, Propositional Logic, and Knowledge-Based Reasoning**

Chapter 9 - Logical Agents

A scholarly treatment of agents that reason with explicit knowledge representations, logical inference, and the Wumpus World as a running example.

---

## Slide 2 - Knowledge-Based Agents

A knowledge-based agent maintains an internal representation of knowledge about the world and reasons about that knowledge to decide what to do.

The agent operates in a cycle:

1. **Telling:** Add new facts to the knowledge base
2. **Asking:** Query the knowledge base for information
3. **Reasoning:** Derive new conclusions from existing facts and rules
4. **Acting:** Select actions based on derived conclusions

The knowledge base (KB) is a set of sentences in a formal language. The **inference mechanism** derives new sentences from the KB. A sentence is **entailed** by the KB if it follows logically from the KB's contents.

This approach separates knowledge (what the agent knows) from reasoning (how the agent uses it) - a principle dating back to the General Problem Solver (Text Note 10).

---

## Slide 3 - The Wumpus World

The Wumpus World is a classic environment for illustrating logical agents:

- A 4×4 grid of rooms
- The agent starts at [1,1], facing right
- A Wumpus (monster) lives in one room; if the agent enters, it dies
- Pits in some rooms; falling in is fatal
- Gold in one room; grabbing it and exiting wins
- The agent senses: stench (adjacent to Wumpus), breeze (adjacent to pit), glitter (gold present), bump (walked into wall), scream (Wumpus killed)
- Actions: move, turn, grab, shoot, climb

Percepts are partial and local. The agent must use logic to infer where pits and the Wumpus are, and plan a safe route to the gold.

---

## Slide 4 - Wumpus World as a Knowledge-Based Task

The agent reasons about:

- Safe vs. unsafe squares (pits, Wumpus)
- Where the gold is
- Whether it is safe to move forward, turn, or shoot

Example reasoning:

- Stench at [1,1] means Wumpus is adjacent ([1,2] or [2,1])
- No breeze at [1,1] means [1,2] and [2,1] are pit-free
- If [2,1] is stench-free but [1,2] is not, infer Wumpus at [1,2]

This requires combining multiple percepts over time, handling uncertainty about hidden facts, and deriving conclusions not directly observed - the essence of logical reasoning.

---

## Slide 5 - Logic as a Knowledge Representation Language

Logic provides a formal language for knowledge representation with precise syntax and semantics:

**Syntax:** Which configurations of symbols constitute valid sentences
**Semantics:** The truth conditions of sentences - what makes a sentence true in a world

A sentence is **valid** (a tautology) if true under all interpretations. A sentence is **satisfiable** if true under at least one interpretation.

The key relationship is **entailment**: KB ⊨ α (KB entails sentence α) if α is true in all worlds where KB is true. Entailment is the formal basis for logical inference: if KB ⊨ α, then α can be derived from KB by sound inference rules.

---

## Slide 6 - Wumpus World Propositional Representation

Propositional symbols for the Wumpus World:

- P[i,j]: There is a pit in [i,j]
- W[i,j]: There is a Wumpus in [i,j]
- B[i,j]: There is a breeze in [i,j]
- S[i,j]: There is a stench in [i,j]
- OK[i,j]: [i,j] is safe

Known facts from percepts:

- ¬P[1,1], ¬W[1,1] (starting square is safe)
- B[1,1] (breeze at start → adjacent pit)
- ¬B[2,1] (no breeze at [2,1])

From B[1,1], the breeze rule gives: B[1,1] ↔ (P[1,2] ∨ P[2,1])
From ¬B[2,1]: ¬P[1,1] ∧ ¬P[2,2] ∧ ¬P[3,1] (neighbors of [2,1] are pit-free)

Logical inference derives: ¬P[1,2] ∧ P[2,1] - a pit at [2,1], [1,2] is safe.

---

## Slide 7 - Propositional Logic Syntax and Semantics

Propositional logic combines propositions (statements true or false) using connectives:

- **¬ (NOT):** ¬P is true iff P is false
- **∧ (AND):** P ∧ Q is true iff both P and Q are true
- **∨ (OR):** P ∨ Q is true iff at least one is true (inclusive)
- **→ (IMPLIES):** P → Q is false only when P is true and Q is false
- **↔ (IFF):** P ↔ Q is true iff P and Q have the same truth value

A **model** is an assignment of truth values to propositions. A sentence is **satisfied** by a model if it evaluates to true under that assignment. KB entails α if every model of KB is also a model of α.

Truth tables enumerate all 2ⁿ models for n propositions and systematically determine entailment.

---

## Slide 8 - Truth Tables and Entailment Checking

For n propositions, there are 2ⁿ possible models. Truth table entailment checking:

1. Enumerate all 2ⁿ models
2. Find all models where KB is true (models of KB)
3. Check whether α is true in all of them

If yes, KB ⊨ α; α is entailed. This is sound and complete but exponential O(2ⁿ) - practical only for small knowledge bases.

Example: KB = {P ∨ Q, ¬P}. Models where KB is true: {P=false, Q=true}. Does KB entail Q? Q is true in the only model → yes.

Text Note 10 provides truth tables for AND, OR, NOT, and implication, showing the exhaustive evaluation of all combinations.

---

## Slide 9 - Inference Rules and Proofs

Rather than enumerating all models, inference rules derive conclusions directly through syntactic manipulation:

**Modus Ponens:** From P and P → Q, infer Q
**And-Elimination:** From P ∧ Q, infer P
**And-Introduction:** From P and Q, infer P ∧ Q
**Or-Introduction:** From P, infer P ∨ Q
**Double-Negation Elimination:** From ¬¬P, infer P
**Unit Resolution:** From P ∨ Q and ¬P, infer Q

A **proof** is a sequence of sentences where each is either an axiom, a known fact, or derived from earlier sentences by an inference rule. The last sentence is the conclusion.

Soundness: Only entailed sentences are derivable. Completeness: All entailed sentences are derivable.

---

## Slide 10 - Resolution: A Complete Inference Rule

Resolution is a single inference rule that is complete for propositional logic:

**Resolution rule:** From (P₁ ∨ ... ∨ Pₙ) and (¬Pᵢ ∨ Q₁ ∨ ... ∨ Qₘ), infer (P₁ ∨ ... ∨ Pₙ₋₁ ∨ Pₙ₊₁ ∨ ... ∨ Q₁ ∨ ... ∨ Qₘ)

In simpler form: from (A ∨ B) and (¬B ∨ C), infer (A ∨ C).

Resolution is used in **proof by contradiction**: To prove KB ⊨ α, add ¬α to KB and try to derive a contradiction (empty clause). If contradiction follows, KB ∧ ¬α is unsatisfiable, so KB ⊨ α.

To use resolution, sentences must be in **conjunctive normal form (CNF)**: a conjunction of disjunctions of literals.

Text Note 10 covers resolution-based theorem proving and the propositional logic agent.

---

## Slide 11 - Converting to Conjunctive Normal Form

Every propositional sentence can be converted to CNF:

1. Eliminate ↔: P ↔ Q becomes (P → Q) ∧ (Q → P)
2. Eliminate →: P → Q becomes ¬P ∨ Q
3. Move ¬ inward (De Morgan's): ¬(P ∧ Q) → ¬P ∨ ¬Q; ¬(P ∨ Q) → ¬P ∧ ¬Q; ¬¬P → P
4. Distribute ∨ over ∧: (P ∧ Q) ∨ R → (P ∨ R) ∧ (Q ∨ R)

Example: (P → Q) ∧ (Q → R)
→ (¬P ∨ Q) ∧ (¬Q ∨ R) - already in CNF

Resolution operates on clauses (disjunctions of literals). A knowledge base in CNF is a set of clauses, and resolution combines pairs to derive new clauses.

---

## Slide 12 - Horn Clauses and Efficiency

A **Horn clause** is a disjunction with at most one positive literal:
(¬P₁ ∨ ¬P₂ ∨ ... ∨ ¬Pₙ ∨ Q)

Equivalently: (P₁ ∧ P₂ ∧ ... ∧ Pₙ) → Q - "if all Pᵢ, then Q"

Horn clauses are common in knowledge bases because they represent rules naturally. Inference for Horn clauses is efficient:

**Forward chaining:** Start with known facts; repeatedly apply rules whose premises are satisfied; add conclusions; stop when query derived or no new facts

**Backward chaining:** Start from the query; recursively prove its premises; succeeds if all premises provable

Horn-clause inference is linear in the size of the knowledge base - far more efficient than general resolution.

---

## Slide 13 - Forward vs. Backward Chaining

**Forward chaining (data-driven):**

- Starts from known facts in the KB
- Fires rules whose premises match known facts
- Adds conclusions as new facts
- Continues until the query is derived or no new facts can be added
- Good when many queries share the same facts

**Backward chaining (goal-driven):**

- Starts from the query (goal)
- Recursively finds rules that could conclude the query
- Proves each rule's premises as subgoals
- Depth-first search through the rule graph
- Good when few queries are asked of a large KB

Both are sound and complete for Horn clauses. Text Note 10 describes forward and backward chaining for first-order logic (Chapter 12), but the ideas apply to propositional Horn clauses too.

---

## Slide 14 - The Propositional Logic Agent

A wumpus-world agent using propositional logic:

1. **Tells** the KB its percepts and actions (e.g., B[1,1], ¬B[2,1], OK[1,1])
2. **Represents** the environment rules (breeze ↔ adjacent pit, stench ↔ adjacent wumpus)
3. **Asks** the KB: "Is [2,1] safe?" → derives ¬P[2,1] (no pit)
4. **Asks**: "Where can I move safely?" → derives OK squares
5. **Acts** by moving to a known-safe square

The agent's knowledge grows with experience. It derives conclusions (safe squares, pit locations) that were never directly perceived - inference extends perception.

Text Note 10 details the propositional logic agent and its limitations: propositional logic requires a separate symbol for every square, which does not scale to larger worlds.

---

## Slide 15 - Limitations of Propositional Logic

Propositional logic is limited because:

- It has no variables or quantifiers: each fact needs its own symbol (P[1,1], P[1,2], ...)
- It cannot express general rules like "all pits cause breezes in adjacent squares" compactly - you need one rule per square
- It cannot reason about objects and relations generally
- Knowledge bases grow large and unwieldy as worlds grow

These limitations motivate **first-order logic** (Chapters 10–11), which adds objects, relations, and quantifiers to express general knowledge economically.

Text Note 10 discusses these limitations and the transition to first-order logic.

---

## Slide 16 - Expert Systems and Symbolic AI

Logical agents are the foundation of **expert systems** (Text Note 10): knowledge-based systems that solve problems in specialized domains using explicit facts and rules.

Advantages (Text Note 10):

- **Explicit rules:** Humans can inspect and modify the knowledge base
- **Logical reasoning:** Derive conclusions by applying rules to facts
- **Explainability:** Show the facts and rules used in a conclusion
- **Consistency:** Same facts and rules produce the same results
- **No large training data needed:** Rules supplied by humans

Limitations (Text Note 10):

- **Knowledge engineering:** Encoding all relevant facts and rules is labor-intensive
- **Perception:** Difficulty with images, speech, and unstructured data
- **Uncertainty:** Classical logic is true/false; real-world situations are uncertain
- **Changing facts:** Knowledge bases need updating as the world changes
- **Common sense:** Background knowledge is hard to express as explicit rules

Modern AI combines symbolic reasoning with neural networks (neuro-symbolic AI).

---

## Slide 17 - Knowledge Bases in Search Systems

Text Note 17 connects knowledge bases to search engines:

- **Knowledge base:** Structured collection of facts and relationships (entities, predicates, objects)
- **Triple:** Subject–Predicate–Object (e.g., "Toni Morrison - wrote - The Bluest Eye")
- **Knowledge graph:** Entities as nodes, relationships as edges
- **NELL (Never-Ending Language Learning):** A system that learns facts from web pages by finding language patterns

A question-answering system transforms "Who wrote The Bluest Eye?" into a query ? - wrote - The Bluest Eye, matches "Toni Morrison - wrote - The Bluest Eye", and returns Toni Morrison.

This is logical reasoning applied to information retrieval: structured facts + query matching = direct answers rather than document lists.

---

## Slide 18 - Logical Agents and the Frame Problem

A subtle challenge for logical agents is the **frame problem**: how to represent what stays the same when an action occurs. In the Wumpus World, moving from [1,1] to [1,2] changes the agent's location but leaves pits, Wumpus, and gold untouched. In propositional logic, one must explicitly state every unchanged fact (frame axioms), which grows quadratically with the number of fluents and actions.

First-order logic (Chapters 10-12) addresses this more compactly by quantifying over objects and using successor-state axioms, but the frame problem remains a foundational issue in knowledge representation: an intelligent agent must know not only what an action changes, but also everything it leaves unchanged.

---

## Slide 19 - Summary: Key Takeaways

1. Knowledge-based agents maintain a knowledge base and reason with it via tell/ask/inference/act cycles
2. The Wumpus World illustrates reasoning under partial observability with logical inference
3. Logic provides syntax (valid sentences) and semantics (truth conditions); entailment KB ⊨ α means α follows from KB
4. Propositional logic uses propositions and connectives (¬, ∧, ∨, →, ↔); models assign truth values
5. Truth-table entailment is sound and complete but exponential O(2ⁿ)
6. Inference rules (Modus Ponens, And-Elimination, Resolution) derive conclusions syntactically
7. Resolution is complete for propositional logic and operates on CNF sentences; proof by contradiction derives unsatisfiability
8. Horn clauses enable efficient linear-time forward and backward chaining
9. The propositional logic agent derives safe moves in the Wumpus World but does not scale due to lack of variables/quantifiers
10. Expert systems embody logical agents but face knowledge engineering, perception, uncertainty, and common-sense limitations

---

## Slide 20 - Review Questions

1. What is a knowledge-based agent, and what is its perception-reasoning-action cycle?
2. Describe the Wumpus World environment and the kinds of inferences an agent must make.
3. What is entailment (KB ⊨ α), and how does it relate to models?
4. List the propositional connectives and give the truth condition for implication.
5. Why is truth-table entailment checking exponential, and what is the alternative?
6. State the resolution rule and explain how proof by contradiction uses it.
7. What is CNF, and why is resolution restricted to CNF sentences?
8. What is a Horn clause, and why does it enable efficient inference?
9. Contrast forward chaining and backward chaining. When is each preferable?
10. What are three limitations of propositional logic, and how does first-order logic address them?
11. What are two advantages and two limitations of expert systems (Text Note 10)?
12. How does a knowledge base differ from an inverted index (Text Note 17)?
