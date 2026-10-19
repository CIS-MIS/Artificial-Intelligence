# Artificial Intelligence - Chapter 10: Propositional Logic

## Lecture Note Slides (20 Slides)

**Source Materials:** AI - Chapter 10 (textbook); AI Lecture Notes 10 (Symbolic AI, Logic, Knowledge Bases, and Expert Systems)

---

## Slide 1 - Propositional Logic

**Propositional Logic: Syntax, Semantics, Inference, and Theorem Proving**

Chapter 10 - Propositional Logic

A scholarly treatment of propositional logic as a formal reasoning system: syntax, semantics, truth tables, inference rules, resolution, and its use in knowledge-based agents.

---

## Slide 2 - Propositional Logic: Purpose and Scope

Propositional logic is the simplest formal logic. It reasons about propositions - statements that are either true or false - using logical connectives.

It is closely related to Boolean logic, which underlies digital circuit design and computer science.

Propositional logic serves as:

- A foundation for more expressive logics (first-order logic, Chapters 11–12)
- A model for knowledge-based reasoning with clear syntax and semantics
- A testbed for inference algorithms (resolution, theorem proving)

It is **propositional** because its atomic units are whole propositions, not objects, properties, or relations. It cannot express "all squares are breezy" or "the Wumpus is in some square" - those require first-order logic (Chapters 11–12).

---

## Slide 3 - Syntax: Propositions and Connectives

**Syntax** defines which arrangements of symbols form valid sentences.

Atomic propositions: P, Q, R, ... (each represents a statement like "the square [1,1] contains a pit")

Logical connectives:

- **¬ (NOT):** ¬P - negation
- **∧ (AND):** P ∧ Q - conjunction
- **∨ (OR):** P ∨ Q - disjunction (inclusive)
- **→ (IMPLIES):** P → Q - implication
- **↔ (IFF):** P ↔ Q - biconditional

Sentences are built recursively:

- Every proposition is a sentence
- If P is a sentence, ¬P is a sentence
- If P, Q are sentences, (P ∧ Q), (P ∨ Q), (P → Q), (P ↔ Q) are sentences

Parentheses remove ambiguity; precedence conventions apply when omitted.

---

## Slide 4 - Semantics: Models and Truth

**Semantics** specifies what makes a sentence true.

A **model** (or interpretation) assigns a truth value (TRUE/FALSE, or 1/0) to each proposition. With n propositions, there are 2ⁿ models.

Truth conditions for connectives:

- ¬P: true iff P is false
- P ∧ Q: true iff both P and Q are true
- P ∨ Q: true iff at least one is true
- P → Q: false iff P true and Q false; true otherwise
- P ↔ Q: true iff P and Q have the same truth value

A sentence is **satisfied by** (true in) a model under these rules. A set of sentences is **satisfiable** if some model satisfies all of them.

---

## Slide 5 - Truth Tables

A truth table lists all 2ⁿ models and the truth value of a sentence under each.

For P ∧ Q:

| P | Q | P ∧ Q |
| - | - | ------ |
| T | T | T      |
| T | F | F      |
| F | T | F      |
| F | F | F      |

For P → Q:

| P | Q | P → Q |
| - | - | ------ |
| T | T | T      |
| T | F | F      |
| F | T | T      |
| F | F | T      |

Note: P → Q is true when P is false (vacuously true). This is a common source of confusion but is essential for logical consistency.

Text Note 10 provides truth tables for AND, OR, NOT, and implication with the car example (P = car is smelly, Q = car is old, R = John-Green-bot drives car).

---

## Slide 6 - Validity, Satisfiability, and Entailment

Key semantic concepts:

- **Valid sentence (tautology):** True in all models (e.g., P ∨ ¬P)
- **Unsatisfiable sentence (contradiction):** False in all models (e.g., P ∧ ¬P)
- **Contingent sentence:** True in some models, false in others

**Entailment:** KB ⊨ α ("KB entails α") means α is true in every model where KB is true.

