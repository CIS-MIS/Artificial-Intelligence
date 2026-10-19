# Artificial Intelligence - Chapter 14: Uncertainty and Probabilistic Reasoning II

## Lecture Note Slides (20 Slides)

**Source Materials:** AI - Chapter 14 (textbook); AI Lecture Notes 09 (Reinforcement Learning - value functions); AI Lecture Notes 05 (Machine Learning - loss, generalization, overfitting); AI Lecture Notes 18 (Algorithmic Bias); AI Lecture Notes 19 (Bias Detection)

---

## Slide 1 - Bayesian Networks: Compact Probabilistic Models, Exact and Approximate Inference

**Bayesian Networks: Compact Probabilistic Models, Exact and Approximate Inference**

Chapter 14 - Probabilistic Reasoning

A scholarly treatment of Bayesian networks: graph structure, conditional probability tables, inference by enumeration and variable elimination, approximate sampling, and causal interpretation.

---

## Slide 2 - From Joint Distributions to Compact Models

The full joint distribution P(X₁,...,Xₙ) is complete but exponential (2ⁿ entries for n Boolean variables). Two problems:

- **Storage:** exponential space
- **Assessment:** eliciting 2ⁿ probabilities from experts is infeasible

Bayesian networks exploit **conditional independence** to factor the joint:
P(X₁,...,Xₙ) = Πᵢ P(Xᵢ | Parents(Xᵢ))

This stores only local conditional distributions - tractable when each variable has few parents. It is the standard representation for probabilistic AI.

---

## Slide 3 - Bayesian Network Structure

A **Bayesian network** is a directed acyclic graph (DAG) where:

- Nodes = random variables (X₁,...,Xₙ)
- Arcs = direct influence (parent → child)
- Each node Xᵢ has a **conditional probability table** (CPT): P(Xᵢ | Parents(Xᵢ))

Semantics: the network encodes the joint via the chain rule with conditional independence:
P(x₁,...,xₙ) = Πᵢ=1ⁿ P(xᵢ | parents(Xᵢ))

The graph asserts that each variable is conditionally independent of its non-descendants given its parents - the **local Markov condition**.

---

## Slide 4 - Example: The Alarm Network

Classic example (Pearl): Burglary (B), Earthquake (E), Alarm (A), JohnCalls (J), MaryCalls (M).

Structure:

- B → A (burglary can trigger alarm)
- E → A (earthquake can trigger alarm)
- A → J (alarm may cause John to call)
- A → M (alarm may cause Mary to call)

