# Homework 06: Logical Reasoning - Propositional and First-Order Logic

**Chapters:** 9–12 (Logical Agents, Propositional Logic, First-Order Logic I & II)
**Estimated time:** 3–4 hours
**Total points:** 100

---

## Instructions

Answer all questions thoroughly. For logic derivations, show each step and cite the inference rule used (e.g., Modus Ponens, Resolution, Universal Instantiation). For translations, use clear notation and define your symbols. Submissions should be typed, with question numbers clearly labeled.

---

## Part A: Propositional Logic (Chapters 9–10) - 50 points

### Question 1: Wumpus World Propositional Reasoning (20 points)

Consider a 2x2 Wumpus World with squares [1,1], [1,2], [2,1], [2,2]. The agent starts at [1,1]. Define propositional symbols:

- P[i,j]: There is a pit in [i,j]
- B[i,j]: There is a breeze in [i,j]
- OK[i,j]: [i,j] is safe

The agent perceives: B[1,1] (breeze at start), ¬B[2,1] (no breeze at [2,1]), ¬P[1,1] (start is safe), ¬P[2,1] (known safe). The domain rule for a 2x2 grid is:

B[1,1] ↔ (P[1,2] ∨ P[2,1])
B[2,1] ↔ (P[1,1] ∨ P[2,2])

(a) Convert the domain rules and known facts into conjunctive normal form (CNF). Show each conversion step (eliminate ↔, eliminate →, move ¬ inward, distribute ∨ over ∧). (10 points)

(b) Using resolution, prove that P[1,2] is entailed by the knowledge base. That is, add ¬P[1,2] to the KB and derive the empty clause. Show each resolution step and the most general unifier (here, simple matching) used. (10 points)

### Question 2: Entailment and Inference Rules (15 points)

(a) Define entailment (KB ⊨ α) in terms of models. (5 points)

(b) State Modus Ponens and Unit Resolution. Give a concrete example of each using propositions P and Q. (5 points)

(c) Explain why truth-table entailment checking is sound and complete but exponential. State the complexity in terms of the number of propositions n. (5 points)

### Question 3: Horn Clauses and Chaining (15 points)

(a) What is a Horn clause? Write a Horn clause in both disjunctive form and implication form ("if premises, then conclusion"). (5 points)

(b) Describe forward chaining. When is it preferable to backward chaining? (5 points)

(c) Describe backward chaining. When is it preferable to forward chaining? (5 points)

---

## Part B: First-Order Logic (Chapters 11–12) - 50 points

### Question 4: Syntax and Semantics of FOL (15 points)

(a) Distinguish among constant symbols, predicate symbols, function symbols, and variables, giving one example of each. (6 points)

(b) Translate the following English sentences into FOL. Define your vocabulary clearly.

- (i) Every king is a person. (2 points)
- (ii) Richard has a brother. (2 points)
- (iii) A square is breezy if and only if it is adjacent to a pit. (3 points)

(c) Explain why ∀ typically pairs with → and ∃ typically pairs with ∧. What goes wrong if you write ∃ x (King(x) → Person(x))? (5 points)

### Question 5: Unification and Generalized Modus Ponens (15 points)

(a) What is unification? What is a most general unifier (MGU)? When does the occurs check cause unification to fail? (6 points)

(b) Compute the MGU, if one exists, for each pair:

- (i) Knows(John, x) and Knows(y, Bill) (2 points)
- (ii) Father(x) and Father(John) (2 points)
- (iii) Father(x) and x (2 points)

(c) Apply Generalized Modus Ponens: given facts King(John) and Greedy(John), and rule ∀ x (King(x) ∧ Greedy(x) → Evil(x)), what conclusion follows, and with what substitution? (3 points)

### Question 6: Forward vs. Backward Chaining (10 points)

Using the kinship rule ∀ x, y (Parent(x, y) ∧ Male(x) → Father(x, y)) and facts Parent(Richard, John), Male(Richard):

(a) Trace forward chaining to derive Father(Richard, John). Show the unification and the derived fact. (5 points)

(b) Trace backward chaining for the query Father(Richard, John). Show the subgoals and how they are resolved. (5 points)

### Question 7: FOL Resolution and Skolemization (10 points)

(a) Convert the sentence ∀ x (King(x) → ∃ y (Father(y, x))) to CNF. Show each step, including Skolemization. (6 points)

(b) Explain what Skolemization does and why it preserves satisfiability (but not validity). (4 points)

---

## Grading Rubric

| Section                       | Points        |
| ----------------------------- | ------------- |
| Q1 (Wumpus PL)                | 20            |
| Q2 (Entailment/Inference)     | 15            |
| Q3 (Horn Clauses)             | 15            |
| Q4 (FOL Syntax/Semantics)     | 15            |
| Q5 (Unification/GMP)          | 15            |
| Q6 (Chaining)                 | 10            |
| Q7 (Resolution/Skolemization) | 10            |
| **Total**               | **100** |

---

## Suggested Length

A complete submission is approximately 6–9 pages, including derivations, truth-table reasoning, and FOL translations.