Entailment is the central relation in logical reasoning: if the knowledge base is true, then α must be true. It generalizes implication: {P, P → Q} ⊨ Q.

Text Note 10 emphasizes entailment as the criterion for whether conclusions follow from premises.

---

## Slide 7 - Model Checking via Truth Tables

To check KB ⊨ α using truth tables:

1. Enumerate all 2ⁿ models
2. Identify models satisfying KB
3. Verify α is true in all those models

If yes, entailment holds. This is **sound** (only derives true conclusions) and **complete** (derives all entailed conclusions) but **exponential** O(2ⁿ) - practical only for small propositional vocabularies.

Example: KB = {P ∨ Q, ¬P}. The only model satisfying KB is P=F, Q=T. Does KB ⊨ Q? Q=T in that model → yes.

Truth-table model checking establishes the theoretical foundation but motivates more efficient inference methods.

---

## Slide 8 - Inference Rules: From Semantics to Syntax

Rather than enumerating models, **inference rules** derive conclusions through syntactic manipulation:

**Modus Ponens:** From P and P → Q, infer Q
**And-Elimination (∧E):** From P ∧ Q, infer P (and Q)
**And-Introduction (∧I):** From P and Q, infer P ∧ Q
**Or-Introduction (∨I):** From P, infer P ∨ Q (for any Q)
**Double-Negation Elimination:** From ¬¬P, infer P

**Unit Resolution:** From P ∨ Q and ¬P, infer Q

A **proof** is a finite sequence of sentences where each is a premise or derived from earlier sentences via an inference rule; the final sentence is the conclusion.

Soundness: every derivable sentence is entailed. Completeness: every entailed sentence is derivable.

---

## Slide 9 - Example Proof with Inference Rules

Knowledge base:

1. P ∨ Q (either P or Q)
2. ¬P (not P)

Goal: Prove Q

Proof:

1. P ∨ Q (premise)
2. ¬P (premise)
3. Q - Unit Resolution from (1) and (2): resolve P ∨ Q with ¬P on P → Q

Alternatively:

1. P ∨ Q
2. ¬P
3. Assume ¬Q (proof by contradiction)
4. ¬P ∧ ¬Q (∧I from 2, 3)
5. ¬(P ∨ Q) (De Morgan from 4)
6. Contradiction with (1)
7. Therefore Q

Both approaches derive Q, showing Q is entailed by KB.

---

## Slide 10 - Resolution: A Complete Inference Rule

**Resolution** is a single, powerful inference rule complete for propositional logic:

From clause C₁ = (L₁ ∨ ... ∨ Lₙ ∨ P) and clause C₂ = (M₁ ∨ ... ∨ Mₘ ∨ ¬P), infer the **resolvent** (L₁ ∨ ... ∨ Lₙ ∨ M₁ ∨ ... ∨ Mₘ)

Simplest case: from (A ∨ B) and (¬B ∨ C), infer (A ∨ C)

Resolution works on **clauses** - disjunctions of literals (propositions or their negations). A knowledge base in **conjunctive normal form (CNF)** is a conjunction of clauses, treated as a set of clauses.

Proof by contradiction with resolution: To show KB ⊨ α, add ¬α to KB and derive the empty clause (contradiction). If derivable, KB ∧ ¬α is unsatisfiable, hence KB ⊨ α.

---

## Slide 11 - Converting to Conjunctive Normal Form (CNF)

Every propositional sentence can be converted to CNF (a conjunction of disjunctions of literals):

