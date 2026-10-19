# Artificial Intelligence - Chapter 11: First-Order Logic I

## Lecture Note Slides (20 Slides)

**Source Materials:** AI - Chapter 11 (textbook); AI Lecture Notes 10 (Symbolic AI, Logic, Knowledge Bases, and Expert Systems)

---

## Slide 1 - First-Order Logic I: Objects, Relations, Quantifiers, and Expressive Knowledge Representation

**First-Order Logic I: Objects, Relations, Quantifiers, and Expressive Knowledge Representation**

Chapter 11 - First-Order Logic

A scholarly treatment of first-order logic (FOL): syntax and semantics, objects and relations, quantifiers, and knowledge representation in domains such as kinship and the Wumpus World.

---

## Slide 2 - Limitations of Propositional Logic

Propositional logic cannot express general knowledge economically:

- It has no variables: "every pit causes a breeze in adjacent squares" requires one sentence per square
- It has no quantifiers: cannot say "there exists a Wumpus" or "all squares are safe"
- It cannot refer to objects or relations: symbols are atomic; no structure like "Wumpus(3,4)"
- Knowledge bases grow with world size rather than with domain complexity

First-order logic (FOL) overcomes these by introducing:

- **Objects:** entities in the world (people, numbers, squares, Wumpuses)
- **Relations:** properties of objects and relationships among them
- **Functions:** mappings from objects to objects (return an object)
- **Quantifiers:** ∀ (for all) and ∃ (there exists)

FOL is the standard logic for knowledge representation and automated reasoning.

---

## Slide 3 - Syntax of First-Order Logic

FOL sentences are built from:

**Constant symbols:** John, Richard, 2, [1,1] - name specific objects
**Predicate symbols:** Brother, >, Pit, Wumpus - name relations (return true/false)
**Function symbols:** Father, Sqrt, LeftLeg - map objects to objects (return an object)
**Variables:** x, y, z - range over objects
**Connectives:** ¬, ∧, ∨, →, ↔ (same as propositional logic)
**Quantifiers:** ∀, ∃
**Equality:** =

Examples:

- Brother(Richard, John) - Richard is John's brother
- Married(Father(John), Mother(John)) - John's parents are married
- > (2, 3) is false; > (Sqrt(16), 3) is true
  >
- ∀ x (King(x) → Person(x)) - every king is a person
- ∃ x (Brother(x, Richard)) - Richard has a brother

---

## Slide 4 - Terms and Atomic Sentences

**Terms** denote objects:

- Constant symbols and variables are terms
- If f is a function of arity n and t₁...tₙ are terms, f(t₁,...,tₙ) is a term

Examples: John, x, Father(John), Sqrt(2), LeftLeg(Richard)

**Atomic sentences** (atoms) are formed from predicate symbols applied to terms:

- If P is a predicate of arity n and t₁...tₙ are terms, P(t₁,...,tₙ) is an atomic sentence

Examples: Brother(Richard, John), Married(Father(x), Mother(x)), > (2, Sqrt(4))

Complex sentences combine atoms with connectives and quantifiers, as in propositional logic.

---

## Slide 5 - Quantifiers

Quantifiers let FOL express general statements:

**Universal quantification ∀ x P(x):** "For all x, P(x) holds" - P is true for every object in the domain

- ∀ x (King(x) → Person(x)) - every king is a person
- ∀ x (P(x) → B(x)) - every pit is breezy

**Existential quantification ∃ x P(x):** "There exists an x such that P(x) holds" - P is true for at least one object

- ∃ x (Brother(x, Richard)) - Richard has a brother
- ∃ x (Pit(x) ∧ B(x)) - some pit is breezy

**Important connective pairing:**

- ∀ typically pairs with →: ∀ x (King(x) → Person(x)) - "if x is a king, x is a person"
- ∃ typically pairs with ∧: ∃ x (Brother(x, Richard) ∧ Person(x)) - "someone is Richard's brother and is a person"

Common error: ∃ x (King(x) → Person(x)) is true if there exists anyone who is not a king - almost never what is intended.

