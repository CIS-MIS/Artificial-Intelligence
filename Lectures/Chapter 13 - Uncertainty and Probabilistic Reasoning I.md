# Artificial Intelligence - Chapter 13: Uncertainty and Probabilistic Reasoning I

## Lecture Note Slides (20 Slides)

**Source Materials:** AI - Chapter 13 (textbook); AI Lecture Notes 09 (Reinforcement Learning - value, reward, credit assignment); AI Lecture Notes 18 (Algorithmic Bias); AI Lecture Notes 19 (Bias Detection and Reduction)

---

## Slide 1 - Uncertainty and Probabilistic Reasoning I: Probability, Conditional Probability, and Bayes' Rule

**Uncertainty and Probabilistic Reasoning I: Probability, Conditional Probability, and Bayes' Rule**

Chapter 13 - Uncertainty

A scholarly treatment of reasoning under uncertainty: the axioms of probability, conditional probability, Bayes' rule, and the foundations of probabilistic inference in AI.

---

## Slide 2 - Why Uncertainty Matters

Classical logic (Chapters 9-12) assumes the world is fully knowable: facts are true or false, and inference is certain. Real AI systems face:

- **Partial observability:** Sensors give incomplete information (robot knows only its current square)
- **Nondeterminism:** Actions have multiple possible outcomes (slippery floors, dice)
- **Ignorance:** Not all relevant facts are known or representable
- **Laziness:** Enumerating all exceptions is impractical ("birds fly" has penguins, injured birds, etc.)
- **Probabilistic causation:** Smoking raises cancer risk but does not guarantee it

Probability theory provides the formal calculus for reasoning under uncertainty. It quantifies degrees of belief and updates them as evidence arrives.

---

## Slide 3 - The Axioms of Probability

Probability assigns a number P(a) ∈ [0,1] to each proposition a, representing the degree of belief that a is true. Three axioms (Kolmogorov):

1. **Non-negativity:** 0 ≤ P(a) ≤ 1 for any proposition a
2. **Normalization:** P(True) = 1, P(False) = 0
3. **Additivity:** P(a ∨ b) = P(a) + P(b) − P(a ∧ b)

From these follow key theorems:

- P(¬a) = 1 − P(a)
- P(a ∨ b) = P(a) + P(b) if a and b are mutually exclusive
- P(a) = Σᵢ P(a ∧ bᵢ) for any partition b₁, ..., bₙ

Probability is the unique calculus satisfying these axioms and avoiding incoherent betting behavior (Dutch book arguments).

---

## Slide 4 - Prior and Conditional Probability

**Prior (unconditional) probability:** P(a) - degree of belief in a before any evidence.

**Conditional probability:** P(a | b) - degree of belief in a given that b is known true.

Definition: P(a | b) = P(a ∧ b) / P(b), provided P(b) > 0

This is the **product rule**: P(a ∧ b) = P(a | b) P(b)

Example: P(Cavity | Toothache) = 0.8 means "given a toothache, there is an 80% chance of a cavity."

Conditional probability captures how evidence updates belief - the core of probabilistic reasoning.

---

## Slide 5 - The Joint Probability Distribution

The **joint distribution** P(X₁, ..., Xₙ) assigns probabilities to all combinations of values of random variables X₁...Xₙ. It is the complete probabilistic specification of a domain.

From the joint, all other probabilities can be derived:

- P(a) = Σ over all assignments consistent with a of the joint probability (marginalization)
- P(a | b) = P(a ∧ b) / P(b)

For n Boolean variables, the joint has 2ⁿ entries - exponential growth. This is why compact representations (Bayesian networks, Chapter 14) are essential.

Example: Cavity, Toothache, Catch (dentist probe catches) - 2³ = 8 joint entries specify everything.

---

## Slide 6 - Inference from the Joint Distribution

Given the full joint, any probabilistic query can be answered:

**Marginalization:** P(Cavity) = Σₜ P(Cavity ∧ Toothache=t) - sum out other variables

**Conditioning:** P(Cavity | Toothache) = P(Cavity ∧ Toothache) / P(Toothache)

**Normalization:** P(Cavity | Toothache) = α × P(Cavity ∧ Toothache) where α = 1/P(Toothache)

Example with dentist domain (cavity ∈ {true, false}, toothache ∈ {true, false}):

- P(Cavity ∧ Toothache) = 0.04
- P(Toothache) = 0.05
- P(Cavity | Toothache) = 0.04 / 0.05 = 0.8

The joint is complete but impractical for large domains - motivating independence assumptions.

---

## Slide 7 - Independence and Conditional Independence

**Independence:** P(a ∧ b) = P(a) P(b), equivalently P(a | b) = P(a). Knowing b tells nothing about a.

**Conditional independence:** P(a ∧ b | c) = P(a | c) P(b | c), equivalently P(a | b, c) = P(a | c). Given c, b tells nothing more about a.