1. **Eliminate ↔:** (P ↔ Q) → (P → Q) ∧ (Q → P)
2. **Eliminate →:** (P → Q) → (¬P ∨ Q)
3. **Move ¬ inward (De Morgan's + double negation):**
   - ¬(P ∧ Q) → ¬P ∨ ¬Q
   - ¬(P ∨ Q) → ¬P ∧ ¬Q
   - ¬¬P → P
4. **Distribute ∨ over ∧:** (A ∧ B) ∨ C → (A ∨ C) ∧ (B ∨ C)

Example: Convert (P → Q) ∧ R
→ (¬P ∨ Q) ∧ R - already CNF

Example: Convert (P ∨ Q) → R
→ ¬(P ∨ Q) ∨ R
→ (¬P ∧ ¬Q) ∨ R
→ (¬P ∨ R) ∧ (¬Q ∨ R) - CNF

---

## Slide 12 - Resolution Algorithm

Resolution-based theorem proving:

```
function PL-RESOLUTION(KB, α) returns true/false
    clauses ← CNF(KB ∧ ¬α)      // convert KB and negation of query to clauses
    new ← ∅
    loop do
        for each pair of clauses Ci, Cj in clauses do
            resolvents ← RESOLVE(Ci, Cj)
            if empty clause in resolvents then return true   // contradiction found
            new ← new ∪ resolvents
        if new ⊆ clauses then return false   // no new clauses → α not entailed
        clauses ← clauses ∪ new
```

The algorithm is **sound** (returns true only when entailed) and **complete** (returns true whenever entailed), terminating because there are finitely many distinct clauses over a finite proposition vocabulary.

Text Note 10 describes resolution-based theorem proving for the propositional logic agent.

---

## Slide 13 - Example: Resolution Proof

KB: {B[1,1] ↔ (P[1,2] ∨ P[2,1]), ¬B[2,1], ¬P[1,1]}
Query: P[2,1] (is there a pit at [2,1]?)

Convert to CNF and add ¬P[2,1]. Resolution steps derive the empty clause, proving KB ⊨ P[2,1].

The derivation combines:

- Breeze definition: (¬B[1,1] ∨ P[1,2] ∨ P[2,1]) ∧ (¬P[1,2] ∨ B[1,1]) ∧ (¬P[2,1] ∨ B[1,1])
- Known: B[1,1], ¬B[2,1]
- Negated query: ¬P[2,1]

Resolving ¬B[2,1] with (¬P[1,1] ∨ ¬P[2,2] ∨ ¬P[3,1] ∨ B[2,1]) yields pit-free neighbors of [2,1]. Combined with B[1,1], this forces P[2,1].

The empty clause emerges, confirming the entailment.

---

## Slide 14 - Efficiency and Limitations of Resolution

Resolution is complete but can be inefficient:

- The number of possible clauses over n propositions is 3ⁿ (each proposition: positive, negative, absent)
- Resolution may generate many clauses before finding contradiction or exhausting possibilities

Improvements:

- **Unit preference:** Resolve clauses of size 1 first (unit resolution)
- **Set of support:** Focus resolution on clauses related to the query
- **Subsumption:** Remove clauses subsumed by others (if C₁ ⊆ C₂, drop C₂)
- **Pure literal elimination:** Remove clauses containing a literal whose negation never appears

Despite improvements, propositional resolution is exponential in the worst case. This motivates Horn-clause methods (linear time) and first-order logic with more scalable inference.

---

## Slide 15 - Horn Clauses and Forward/Backward Chaining

A **Horn clause** has at most one positive literal:
(¬P₁ ∨ ¬P₂ ∨ ... ∨ ¬Pₙ ∨ Q) ≡ (P₁ ∧ P₂ ∧ ... ∧ Pₙ) → Q

Horn clauses represent rules naturally ("if premises, then conclusion"). Inference is efficient:

**Forward chaining:**

1. Start with known facts (positive literals)
2. Find rules whose all premises are known
3. Add their conclusions as new facts
4. Repeat until query derived or no new facts

**Backward chaining:**

1. Start from the query
2. Find rules whose conclusion matches the query
3. Recursively prove each rule's premises
4. Succeed if all premises provable

Both are sound and complete for Horn KBs and run in linear time - far better than general resolution.

---

## Slide 16 - Forward vs. Backward Chaining: Comparison

|             | Forward Chaining                          | Backward Chaining                      |
| ----------- | ----------------------------------------- | -------------------------------------- |
| Direction   | Data-driven (facts → conclusions)        | Goal-driven (query → premises)        |
| Starts from | Known facts in KB                         | The query to prove                     |
| Search      | Breadth-first through rules               | Depth-first through subgoals           |
| Best when   | Many queries, few facts                   | Few queries, large KB                  |
| Example use | Deriving all conclusions from sensor data | Proving a specific diagnostic question |

Text Note 10 describes both for first-order logic (Chapter 12); the propositional versions are simpler instances of the same ideas.

---

## Slide 17 - The Propositional Logic Agent

A wumpus-world agent built on propositional logic:

1. **Tells** the KB percepts: B[1,1] (breeze at start), ¬B[2,1] (no breeze at [2,1]), OK[1,1]
2. **Tells** the KB domain rules: B[i,j] ↔ (P[i-1,j] ∨ P[i+1,j] ∨ P[i,j-1] ∨ P[i,j+1])
3. **Asks** the KB: Is [2,1] pit-free? → derives ¬P[2,1] via resolution/forward chaining
4. **Asks**: Which neighbors are safe? → derives OK squares
5. **Acts**: Move to a known-safe square

The agent's KB grows as it explores. Each new percept is added; new conclusions are derived. Inference extends perception beyond what is directly observed.

Limitation: Propositional logic needs a separate symbol per square (P[1,1], P[1,2], ...), so KBs grow quadratically with world size and cannot express general rules compactly.

---

## Slide 18 - Propositional Logic in Expert Systems

Text Note 10 connects propositional logic to expert systems:

- Knowledge base contains facts and rules in logical form
- Inference derives conclusions via rule application (forward/backward chaining)
- Explainability: show which rules and facts supported a conclusion
- Example: loan evaluation rules (credit_score ∧ income → eligible)

Limitations carried into expert systems:

- Knowledge engineering is labor-intensive
- Uncertainty is not represented (true/false only)
- Changing facts require KB updates
- Common-sense knowledge is hard to encode

Modern systems combine symbolic logic with neural networks (neuro-symbolic AI).

---

## Slide 19 - Summary: Key Takeaways

1. Propositional logic reasons about propositions (true/false statements) using connectives ¬, ∧, ∨, →, ↔
2. Semantics is defined via models (truth assignments); 2ⁿ models for n propositions
3. Validity = true in all models; unsatisfiability = false in all models; entailment KB ⊨ α = α true in all KB-models
4. Truth-table model checking is sound and complete but exponential O(2ⁿ)
5. Inference rules (Modus Ponens, ∧E, ∧I, ∨I, Unit Resolution) derive conclusions syntactically
6. Resolution is a complete inference rule operating on clauses in CNF; proof by contradiction derives the empty clause
7. CNF conversion: eliminate ↔ and →, move ¬ inward, distribute ∨ over ∧
8. Horn clauses (≤1 positive literal) enable linear-time forward and backward chaining
9. The propositional logic agent derives safe Wumpus World moves but does not scale (no variables/quantifiers)
10. Propositional logic underlies expert systems but faces uncertainty, scaling, and common-sense limitations

---

## Slide 20 - Review Questions

1. What is the difference between syntax and semantics in propositional logic?
2. How many models exist for n propositions, and what does each model represent?
3. Construct truth tables for ¬P, P ∧ Q, P ∨ Q, P → Q, and P ↔ Q.
4. Define entailment (KB ⊨ α) in terms of models. Is P ∨ Q entailed by {P ∨ Q, ¬P}?
5. What makes a sentence valid, unsatisfiable, or contingent?
6. State Modus Ponens and Unit Resolution. Give an example of each.
7. Explain proof by contradiction using resolution: how does adding ¬α to KB test entailment?
8. What is CNF, and list the four steps to convert a sentence to CNF.
9. Convert (P ∨ Q) → R to CNF, showing each step.
10. What is a Horn clause, and why do forward/backward chaining run in linear time on Horn KBs?
11. Contrast forward chaining and backward chaining with an example domain.
12. Why doesn't propositional logic scale to large Wumpus Worlds, and what logic addresses this?