---

## Slide 6 - Semantics of First-Order Logic

FOL semantics requires a **domain of discourse** (the set of objects) and an **interpretation**:

- Each constant symbol refers to an object in the domain
- Each predicate symbol refers to a relation on the domain
- Each function symbol refers to a function on the domain
- Each variable is assigned an object via a variable assignment

A sentence is true or false relative to an interpretation and variable assignment:

- Atomic sentence P(t₁,...,tₙ) is true iff the tuple of objects referred to by t₁...tₙ is in the relation referred to by P
- ∀ x P(x) is true iff P(x) is true for every object assigned to x
- ∃ x P(x) is true iff P(x) is true for some object assigned to x

Equality: t₁ = t₂ is true iff both terms refer to the same object.

---

## Slide 7 - Example Domains: Kinship

The kinship domain illustrates FOL's expressive power:

Objects: people (John, Richard, ...)
Relations: Brother, Sister, Father, Mother, Parent, Child, Spouse, Married, Person, Male, Female
Functions: Father, Mother (each person has exactly one father and mother)

Axioms:

1. ∀ x, y (Father(x) = y ↔ Parent(y, x) ∧ Male(y))
2. ∀ x, y (Brother(x, y) ↔ Male(x) ∧ ∃ z (Parent(z, x) ∧ Parent(z, y)) ∧ x ≠ y)
3. ∀ x, y (Parent(x, y) ↔ Child(y, x))
4. ∀ x (Male(x) ↔ ¬Female(x))

These axioms capture general kinship knowledge compactly - one sentence covers all people, not one per person.

Queries: ∃ y (Brother(y, Richard)) - does Richard have a brother? ∀ x (Person(x) → ∃ y (Mother(y) = x)) - does everyone have a mother?

---

## Slide 8 - Example Domain: The Wumpus World in FOL

In FOL, the Wumpus World can be represented compactly:

Objects: squares [1,1]...[4,4]
Relations: Pit(x), Wumpus(x), Breezy(x), Stenchy(x), Safe(x), Adjacent(x,y)
Functions: East(x), West(x), North(x), South(x) - neighboring squares

Axioms:

1. ∀ x (Breezy(x) ↔ ∃ y (Adjacent(x,y) ∧ Pit(y))) - a square is breezy iff adjacent to a pit
2. ∀ x (Stenchy(x) ↔ ∃ y (Adjacent(x,y) ∧ Wumpus(y))) - stench iff adjacent to Wumpus
3. ∀ x, y (Adjacent(x, East(y)) ↔ x = East(y)) - adjacency definition
4. ∀ x (Pit(x) → ¬Safe(x)) - pits are unsafe
5. ∀ x (Wumpus(x) → ¬Safe(x)) - Wumpus squares are unsafe

FOL expresses the breeze rule once for all squares; propositional logic needs one rule per square (16 rules for a 4×4 grid).

---

## Slide 9 - FOL vs. Propositional Logic: Expressiveness

Propositional Wumpus knowledge base (16 squares):

- B[1,1] ↔ (P[1,2] ∨ P[2,1])
- B[1,2] ↔ (P[1,1] ∨ P[1,3] ∨ P[2,2])
- ... (16 rules, one per square)

FOL Wumpus knowledge base:

- ∀ x (Breezy(x) ↔ ∃ y (Adjacent(x,y) ∧ Pit(y))) - ONE rule for all squares

FOL also expresses:

- Uniqueness: ∃! x (Wumpus(x)) - exactly one Wumpus
- Generalization: ∀ x (Pit(x) → ¬Safe(x)) - all pits are unsafe
- Existence: ∃ x (Gold(x)) - gold exists somewhere

This compactness is why FOL scales to complex domains where propositional logic fails.

---

## Slide 10 - The Wumpus World Agent in FOL

A FOL-based wumpus agent:

1. **Tells** the KB percepts: Breezy([1,1]), ¬Breezy([2,1]), Stenchy([3,1])
2. **Tells** the KB: ¬Pit([1,1]), ¬Wumpus([1,1]), Adjacent facts
3. **Represents** rules: ∀ x (Breezy(x) ↔ ∃ y (Adjacent(x,y) ∧ Pit(y)))
4. **Asks**: Which squares are safe? → derives Safe([1,2]), Safe([2,1]) etc.
5. **Asks**: Where is the Wumpus? → derives Wumpus location if entailed
6. **Acts**: Move to safe square, shoot toward Wumpus

FOL lets the agent reason with general rules and quantified statements, deriving conclusions about many squares from few percepts.

Text Note 10 provides detailed FOL examples: kinship domain and Wumpus domain, showing how relations, functions, and quantifiers represent knowledge.

---

## Slide 11 - Inference in First-Order Logic

FOL inference is more complex than propositional inference because:

- Variables can be instantiated with any object (infinitely many possibilities in infinite domains)
- Quantifiers range over potentially infinite domains
- Unification is needed to match terms with variables

Key inference approach: **reduce FOL to propositional logic** via **instantiation**:

**Universal Instantiation:** From ∀ x P(x), infer P(A) for any ground term A (no variables)
**Existential Instantiation:** From ∃ x P(x), infer P(c) where c is a new constant symbol (Skolem constant) not appearing elsewhere

After instantiation, propositional inference methods (resolution, truth tables) apply - but the instantiation may be infinite, so this is not always practical.

This motivates FOL-native inference: unification, generalized modus ponens, resolution with unification (Chapter 12).

---

## Slide 12 - Unification

**Unification** finds a substitution that makes two logical expressions identical:

UNIFY(P(x), P(A)) = {x/A}
UNIFY(Knows(John, x), Knows(y, Bill)) = {x/Bill, y/John}
UNIFY(Father(x), Father(John)) = {x/John}
UNIFY(Father(x), x) = FAIL (occurs check: x cannot equal Father(x))

A substitution is a set of variable→term bindings. Unification succeeds if a consistent substitution exists; it fails if variables would need to bind to terms containing themselves (occurs check).

Unification is the heart of FOL inference: it matches atomic sentences with variables, enabling generalized modus ponens and FOL resolution (Chapter 12).

---

## Slide 13 - Generalized Modus Ponens (GMP)

GMP lifts propositional Modus Ponens to FOL with unification:

From:

- P₁′ ∧ P₂′ ∧ ... ∧ Pₙ′ (facts with variables)
- (P₁ ∧ P₂ ∧ ... ∧ Pₙ) → Q (rule)

If there exists a substitution θ such that Pᵢ′θ = Pᵢθ for all i, infer Qθ.

Example:
Facts: King(John), Greedy(John)
Rule: ∀ x (King(x) ∧ Greedy(x) → Evil(x))

Substitution θ = {x/John} unifies King(John) with King(x) and Greedy(John) with Greedy(x).
Conclusion: Evil(John)

GMP is complete for definite clause knowledge bases (Horn clauses in FOL) and underlies forward/backward chaining in FOL.

---

## Slide 14 - Forward and Backward Chaining in FOL

**Forward chaining (data-driven):**

- Start with known ground facts
- Use GMP with unification to fire rules whose premises match facts
- Add conclusions as new facts
- Repeat until query derived or no new facts

**Backward chaining (goal-driven):**

- Start from the query
- Find rules whose conclusion unifies with the query
- Recursively prove each premise as a subgoal
- Depth-first with backtracking

Both are sound and complete for definite clause KBs. Forward chaining derives all entailed facts; backward chaining focuses on proving one query.

Text Note 10 covers forward/backward chaining for FOL with examples (kinship queries).

---

## Slide 15 - Limitations of First-Order Logic

FOL is powerful but limited:

1. **Undecidability:** FOL entailment is semidecidable - if KB ⊨ α, a proof exists and can be found; but if KB ⊭ α, the search may never terminate (Church-Turing theorem)
2. **No uncertainty:** FOL is true/false; cannot express "probably," "likely," or "uncertain"
3. **No vagueness:** Cannot express "tall," "warm," or "similar"
4. **Knowledge engineering:** Encoding domain knowledge in FOL is labor-intensive
5. **Computational cost:** FOL inference can be very expensive

