# Artificial Intelligence - Chapter 12: First-Order Logic II

## Lecture Note Slides (20 Slides)

**Source Materials:** AI - Chapter 12 (textbook); AI Lecture Notes 10 (Symbolic AI, Logic, Knowledge Bases, and Expert Systems); AI Lecture Notes 17 (Search Engines and Knowledge Bases)

---

## Slide 1 - First-Order Logic II: Inference, Unification, Resolution, and Logic Programming

**First-Order Logic II: Inference, Unification, Resolution, and Logic Programming**

Chapter 12 - First-Order Logic

A scholarly treatment of FOL inference methods: forward/backward chaining, resolution, unification, logic programming (Prolog), and knowledge engineering.

---

## Slide 2 - From FOL Syntax to FOL Inference

Chapter 11 introduced FOL syntax and semantics. Chapter 12 addresses how to **do inference** in FOL - deriving entailed conclusions from a knowledge base.

Key challenge: FOL entailment is semidecidable. If KB ⊨ α, a proof exists and can in principle be found; if KB ⊭ α, the search may never terminate.

Inference approaches:

1. **Reduce FOL to propositional logic** via instantiation (propositionalization) - complete but potentially infinite
2. **Native FOL inference** using unification - generalized modus ponens, forward/backward chaining
3. **Resolution with unification** - a single complete inference rule for FOL
4. **Logic programming (Prolog)** - backward chaining as computation

---

## Slide 3 - Propositionalization and Its Limits

**Propositionalization:** Replace FOL sentences with propositional instances by:

- Universal instantiation: ∀ x P(x) → P(A) for all ground terms A
- Existential instantiation: ∃ x P(x) → P(c) for a new constant c

Then apply propositional inference (resolution, truth tables).

**Herbrand's theorem:** If a set of FOL sentences is unsatisfiable, there is a finite unsatisfiable propositional subset of its Herbrand base (ground terms built from constants/functions in the KB).

**Problem:** The Herbrand base may be infinite (e.g., with functions: John, Father(John), Father(Father(John)), ...). Propositionalization may never terminate even when a proof exists.

This motivates native FOL inference that avoids full propositionalization.

---

## Slide 4 - Unification: Matching Terms with Variables

Unification finds a substitution making two expressions identical:

UNIFY(P(x), P(A)) = {x/A}
UNIFY(Knows(John, x), Knows(y, Bill)) = {x/Bill, y/John}
UNIFY(Father(x), Father(John)) = {x/John}
UNIFY(Father(x), x) = FAIL (occurs check)
UNIFY(Older(Father(x), y), Older(x, x)) = FAIL (occurs check on x)

Properties:

- A **unifier** is a substitution making expressions identical
- A **most general unifier (MGU)** is unique up to renaming and is the least committing unifier
- Unification occurs in linear time for most practical cases

Unification is the core matching mechanism enabling FOL inference without full propositionalization.

---

## Slide 5 - Generalized Modus Ponens (GMP)

GMP lifts propositional Modus Ponens to FOL:

Given:

- Atomic sentences P₁′, ..., Pₙ′ (facts)
- Rule (P₁ ∧ ... ∧ Pₙ) → Q

If substitution θ unifies Pᵢ′ = Pᵢ for all i (i.e., Pᵢ′θ = Pᵢθ), infer Qθ.

Example:
Facts: King(John), Greedy(John)
Rule: ∀ x (King(x) ∧ Greedy(x) → Evil(x))
MGU: θ = {x/John}
Conclusion: Evil(John)

GMP is sound and complete for **definite clause knowledge bases** (clauses with exactly one positive literal - Horn clauses in FOL).

---

## Slide 6 - Forward Chaining in FOL

**Forward chaining (data-driven):**

1. Start with known ground facts in the KB
2. Use GMP with unification to find rules whose premises unify with known facts
3. Add rule conclusions as new facts
4. Repeat until the query is derived or no new facts can be added