Conditional independence dramatically reduces the joint:
P(Cavity, Toothache, Catch) = P(Cavity) P(Toothache | Cavity) P(Catch | Cavity)

if Toothache and Catch are conditionally independent given Cavity. This is the structure exploited by Bayesian networks.

---

## Slide 8 - Bayes' Rule

Bayes' rule inverts conditional probabilities:

P(b | a) = P(a | b) P(b) / P(a)

Derived from the product rule applied both ways:
P(a ∧ b) = P(a | b) P(b) = P(b | a) P(a)

The **normalized** form:
P(b | a) = α P(a | b) P(b), where α = 1/P(a) = Σᵦ P(a | bᵢ) P(bᵢ)

Bayes' rule is the foundation of **diagnostic reasoning**: from evidence (symptoms) infer causes (diseases).

P(Cause | Effect) = P(Effect | Cause) P(Cause) / P(Effect)

---

## Slide 9 - Bayes' Rule: Medical Diagnosis Example

A doctor wants P(Cavity | Toothache). Known:

- P(Cavity) = 0.1 (prior - base rate)
- P(Toothache | Cavity) = 0.8 (likelihood)
- P(Toothache | ¬Cavity) = 0.1
- P(Toothache) = P(Toothache | Cavity)P(Cavity) + P(Toothache | ¬Cavity)P(¬Cavity)
  = 0.8 × 0.1 + 0.1 × 0.9 = 0.08 + 0.09 = 0.17

P(Cavity | Toothache) = 0.8 × 0.1 / 0.17 ≈ 0.47

Despite a strong likelihood (0.8), the posterior is only 0.47 because cavities are rare (base rate 0.1). This illustrates the **base rate fallacy** - ignoring priors leads to overconfident diagnoses.

---

## Slide 10 - The Base Rate Fallacy and Diagnostic Caution

People often neglect prior probabilities. Example: a rare disease affects 1 in 1000; a test is 99% accurate (sensitivity and specificity).

P(Disease | Positive) = 0.99 × 0.001 / [0.99 × 0.001 + 0.01 × 0.999] ≈ 0.09

Even with a positive test, only a 9% chance of disease because the disease is rare.

Implications for AI:

- Systems must incorporate base rates, not just likelihoods
- Text Note 18 warns algorithmic bias can arise when base rates in training data reflect historical inequalities
- A model predicting loan default must account for base default rates by demographic group to avoid unfair disparities

---

## Slide 11 - Random Variables and Probability Distributions

A **random variable** represents a quantity with uncertain value: Weather ∈ {sunny, rain, cloudy, snow}, Cavity ∈ {true, false}, Temperature ∈ ℝ.

**Probability distribution:** P(X) assigns probabilities to all values of X, summing to 1.

**Joint distribution:** P(X, Y) over pairs of values.

**Marginal distribution:** P(X) = Σᵧ P(X, Y=y)

**Conditional distribution:** P(X | Y=y) = P(X, Y=y) / P(Y=y)

Distributions may be:

- **Discrete:** finite or countable values (Cavity, Weather)
- **Continuous:** uncountable values (Temperature) - use probability density functions

AI systems typically work with discrete distributions for tractability, though continuous methods exist (Gaussian, Kalman filters).

---

## Slide 12 - Probability as a Basis for Decision: Expected Utility

Probability alone describes belief; **utility** captures preferences over outcomes. Decision theory combines them.

**Expected utility** of action A:
EU(A) = Σₛ P(s | A) U(s)

where s ranges over possible resulting states and U(s) is the utility of state s.

A **rational agent** (Chapter 2) chooses the action maximizing expected utility - generalizing expected monetary value to arbitrary preferences.

Text Note 09 (Reinforcement Learning) connects to value: V(s) estimates expected future reward, guiding action selection under uncertainty. The credit assignment problem (attributing outcomes to actions) is harder under probabilistic outcomes.

---

## Slide 13 - Representing Uncertainty in AI Systems

FOL (Chapters 11-12) is true/false and cannot express uncertainty. Probabilistic representations:

- **Probability distributions:** degrees of belief over propositions
- **Bayesian networks (Chapter 14):** compact joint distributions via conditional independence and graph structure
- **Markov models / HMMs:** uncertainty over time
- **Markov Decision Processes (Text Note 09):** stochastic transitions, rewards, value functions

The shift from logic to probability is the shift from **certain deduction** to **probabilistic inference** - from "P is true" to "P is true with probability 0.83."

---

## Slide 14 - Probabilistic Inference: The Core Tasks

Given a probabilistic model, three canonical inference tasks:

1. **Probability of evidence:** P(e) - how likely is observed evidence?
2. **Posterior query:** P(X | e) - belief in variable X given evidence e
3. **Most probable explanation (MPE):** argmaxₓ P(x | e) - most likely complete state