These limitations motivate **probabilistic reasoning** (Chapters 13-14) for uncertainty, and **fuzzy logic** / probabilistic logic for vagueness.

---

## Slide 16 - FOL in Knowledge Bases and Expert Systems

Logical agents and expert systems (Text Note 10) use FOL to encode domain knowledge in a declarative, inspectable form. Because FOL sentences have clear semantics, a domain expert can review the axioms and verify they capture the intended domain knowledge. This explainability is a major advantage over black-box neural models.

However, the labor of knowledge engineering - writing axioms by hand - limits the scale of FOL knowledge bases. Real-world domains contain millions of facts and exceptions, making purely symbolic knowledge bases hard to complete and maintain. This motivates hybrid systems that combine symbolic rules with learned components.

---

## Slide 17 - From FOL to Automated Theorem Proving

FOL inference underpins automated theorem provers and logic programming languages such as Prolog (Chapter 12). A theorem prover takes a set of axioms and a conjecture, then attempts to derive the conjecture via resolution and unification. If successful, the conjecture is a logical consequence of the axioms.

Theorem proving has been applied to verify hardware designs, prove mathematical theorems, and validate security protocols. Its limitation is semidecidability: when the conjecture is not entailed, the prover may run forever without reporting failure.

---

## Slide 18 - FOL and the Frame Problem

A foundational challenge for logical agents is the frame problem: how to compactly represent what stays the same when an action occurs. In the Wumpus World, moving from [1,1] to [1,2] changes the agent's location but leaves pits, the Wumpus, and the gold untouched. In propositional logic, every unchanged fact must be stated explicitly (frame axioms), which grows with the number of fluents and actions.

FOL addresses this more compactly through quantification and successor-state axioms, but the frame problem remains a foundational issue in knowledge representation: an intelligent agent must know not only what an action changes, but everything it leaves unchanged. This limitation, together with FOL's inability to handle uncertainty, motivates the probabilistic methods of Chapters 13-14.

---

## Slide 19 - Summary: Key Takeaways

1. Propositional logic lacks variables, quantifiers, objects, and relations; FOL overcomes all four limitations
2. FOL syntax: constants, predicates, functions, variables, connectives, quantifiers, equality
3. Terms denote objects; atomic sentences apply predicates to terms
4. Universal quantifier ∀ typically pairs with →; existential ∃ typically pairs with ∧
5. Semantics requires a domain and interpretation; truth is relative to interpretation and variable assignment
6. FOL expresses general knowledge compactly: one rule covers all objects (kinship, Wumpus examples)
7. Universal instantiation reduces ∀ statements to ground instances; existential instantiation introduces Skolem constants
8. Unification finds substitutions making expressions identical; it is the core matching operation in FOL inference
9. Generalized Modus Ponens applies propositional Modus Ponens to FOL via unification
10. Forward and backward chaining extend to FOL with unification and GMP; both are sound and complete for definite clauses

---

## Slide 20 - Review Questions

1. What four limitations of propositional logic does FOL address?
2. Distinguish constant symbols, predicate symbols, function symbols, and variables with examples.
3. What is a term in FOL? Give three examples.
4. Why does ∀ typically pair with → and ∃ with ∧? What goes wrong if you swap them?
5. What is the domain of discourse, and what does an interpretation specify?
6. Translate "Every king is a person" and "Richard has a brother" into FOL.
7. Translate the Wumpus breeze rule into FOL: "a square is breezy iff it is adjacent to a pit."
8. What is universal instantiation, and what is existential instantiation (Skolemization)?
9. What is unification, and when does the occurs check cause unification to fail?
10. State Generalized Modus Ponens and apply it: from King(John), Greedy(John), and ∀ x(King(x) ∧ Greedy(x) → Evil(x)), what follows?
11. Why is FOL entailment semidecidable rather than decidable?
12. What are three limitations of FOL, and how does probabilistic reasoning address limitation #2?