Example (kinship):
Facts: Parent(Richard, John), Male(Richard)
Rule: ∀ x, y (Parent(x, y) ∧ Male(x) → Father(x, y))
Unify: x→Richard, y→John
Derive: Father(Richard, John)

Properties:

- Sound and complete for definite clauses
- Derives all entailed facts (may be infinite)
- Forward chaining is incremental: new facts trigger new rule firings

Text Note 10 describes forward chaining for FOL with kinship examples.

---

## Slide 7 - Backward Chaining in FOL

**Backward chaining (goal-driven):**

1. Start from the query (goal)
2. Find rules whose conclusion unifies with the query
3. For each such rule, recursively prove each premise as a subgoal
4. Succeed if all premises provable; backtrack on failure

Example: Query Father(Richard, John)

- Find rule: Parent(x, y) ∧ Male(x) → Father(x, y)
- Unify conclusion with query: x→Richard, y→John
- Subgoals: Parent(Richard, John), Male(Richard)
- Both are known facts → query succeeds

Properties:

- Sound and complete for definite clauses
- Depth-first with backtracking; may loop on recursive rules without loop checking
- Goal-focused: only explores rules relevant to the query

---

## Slide 8 - Forward vs. Backward Chaining (FOL)

|                | Forward Chaining                                       | Backward Chaining                                |
| -------------- | ------------------------------------------------------ | ------------------------------------------------ |
| Direction      | Data-driven (facts → conclusions)                     | Goal-driven (query → subgoals)                  |
| Starting point | Known facts                                            | The query                                        |
| Search pattern | Breadth-first through rule firings                     | Depth-first through subgoals                     |
| Best for       | Many queries over same facts; deriving all conclusions | Few specific queries over large KB               |
| Risk           | May derive irrelevant facts                            | May loop on recursive rules; needs loop checking |

Text Note 10 recommends backward chaining for diagnostic/query tasks and forward chaining for monitoring/diagnosis streams.

---

## Slide 9 - Resolution: A Complete Inference Rule for FOL

**FOL Resolution** extends propositional resolution with unification:

From clauses:

- C₁ = (L₁ ∨ ... ∨ Lₙ ∨ P)
- C₂ = (M₁ ∨ ... ∨ Mₘ ∨ ¬Q)

If P and Q have MGU θ, infer the resolvent: (L₁ ∨ ... ∨ Lₙ ∨ M₁ ∨ ... ∨ Mₘ)θ

Example:
C₁: ¬King(x) ∨ Greedy(x) ∨ Evil(x)
C₂: King(John)
MGU: {x/John}
Resolvent: Greedy(John) ∨ Evil(John)

**Resolution is refutation-complete for FOL:** To prove KB ⊨ α, add ¬α and derive the empty clause (contradiction).

Resolution subsumes GMP: forward/backward chaining can be simulated by resolution with appropriate strategies.

---

## Slide 10 - Converting FOL to Conjunctive Normal Form (CNF)

Resolution requires sentences in CNF. FOL CNF conversion:

1. Eliminate ↔ and →
2. Move ¬ inward (De Morgan's, quantifier negation: ¬∀ x P → ∃ x ¬P, ¬∃ x P → ∀ x ¬P)
3. Standardize variables apart (rename variables so each quantifier uses a unique variable)
4. **Skolemization:** Eliminate existential quantifiers:
   - ∃ x P(x) → P(c) where c is a new constant (Skolem constant)
   - ∀ x ∃ y P(x, y) → ∀ x P(x, f(x)) where f is a new function (Skolem function)
5. Drop universal quantifiers (assume all remaining variables universally quantified)
6. Distribute ∨ over ∧

Example: ∀ x (King(x) → ∃ y (Father(y, x)))
→ ¬King(x) ∨ Father(f(x), x) after Skolemization

Skolemization preserves satisfiability (not validity) - suitable for refutation proofs.

---

## Slide 11 - FOL Resolution Algorithm

```
function FOL-RESOLUTION(KB, α) returns true/false
    clauses ← CNF(KB ∧ ¬α)
    new ← ∅
    loop do
        for each pair Ci, Cj in clauses do
            for each literal Pi in Ci, Qj in Cj do
                if UNIFY(Pi, ¬Qj) succeeds with θ then
                    resolvent ← (subst θ of union minus complementary pair)
                    if resolvent is empty clause then return true
                    new ← new ∪ {resolvent}
        if new ⊆ clauses then return false
        clauses ← clauses ∪ new
```

Complete but potentially infinite. Strategies to improve:

- **Unit preference:** resolve unit clauses first
- **Set of support:** resolve only clauses related to the query
- **Subsumption:** remove clauses subsumed by others
- **Input resolution:** resolve each new clause with an original KB clause

---

## Slide 12 - Resolution Proof Example

KB: {∀ x (King(x) → Evil(x)), King(John)}
Query: Evil(John)

CNF:

- ¬King(x) ∨ Evil(x)
- King(John)
- ¬Evil(John) (negated query)

Resolution:

1. Resolve ¬King(x) ∨ Evil(x) with King(John), MGU {x/John} → Evil(John)
2. Resolve Evil(John) with ¬Evil(John) → empty clause

Contradiction derived → KB ⊨ Evil(John).

This mirrors generalized modus ponens but uses the uniform resolution machinery.

---

## Slide 13 - Logic Programming and Prolog

**Logic programming** treats computation as logical deduction. Prolog (Programmation en Logique) is the canonical language.

A Prolog program is a set of definite clauses:

- Facts: parent(richard, john).
- Rules: father(X, Y) :- parent(X, Y), male(X). (means: parent(X,Y) ∧ male(X) → father(X,Y))

Execution uses **backward chaining with unification**:

- Query: ?- father(richard, john).
- Prolog unifies the query with rule heads, proves subgoals depth-first, backtracks on failure

Prolog features:

- **Unification** for pattern matching
- **Backtracking** for search
- **Cut (!)** to prune search (non-logical control)
- **Negation as failure:** not(P) succeeds if P cannot be proved (not true negation)

Prolog is declarative: the programmer states what is true, not how to compute it.

---

## Slide 14 - Prolog Execution Example

Program:

```
parent(richard, john).
parent(john, robert).
male(richard). male(john).
father(X, Y) :- parent(X, Y), male(X).
grandfather(X, Z) :- father(X, Y), father(Y, Z).
```

Query: ?- grandfather(richard, Z).

1. Unify with grandfather(X,Z): X→richard
2. Subgoals: father(richard, Y), father(Y, Z)
3. father(richard, Y) → parent(richard, Y), male(richard) → Y→john
4. father(john, Z) → parent(john, Z), male(john) → Z→robert
5. Answer: Z = robert

Prolog returns all solutions via backtracking on request.

---

## Slide 15 - Knowledge Engineering in FOL

Knowledge engineering is the process of building a knowledge base. Steps (Text Note 10):

1. **Identify the task:** What questions must the KB answer?
2. **Assemble relevant knowledge:** What facts and rules are needed?
3. **Decide on a vocabulary:** Choose predicates, functions, constants
4. **Encode general knowledge:** Write axioms for the domain
5. **Encode specific instances:** Add facts about particular objects
6. **Pose queries:** Test whether the KB answers questions correctly
7. **Debug and revise:** Fix errors and gaps

Example: electronic circuits domain - encode components, connections, signal behavior; query whether output is correct given inputs.

Pitfalls:

- Using the wrong predicate arity
- Confusing ∀ with → vs. ∀ with ∧
- Confusing ∃ with ∧ vs. ∃ with →
- Forgetting uniqueness or exclusion axioms

---

## Slide 16 - Limits of FOL Inference

FOL inference has fundamental limits:

1. **Semidecidability:** If KB ⊨ α, a proof exists; if KB ⊭ α, search may not terminate (Church-Turing)
2. **Computational cost:** FOL resolution can be extremely expensive; even propositional resolution is exponential
3. **No uncertainty:** FOL cannot express "probably," "typically," or "by default"
4. **No reasoning about ignorance:** Cannot easily represent "we don't know whether P"
5. **Frame problem:** Representing what changes and what stays the same over time is cumbersome in pure FOL

These limits motivate:

- **Probabilistic reasoning** (Chapters 13-14) for uncertainty
- **Non-monotonic logic** and default reasoning for typicality
- **Temporal/logic of action** for change over time

---

## Slide 17 - FOL in Knowledge Bases and Question Answering

FOL provides the formal foundation for structured knowledge bases and question-answering systems (Text Note 17). A knowledge base stores facts as triples (subject, predicate, object), and a question-answering system translates a natural-language question into a logical query over those triples.

For example, "Who wrote The Bluest Eye?" becomes the query ∃ x (Wrote(x, TheBluestEye)), which the KB answers by matching the stored fact Wrote(ToniMorrison, TheBluestEye). This is logical inference applied to information retrieval: structured facts plus query matching yield direct answers rather than document lists.

The limitation is that real-world knowledge is vast, uncertain, and constantly changing - challenges that purely logical knowledge bases struggle to handle without probabilistic extensions.

---

## Slide 18 - From FOL to Probabilistic Logic

FOL's inability to represent uncertainty is its most significant practical limitation. Real-world knowledge is rarely certain: "birds usually fly" has exceptions, and sensor readings are noisy. Probabilistic logic extends FOL by attaching probabilities to formulas, allowing statements like "P(Fly(x) | Bird(x)) = 0.95."

Markov logic networks and probabilistic soft logic combine FOL-style weighted formulas with probabilistic inference. These hybrid systems retain the expressiveness of first-order logic while handling uncertainty, bridging the symbolic and statistical traditions in AI. Chapters 13-14 develop the probabilistic foundations these methods build on.

---

## Slide 19 - Summary: Key Takeaways

1. FOL entailment is semidecidable; inference may not terminate when the query is not entailed
2. Propositionalization via instantiation is complete but may never terminate (infinite Herbrand base)
3. Unification finds MGUs making expressions identical; it is the core matching operation in FOL inference
4. Generalized Modus Ponens applies propositional Modus Ponens to FOL via unification; complete for definite clauses
5. Forward chaining (data-driven) derives all entailed facts; backward chaining (goal-driven) proves specific queries
6. FOL resolution is refutation-complete and subsumes chaining methods
7. CNF conversion for FOL requires Skolemization to eliminate existential quantifiers
8. Prolog implements logic programming via backward chaining, unification, and backtracking
9. Knowledge engineering follows a disciplined process with common pitfalls (quantifier/connective pairing)
10. FOL inference limits (semidecidability, cost, no uncertainty) motivate probabilistic and non-monotonic extensions

---

## Slide 20 - Review Questions

1. What is propositionalization, and why might it fail to terminate even when a proof exists?
2. What does Herbrand's theorem state about unsatisfiable FOL sentence sets?
3. Define unification and MGU. When does the occurs check cause unification to fail?
4. State Generalized Modus Ponens and give an FOL example.
5. Trace forward chaining: from Parent(Richard, John), Male(Richard), and ∀ x,y(Parent(x,y) ∧ Male(x) → Father(x,y)), what is derived?
6. Trace backward chaining for query Father(Richard, John) with the same knowledge.
7. Contrast forward and backward chaining in FOL: when is each preferable?
8. State the FOL resolution rule and explain how unification is integrated.
9. What is Skolemization, and why does it preserve satisfiability (not validity)?
10. Convert ∀ x ∃ y (Father(y, x)) to CNF, showing Skolemization.
11. How does Prolog execute a query? Describe unification, backtracking, and negation as failure.
12. What are three limits of FOL inference, and what AI approaches address them?