Exact inference is intractable in general (#P-complete), motivating approximate methods:

- Variable elimination (exact, for polytrees)
- Belief propagation
- Sampling (likelihood weighting, Gibbs sampling, particle filtering)
- Variational methods

Chapter 14 develops Bayesian networks and exact inference; later techniques handle scale.

---

## Slide 15 - Uncertainty and Algorithmic Bias (Text Note 18)

Probabilistic models learn from data, and data can encode bias:

- **Unrepresentative training data** skews probability estimates
- **Historical inequalities** appear as statistical regularities (e.g., loan default rates by zip code reflecting past discrimination)
- **Incorrect labels** corrupt likelihood estimates
- **Poorly chosen objectives** optimize the wrong quantity

Text Note 18 describes algorithmic bias: systematically distorted or unfair results. Sources include unrepresentative data, historical inequality, incorrect labels, poorly chosen objectives, inappropriate assumptions, measurement error, and deployment context.

Mitigation: examine training data, test across groups, check labels, evaluate assumptions, monitor post-deployment outcomes. Human oversight is essential (Text Note 14).

---

## Slide 16 - Uncertainty in Reinforcement Learning (Text Note 09)

Text Note 09 frames uncertainty in sequential decision-making:

- **Stochastic environments:** transitions are probabilistic; the agent cannot predict exact next states
- **Sparse rewards:** feedback arrives only after long action sequences (credit assignment)
- **Value functions:** V(s) estimates expected long-term reward under uncertainty
- **Exploration vs. exploitation:** balance trying uncertain actions vs. using known-good ones

Bayesian RL extends this: maintain a distribution over possible models (model uncertainty) and act to reduce it (information-directed exploration). This unifies probability and sequential decision-making.

---

## Slide 17 - Probability in Representation Learning and Language Models

Text Note 06 (Unsupervised Learning, Representation Learning) shows how probability underlies representation learning: word embeddings capture distributional similarity, where words appearing in similar contexts have similar vector representations. These representations are learned from probabilistic co-occurrence statistics over large text corpora.

Text Notes 07-08 (Language Models) treat language modeling as probabilistic next-token prediction: the model estimates P(next word | previous words) and samples or greedily selects tokens. Perplexity, a standard evaluation metric, is the exponential of the average negative log-likelihood - a direct probability-based measure.

Thus probability is not only a reasoning tool but also the objective that drives modern representation and language learning.

---

## Slide 18 - From Exact to Approximate Inference

Exact probabilistic inference is intractable in general (#P-complete), so AI systems rely on approximations. Variable elimination is exact but exponential in treewidth; sampling methods (likelihood weighting, Gibbs sampling) are approximate but scale to large networks. Loopy belief propagation and variational inference offer further trade-offs between speed and accuracy.

The choice of inference method mirrors the search trade-offs earlier in the course: exact methods give guarantees but scale poorly, while approximate methods scale well but provide no optimality guarantees. In large probabilistic models such as modern language models, inference is approximated by a single forward pass through a neural network rather than by enumerating the joint distribution.

---

## Slide 19 - Summary: Key Takeaways

1. Uncertainty arises from partial observability, nondeterminism, ignorance, laziness, and probabilistic causation - classical logic is insufficient
2. Probability axioms: 0 ≤ P(a) ≤ 1, P(True) = 1, P(a ∨ b) = P(a) + P(b) − P(a ∧ b)
3. Conditional probability P(a | b) = P(a ∧ b) / P(b); product rule P(a ∧ b) = P(a | b) P(b)
4. The joint distribution is complete but exponential; marginalization and conditioning derive all queries
5. Independence and conditional independence enable compact representations
6. Bayes' rule: P(b | a) = P(a | b) P(b) / P(a) - the basis of diagnostic reasoning
7. Base rate neglect leads to overconfident inference; priors matter
8. Random variables and distributions (discrete/continuous) formalize uncertain quantities
9. Expected utility combines probability with preferences for rational decision-making
10. Uncertainty interacts with bias (data skew) and RL (stochastic transitions, credit assignment)

---

## Slide 20 - Review Questions

1. Why is classical logic insufficient for real-world AI systems? Name five sources of uncertainty.
2. State the three axioms of probability and derive P(¬a) = 1 − P(a).
3. Define conditional probability and the product rule. Compute P(Cavity | Toothache) given P(Cavity ∧ Toothache) = 0.04 and P(Toothache) = 0.05.
4. What is the joint distribution, and why is it impractical for large domains?
5. Distinguish independence from conditional independence with an example.
6. Derive Bayes' rule from the product rule.
7. Apply Bayes' rule: given P(Disease)=0.001, P(Positive|Disease)=0.99, P(Positive|¬Disease)=0.01, compute P(Disease|Positive).
8. What is the base rate fallacy, and why does it matter for AI diagnosis systems?
9. Define random variable, marginal distribution, and conditional distribution.
10. How does expected utility generalize expected monetary value for rational agents?
11. How does Text Note 18 connect uncertain data to algorithmic bias?
12. How does uncertainty affect credit assignment in reinforcement learning (Text Note 09)?