Intuition: burglary and earthquake are root causes; alarm is their common effect; John/Mary call in response to the alarm. J and M are conditionally independent given A (they don't call each other).

CPTs specify P(A | B, E), P(J | A), P(M | A), P(B), P(E).

---

## Slide 5 - Semantics: Global vs. Local Markov

**Global Markov condition:** A node is independent of all non-descendants given its parents (and all its descendants given its parents, children, and children's parents - the Markov blanket).

**Local Markov condition:** A node is conditionally independent of its non-descendants given its parents.

For a DAG, global and local Markov conditions are equivalent. The network's CPTs plus structure fully determine the joint distribution.

**D-separation** (directional separation) determines which independence assertions hold: two nodes are d-separated if all paths between them are "blocked" by evidence. This supports probabilistic query answering without enumerating the joint.

---

## Slide 6 - Constructing Bayesian Networks

Steps:

1. Choose variables and ordering (causal ordering often natural: causes before effects)
2. For each variable Xᵢ in order:
   - Add node Xᵢ
   - Select Parents(Xᵢ) as a minimal set of already-added nodes such that Xᵢ is conditionally independent of all other added nodes given parents
   - Specify CPT P(Xᵢ | Parents(Xᵢ))

The ordering affects compactness. Causal ordering (root causes first) typically yields minimal parents. Expert knowledge or structure learning (from data) determines both graph and CPTs.

CPT size: for Boolean Xᵢ with k Boolean parents, 2ᵏ entries. Small k keeps assessment feasible.

---

## Slide 7 - Inference in Bayesian Networks: Three Tasks

Given evidence e and query variable X:

1. **Posterior probability:** P(X | e) - belief update (e.g., P(Burglary | JohnCalls))
2. **Probability of evidence:** P(e) - model fit / anomaly detection
3. **Most probable explanation (MPE):** argmaxₓ P(x | e) - most likely state (e.g., did burglary or earthquake cause the alarm?)

Exact inference is **#P-complete** (intractable in general). Bayesian networks make many cases tractable, especially polytrees (singly-connected graphs).

---

## Slide 8 - Inference by Enumeration

For discrete variables, compute P(X | e) via the joint:

P(X | e) = α P(X, e) = α Σ_y P(X, e, Y=y)

where Y = non-evidence, non-query variables, and α normalizes.

Using the network factorization:
P(X, e) = Σ_y Πᵢ P(xᵢ | parents(Xᵢ)) with evidence fixed

Enumeration sums over all configurations of Y - exponential in |Y|. Correct but impractical for many variables. Variable elimination improves this.

Example: P(Burglary | JohnCalls=true) = α Σₑ,ₐ,ₘ P(B, E, A, J=true, M) - sum over E, A, M.

---

## Slide 9 - Variable Elimination

Variable elimination (VE) avoids redundant computation by pushing summations inward:

P(X | e) = α Σ_z₁ ... Σ_zₖ Πᵢ P(xᵢ | parents(Xᵢ))

Process variables one at a time: sum out each non-query, non-evidence variable, producing factors (tables over remaining variables). Reuse intermediate factors.

Complexity is exponential in the **treewidth** of the graph (size of largest factor during elimination), not n. Polytrees have treewidth 1 - linear-time inference. Ordering of elimination affects treewidth; finding optimal order is NP-hard, heuristics work well.

VE is exact and typically far faster than enumeration.

---

## Slide 10 - Example: Variable Elimination on the Alarm Network

Compute P(B | J=true). Variables: B, E, A, M (J fixed to true).

Factors: P(B), P(E), P(A|B,E), P(J=true|A), P(M|A)

Eliminate M: Σₘ P(M|A) = 1 → removes M
Eliminate A: new factor τ(B,E) = Σₐ P(A=a|B,E) × P(J=true|A=a)
Eliminate E: τ'(B) = Σₑ P(E=e) × τ(B,e)
Result: P(B | J=true) = α × P(B) × τ'(B)

Only small factors (over B, E at most) - tractable.

---

## Slide 11 - Approximate Inference: Sampling

For large networks, exact inference is too slow. Sampling approximates P(X | e):

**Prior sampling:** Sample each variable in topological order from its CPT given already-sampled parents. The fraction of samples with X=x estimates P(X).

**Rejection sampling:** Generate prior samples; keep only those consistent with evidence e; fraction with X=x estimates P(X | e). Wasteful when e is rare.

**Likelihood weighting:** Fix evidence variables; sample non-evidence variables; weight each sample by Π P(eᵢ | parents(eᵢ)) (likelihood of evidence given parents). Better for rare evidence.

**Gibbs sampling (MCMC):** Initialize; repeatedly resample each non-evidence variable from P(Xᵢ | Markov blanket) given current values; after burn-in, samples approximate the posterior. Handles evidence naturally.

Sampling is approximate but converges to correct answers with enough samples; scales to large networks.

---

## Slide 12 - Beyond Exact Inference: When to Use What

| Method               | Exact/Approximate | Complexity               | Best for                         |
| -------------------- | ----------------- | ------------------------ | -------------------------------- |
| Enumeration          | Exact             | O(n·2ⁿ)                | Tiny networks                    |
| Variable elimination | Exact             | Exponential in treewidth | Polytrees, moderate treewidth    |
| Prior sampling       | Approximate       | O(samples × n)          | Common evidence                  |
| Rejection sampling   | Approximate       | O(samples / P(e))        | Very common evidence             |
| Likelihood weighting | Approximate       | O(samples × n)          | Rare evidence                    |
| Gibbs sampling       | Approximate       | O(samples × n)          | Large networks, multiple queries |

Text Note 05 (Machine Learning) connects: evaluation on unseen data, overfitting, and generalization apply equally to learned Bayesian network parameters.

---

## Slide 13 - Causal vs. Diagnostic Reasoning

Bayesian networks support both directions naturally:

**Causal (top-down):** P(JohnCalls | Burglary) - propagate from cause to effect. Given burglary, probability John calls.

**Diagnostic (bottom-up):** P(Burglary | JohnCalls) - propagate from effect to cause. Given John called, probability of burglary.

The same network answers both because the joint is symmetrical; only the query direction differs. This is a key advantage over rule-based systems that hardcode one direction.

However, **correlation ≠ causation.** The network encodes conditional independencies; whether arcs represent true causal mechanisms depends on domain knowledge and structure learning validity. Text Note 19 warns that statistical associations may reflect bias rather than causal truth.

---

## Slide 14 - Learning Bayesian Networks from Data

Parameters (CPTs) can be learned from data:

- **Complete data:** maximum likelihood estimates = observed frequencies (with Bayesian smoothing/pseudocounts for sparse data)
- **Incomplete data (missing values):** Expectation-Maximization (EM) - iterate E-step (expected sufficient statistics) and M-step (re-estimate parameters)

Structure can also be learned:

- **Score-based:** search over DAGs maximizing a score (e.g., BIC, Bayesian score) penalizing complexity
- **Constraint-based:** use conditional independence tests from data to infer edges

Structure learning is hard (super-exponential number of DAGs); heuristic search (greedy hill climbing, MCMC) is standard.

Text Note 05 notes that larger networks require more computation and data, and more data does not guarantee better performance without suitable structure.

---

## Slide 15 - Dynamic Bayesian Networks and Temporal Models

For domains evolving over time, **Dynamic Bayesian Networks (DBNs)** replicate the network at each time step with temporal arcs:

- Hidden Markov Model: single hidden state Xₜ, observations Eₜ, arcs Xₜ→Xₜ₊₁, Xₜ→Eₜ
- Used for speech recognition, robot localization (Text Note 11 - SLAM), bioinformatics

Inference (filtering, prediction, smoothing) uses the same VE/sampling methods unrolled over time. Text Note 11 (Robotics) describes localization and SLAM as estimating state over time from noisy sensors - a DBN application.

---

## Slide 16 - Uncertainty, Bias, and Fairness (Text Notes 18–19)

Probabilistic models inherit data limitations:

- **Skewed training data** produces biased conditional probability estimates
- **Historical discrimination** appears as statistical associations (e.g., P(Default | Group) differing by group due to past lending practices, not risk)
- **Measurement error** corrupts CPTs

Text Note 18 lists bias sources: unrepresentative data, historical inequality, incorrect labels, poor objectives, inappropriate assumptions, measurement error, deployment context.

Text Note 19 describes bias detection: examine data distribution, test across groups, evaluate ranking, assess stereotype reproduction. Mitigation requires human oversight, transparent reporting, and sometimes adjusting objectives or collecting better data.

A Bayesian network giving P(LoanApproved | Group, Income, Credit) must be audited to ensure group differences reflect genuine risk, not historical bias.

---

## Slide 17 - Probabilistic Reasoning in Language Models

Text Notes 07-08 connect probability to language modeling. A language model estimates P(next token | previous tokens), a high-dimensional conditional distribution learned from text. Text generation samples from this distribution (greedy decoding or temperature sampling), and perplexity measures how well the model assigns probability to held-out text.

These models are essentially enormous probabilistic graphical models where each token is a random variable conditioned on all preceding tokens. The same probability calculus from Chapters 13-14 underlies both small Bayesian networks and large language models, though inference in the latter is approximated by the forward pass of a neural network rather than exact variable elimination.

---

## Slide 18 - From Bayesian Networks to Causal Inference

Bayesian networks encode conditional independencies, but whether their arcs represent true causal mechanisms is a separate question. Two variables can be correlated without one causing the other (a confounder may explain both). Causal inference extends Bayesian networks by requiring that arcs represent direct causal influence and by using do-calculus to reason about interventions: "what happens if we force X = x?" rather than merely "what is P(Y | X = x)?"

This distinction matters for AI systems that act in the world. A recommender system that correlates ice cream sales with drowning incidents should not conclude that ice cream causes drowning; both are caused by hot weather. Causal reasoning helps AI avoid such mistakes and make better decisions under intervention.

---

## Slide 19 - Summary: Key Takeaways

1. Bayesian networks factor the joint via conditional independence: P(X₁,...,Xₙ) = Πᵢ P(Xᵢ | Parents(Xᵢ))
2. Structure is a DAG; each node has a CPT; local Markov condition asserts conditional independence
3. Compact when variables have few parents; CPT size grows exponentially with parent count
4. Inference tasks: posterior, evidence probability, MPE; exact inference is #P-complete
5. Inference by enumeration sums the joint; variable elimination pushes summations inward (complexity exponential in treewidth)
6. Polytrees admit linear-time exact inference; approximate sampling (likelihood weighting, Gibbs) scales to large networks
7. Networks support both causal and diagnostic reasoning from the same joint
8. Parameters and structure can be learned from data (MLE, EM for missing data, score/constraint-based structure search)
9. DBNs extend to temporal domains (HMMs, robot localization/SLAM)
10. Probabilistic models can encode bias from skewed data; auditing and human oversight are essential

---

## Slide 20 - Review Questions

1. What does a Bayesian network's structure (DAG) and CPTs jointly specify?
2. State the local Markov condition and the chain-rule factorization of the joint.
3. In the Alarm network, are JohnCalls and MaryCalls conditionally independent given Alarm? Why?
4. What is D-separation, and what is it used for?
5. Describe the steps to construct a Bayesian network. Why does variable ordering matter?
6. Why is exact inference #P-complete, and how does variable elimination improve on enumeration?
7. What is treewidth, and how does it affect variable elimination complexity?
8. Contrast rejection sampling and likelihood weighting. When is each preferable?
9. How does Gibbs sampling estimate a posterior, and what role does the Markov blanket play?
10. What is the difference between parameter learning and structure learning?
11. Describe EM for learning with incomplete data.
12. How do Dynamic Bayesian Networks extend static BNs, and name an application from robotics (Text Note 11).
13. How can Bayesian networks encode algorithmic bias, and what auditing steps does Text Note 19 recommend?
14. Give one advantage of Bayesian networks over rule-based systems for diagnostic reasoning.
