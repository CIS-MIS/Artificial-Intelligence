# Homework 07: Probability and Bayesian Networks

**Chapters:** 13 (Uncertainty and Probabilistic Reasoning I) and 14 (Probabilistic Reasoning II - Bayesian Networks)
**Estimated time:** 3–4 hours
**Total points:** 100

---

## Instructions

Answer all questions thoroughly. For probability calculations, show each step and state any assumptions (e.g., independence, base rates). For Bayesian network questions, show the factorization of the joint distribution and any summations. Submissions should be typed, with question numbers clearly labeled.

---

## Part A: Foundations of Probability (Chapter 13) - 50 points

### Question 1: Axioms and Theorems (15 points)

(a) State the three axioms of probability (Kolmogorov). (6 points)

(b) From the axioms, derive P(¬a) = 1 − P(a). Show each step. (5 points)

(c) State the product rule and the definition of conditional probability. (4 points)

### Question 2: Bayes' Rule and Medical Diagnosis (20 points)

A doctor uses a test for a rare disease. Given:

- P(Disease) = 0.001 (base rate: 1 in 1000)
- P(Positive | Disease) = 0.99 (sensitivity)
- P(Positive | ¬Disease) = 0.01 (false-positive rate; specificity = 0.99)

(a) Compute P(Disease | Positive) using Bayes' rule. Show the full calculation, including the computation of P(Positive) via the law of total probability. (10 points)

(b) Despite a positive test result, the posterior probability of disease is below 10%. Explain this result in terms of the base rate fallacy. Why does ignoring the base rate lead to overconfident diagnoses? (6 points)

(c) Suppose the disease were common instead, with P(Disease) = 0.1. Recompute P(Disease | Positive) with the same test characteristics. How does the posterior change, and why? (4 points)

### Question 3: Joint Distribution and Marginalization (15 points)

Consider two Boolean random variables: Cavity (C) and Toothache (T). The joint distribution is:

|         | T=true | T=false |
| ------- | ------ | ------- |
| C=true  | 0.04   | 0.06    |
| C=false | 0.01   | 0.89    |

(a) Compute P(Cavity) by marginalizing over Toothache. (4 points)

(b) Compute P(Toothache) by marginalizing over Cavity. (4 points)

(c) Compute P(Cavity | Toothache) using the definition of conditional probability. (4 points)

(d) Are Cavity and Toothache independent? Justify your answer by comparing P(Cavity ∧ Toothache) to P(Cavity) × P(Toothache). (3 points)

---

## Part B: Bayesian Networks (Chapter 14) - 50 points

### Question 4: Network Structure and Semantics (15 points)

Consider the classic Alarm network with variables: Burglary (B), Earthquake (E), Alarm (A), JohnCalls (J), MaryCalls (M). The structure is: B → A, E → A, A → J, A → M.

(a) Write the chain-rule factorization of the joint distribution P(B, E, A, J, M) implied by this network. (5 points)

(b) State the local Markov condition for this network: which variables is each node conditionally independent of, given its parents? (5 points)

(c) Are JohnCalls and MaryCalls conditionally independent given Alarm? Explain using the network structure. (5 points)

### Question 5: Inference by Enumeration and Variable Elimination (20 points)

Using the Alarm network from Question 4, suppose we want to compute P(Burglary | JohnCalls = true).

(a) Write the expression for P(B | J=true) using enumeration over the non-evidence, non-query variables (E, A, M). (5 points)

(b) Perform variable elimination to compute P(B | J=true). Show:

- Eliminate M: what factor results?
- Eliminate A: what new factor τ(B, E) results?
- Eliminate E: what factor τ'(B) results?
- Final normalization to obtain P(B=true | J=true) and P(B=false | J=true).

You may leave the arithmetic in terms of the CPT entries (e.g., P(A=true | B=true, E=true)) rather than computing final decimal values, but show the structure of each eliminated factor clearly. (15 points)

### Question 6: Approximate Inference (10 points)

(a) Describe likelihood weighting. How does it differ from rejection sampling, and why is it better for rare evidence? (6 points)

(b) Describe Gibbs sampling (MCMC). What is the Markov blanket of a node, and how is it used in Gibbs sampling? (4 points)

### Question 7: Bias, Fairness, and Causality (10 points)

(a) Text Note 18 lists sources of algorithmic bias. Name three sources and give a one-sentence example of how each could distort a Bayesian network's conditional probability tables. (6 points)

(b) Explain the difference between correlation and causation in a Bayesian network. Give an example of two variables that might be correlated in a network but not causally related (e.g., a common cause). (4 points)

---

## Grading Rubric

| Section                               | Points        |
| ------------------------------------- | ------------- |
| Q1 (Axioms)                           | 15            |
| Q2 (Bayes/Medical)                    | 20            |
| Q3 (Joint/Marginalization)            | 15            |
| Q4 (Network Structure)                | 15            |
| Q5 (Enumeration/Variable Elimination) | 20            |
| Q6 (Approximate Inference)            | 10            |
| Q7 (Bias/Causality)                   | 10            |
| **Total**                       | **100** |

---

## Suggested Length

A complete submission is approximately 6–9 pages, including probability tables, derivations, and network diagrams.
