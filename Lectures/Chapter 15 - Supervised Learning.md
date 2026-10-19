# Artificial Intelligence - Chapter 15: Supervised Learning

## Lecture Note Slides (20 Slides)

**Source Materials:** AI - Chapter 18/19 (textbook: Learning); AI Lecture Notes 03–08 (Neural Networks, Training, NLP, Language Models); AI Lecture Notes 09 (Reinforcement Learning); AI Lecture Notes 15–17 (Recommender Systems)

---

## Slide 1 - Supervised Learning

**Supervised Learning: From Labeled Data to Predictive Models**

Chapter 15 - Learning from Examples

A scholarly treatment of supervised learning: problem formulation, decision trees, linear models, neural networks, evaluation, overfitting, and the full machine-learning pipeline.

---

## Slide 2 - What Is Supervised Learning?

Supervised learning is learning a function f: X → Y from labeled examples (xᵢ, yᵢ), where xᵢ is an input feature vector and yᵢ is the known target (label).

The learner's job: produce a hypothesis h that approximates f, so h(x) predicts y for new, unseen inputs.

Tasks:

- **Classification:** Y is discrete (spam/not spam, digit 0–9, letter A–Z)
- **Regression:** Y is continuous (house price, temperature, attendance)

Supervised learning contrasts with:

- **Unsupervised learning** (Text Note 06): no labels; discover structure (clustering, K-means, autoencoders)
- **Reinforcement learning** (Text Note 09): learn from reward signals, not labeled examples

Text Note 05 formalizes: training set fits parameters; testing set evaluates unseen performance; validation set tunes hyperparameters.

---

## Slide 3 - The Learning Problem: Formal Setup

A hypothesis space H is the set of candidate functions the learner may choose from.

Given:

- Training examples D = {(x⁽¹⁾, y⁽¹⁾), ..., (x⁽ⁿ⁾, y⁽ⁿ⁾)} drawn i.i.d. from an unknown distribution P(X, Y)
- A loss function L(y, h(x)) measuring prediction error
- A hypothesis class H

Goal: choose h* ∈ H minimizing expected risk:
R(h) = E₍ₓ,ᵧ₎[L(y, h(x))]

Since P(X, Y) is unknown, we minimize **empirical risk** on training data:
R̂(h) = (1/n) Σᵢ L(y⁽ⁱ⁾, h(x⁽ⁱ⁾))

The gap between empirical and expected risk is the **generalization gap** - the core challenge of supervised learning.

---

## Slide 4 - Decision Trees

A decision tree is a flowchart-like structure: internal nodes test features, branches represent outcomes, leaves predict classes/values.

ID3/C4.5/CART algorithms grow trees top-down:

1. Select the best feature to split on (maximizing information gain / minimizing impurity)
2. Partition examples by feature value
3. Recurse on each partition
4. Stop when pure, small, or no features remain

**Information gain:** IG(Y, X) = H(Y) − H(Y | X), where H is entropy. Choose the feature reducing uncertainty most.

**Entropy:** H(Y) = −Σ_y P(y) log₂ P(y) - measures label uncertainty.

Decision trees are interpretable (white-box) but can overfit; pruning (reduced-error, cost-complexity) addresses this.

Example (Text Note 10-style): loan approval based on credit score, income, debt - tree splits on thresholds.

---

## Slide 5 - Linear Regression and Linear Classification

**Linear regression:** predicts a continuous target:
ŷ = w·x + b = Σⱼ wⱼxⱼ + b

Fit by minimizing squared error (Text Note 04):
L = (1/n) Σᵢ (y⁽ⁱ⁾ − ŷ⁽ⁱ⁾)²

**Linear classification (logistic regression / perceptron):** predicts discrete class via a decision boundary:
ŷ = sign(w·x + b) or σ(w·x + b) for probability

Text Note 04 details the swimming-pool example: predict attendance from temperature using ŷ = wx + b, extended to multiple features ŷ = w₁x₁ + ... + wₙxₙ + b.

Linear models are simple, interpretable, and efficient but cannot capture nonlinear relationships without feature engineering.

---

## Slide 6 - Neural Networks as Function Approximators

Neural networks compose many simple units into flexible nonlinear functions (Text Notes 03–05).

A neuron computes:
z = w·x + b; output = a(z)

where a is an activation function (sigmoid, ReLU, tanh, softmax).

Layers:

- Input: features x
- Hidden: transform representations
- Output: prediction (class scores or regression value)

Forward propagation (Text Note 03): inputs → weights → bias → activation → output; passes layer to layer.

Text Note 04: neural networks extend linear regression by combining many weighted neurons across layers, learning complex relationships among numerous features.

---

## Slide 7 - Training Neural Networks: Backpropagation and Gradient Descent

Training minimizes loss L over parameters (weights w, biases b):

**Gradient descent update** (Text Note 04):
w_new = w_old − η ∇L/∂w

where η is the learning rate; ∇L/∂w is the gradient computed via **backpropagation** (chain rule backward from output to input).

Process per epoch:

1. Forward pass: compute predictions
2. Loss: compare predictions to labels
3. Backward pass: compute gradients
4. Update: adjust parameters
5. Repeat across epochs and mini-batches

Text Note 04 distinguishes backpropagation (computes gradients) from gradient descent (uses them to update parameters).

Loss functions: MSE for regression; cross-entropy for classification (binary or categorical).

---

## Slide 8 - Loss Functions for Supervised Learning

Task-appropriate losses:

**Regression:**

- MSE = (1/n) Σ(yᵢ − ŷᵢ)² - penalizes large errors heavily
- MAE = (1/n) Σ|yᵢ − ŷᵢ| - robust to outliers

**Classification:**

- Binary cross-entropy: −[y log ŷ + (1−y) log(1−ŷ)]
- Categorical cross-entropy: −Σᵧ yᵧ log ŷᵧ (softmax output)

Text Notes 04–05 cover MSE, MAE, cross-entropy. Text Note 05 (handwritten letters) uses cross-entropy implicitly via MLPClassifier; accuracy is the reported metric.

Lower training loss indicates better fit but not necessarily better generalization - overfitting risk (Text Note 04).

---

## Slide 9 - Evaluation: Classification Metrics

Beyond raw accuracy, richer metrics:

- **Accuracy:** correct / total (Text Note 05: 84% → 88% on EMNIST)
- **Precision:** TP / (TP + FP) - of predicted positives, how many are truly positive
- **Recall (Sensitivity):** TP / (TP + FN) - of true positives, how many found
- **F1:** harmonic mean of precision and recall
- **Confusion matrix** (Text Note 05): rows = actual, columns = predicted; diagonal = correct; off-diagonal = confusions (e.g., U↔V, I↔L)

Threshold choice trades precision vs. recall (e.g., fraud detection favors recall; spam filtering favors precision).

ROC curve and AUC summarize performance across thresholds.

---

## Slide 10 - Evaluation: Regression and Generalization

**Regression metrics:**

- RMSE = √MSE - in same units as target
- R² = 1 − SS_res / SS_tot - fraction of variance explained

**Train/validation/test split** (Text Notes 04–05):

- Training data: fit parameters
- Validation data: tune hyperparameters, model selection
- Test data: final independent evaluation (do not use for tuning)

Generalization = performance on unseen data. Text Note 04's exam analogy: memorizing practice answers ≠ understanding; test on new questions measures true learning.

Text Note 05 warns: 88% test accuracy does not mean 88% of a real document is readable - real-world distribution may differ (distribution shift).

---

## Slide 11 - Overfitting and Generalization

**Overfitting** (Text Note 04): model learns training data too closely, including noise and coincidental correlations; performs poorly on unseen data.

Signs: very low training loss, much higher validation/test loss.

Causes (Text Notes 04–05):

- Too many irrelevant features (grass length, butterfly count predicting pool attendance)
- Excessive model capacity (too many neurons/layers)
- Too many epochs relative to data

**Techniques to reduce overfitting** (Text Note 04):

- Remove irrelevant features
- Use a simpler model
- Collect more representative data
- Regularization (L2: penalize ‖w‖²)
- Early stopping (monitor validation, stop when it degrades)
- Data augmentation (rotate/crop images preserving class)

Text Note 06 adds: representation learning and autoencoders learn compact features, indirectly aiding generalization.

---

## Slide 12 - Bias-Variance Trade-off

Expected error decomposes:
Error = Bias² + Variance + Irreducible noise

- **Bias:** error from overly simple assumptions (underfitting)
- **Variance:** error from sensitivity to training data fluctuations (overfitting)
- **Irreducible noise:** inherent randomness in labels

High bias (linear model on nonlinear data) underfits. High variance (deep tree memorizing noise) overfits. The optimal model balances both.

Complexity control: regularization strength, tree depth, network size, epochs. Validation data guides selection.

Text Note 04: reaching exact global minimum is not necessary; sufficiently low loss with strong generalization suffices.

---

## Slide 13 - The Full Supervised Learning Pipeline

(Text Notes 03–05 formalize these stages)

1. **Problem formulation:** classification vs. regression, features, labels
2. **Data collection:** labeled dataset (EMNIST: 60k train, 10k test)
3. **Preprocessing:** normalization (pixel / 255), handling missing values, feature scaling
4. **Train/validation/test split**
5. **Model selection:** decision tree, linear model, neural network, etc.
6. **Training:** optimization (gradient descent, backprop)
7. **Hyperparameter tuning:** learning rate, layers, neurons, epochs, regularization
8. **Evaluation:** metrics, confusion matrix, held-out test
9. **Deployment & monitoring:** watch for distribution shift, drift, degradation

Text Note 05's complete workflow: collect → preprocess → build → train → evaluate → prepare new data → infer → review.

---

## Slide 14 - Neural Network Case Study: Handwritten Letters (Text Note 05)

EMNIST letters: 28×28 grayscale = 784 features, normalized to [0,1], 26 classes.

MLP architecture (initial): 784 input → 50 hidden → 26 output; 20 epochs; ~84% test accuracy.

Larger: 784 → 5×100 hidden → 26; 50 epochs; ~88% test accuracy (+4 points).

Lessons:

- More capacity/epochs can improve accuracy but costs computation and overfit risk
- Confusion matrix reveals confusions (U↔V, O↔Q)
- Preprocessing must match training at inference (resize 28×28, invert dark→light background, center, smooth)
- 88% accuracy ⇒ ~12% error rate; real documents may differ due to distribution shift

---

## Slide 15 - From Supervised Learning to Language (Text Notes 07–08)

Text Note 07: language modeling as self-supervised next-token prediction - the training targets come from the data itself (no manual labels). Word embeddings capture distributional semantics (words in similar contexts have similar vectors).

Text Note 08: John-Green-bot language model - embedding matrix + RNN, trained via backpropagation on next-token prediction; evaluated with perplexity (train ~45, validation ~72); inference via greedy decoding or sampling.

Key insight: supervised learning principles (loss, backprop, train/val split, overfitting) carry into NLP, though labels are auto-generated (self-supervised).

Limitation (Text Notes 07–08): fluency ≠ understanding; models learn statistical associations, not grounded meaning.

---

## Slide 16 - From Supervised Learning to Recommendation (Text Notes 15–16)

Text Note 15: recommender systems predict user-item preferences. Methods: content-based (item features), popularity-based, personalized, collaborative filtering (user-user or item-item).

Text Note 16: movie recommender with user-user collaborative filtering:

- Ratings matrix (sparse - most user-movie pairs unobserved)
- Missing ≠ negative; unknown preference
- Average ratings + minimum count threshold (reliable averages)
- User vectors in high-dimensional space (one dimension per movie)
- Neighborhood of similar users; predicted ratings for unseen movies
- Group profiles via averaging two users' ratings (may hide disagreement)

Supervised learning angle: predict rating (regression) or click/purchase (classification) from user + item features; cold-start and sparsity are core challenges.

---

## Slide 17 - Practical Considerations and Pitfalls

Common mistakes (Text Notes 04–05, 16):

- Interpreting missing ratings as zero (they're unknown)
- Trusting highest average without checking sample size
- Confusing predictions with facts (predicted rating ≠ actual)
- Assuming larger neighborhood is always better
- Assuming average of two ratings guarantees group satisfaction
- Assuming more data solves everything

Data quality matters (Text Notes 05, 08, 15): preprocessing consistency, label correctness, feature representation, distribution shift between train and inference.

Responsible ML (Text Notes 04, 14, 18): evaluate errors, consider harmful mistakes, check bias, monitor post-deployment, ensure fairness and transparency.

---

## Slide 18 - Supervised Learning in Larger Systems

Supervised learning rarely operates in isolation. It is a component within larger AI systems that combine multiple techniques:

- **Recommender systems (Text Notes 15-16):** Collaborative filtering predicts ratings (a regression task), while ranking and diversity are handled by additional heuristics and business rules.
- **Language models (Text Notes 07-08):** Next-token prediction is self-supervised learning, but decoding (beam search, sampling) and fine-tuning with human feedback (RLHF) add search and reinforcement-learning layers on top.
- **Robotics (Text Note 11):** Supervised learning can map sensor inputs to actions (imitation learning), but the robot must also localize, plan, and react online using search and control.

In each case, supervised learning provides a predictive core, but the full intelligent system requires integrating that core with search, reasoning, control, and human oversight.

---

## Slide 19 - Summary: Key Takeaways

1. Supervised learning learns f: X → Y from labeled (input, target) pairs; classification (discrete) vs. regression (continuous)
2. Empirical risk minimization on training data; generalization gap to unseen data is the central challenge
3. Decision trees split on information gain; interpretable but prone to overfitting without pruning
4. Linear models (regression/classification) are simple and efficient but limited to linear relationships
5. Neural networks compose weighted neurons with activations; trained via forward pass, loss, backpropagation, gradient descent
6. Loss functions: MSE/MAE for regression; cross-entropy for classification
7. Evaluation: accuracy, precision/recall/F1, confusion matrix, RMSE/R²; train/validation/test separation
8. Overfitting: low train loss, high test loss; mitigated by simpler models, fewer features, regularization, early stopping, more data
9. Bias-variance trade-off governs model complexity selection
10. Supervised learning principles extend to NLP (self-supervised next-token prediction) and recommendation (collaborative filtering), with distribution shift and bias as key caveats

---

## Slide 20 - Review Questions

1. Define supervised learning and distinguish classification from regression with examples.
2. What is empirical risk minimization, and what is the generalization gap?
3. How does a decision tree choose splits? What is information gain?
4. Write the linear regression and linear classification equations. What do w and b represent?
5. Describe the forward pass of a neural network neuron: weighted sum, bias, activation.
6. Distinguish backpropagation from gradient descent.
7. Name appropriate loss functions for regression and classification.
8. Compute precision, recall, and F1 from a confusion matrix. When does each matter most?
9. Why must the test set remain separate from hyperparameter tuning?
10. What are the signs of overfitting, and name three techniques to reduce it.
11. Explain the bias-variance decomposition of error.
12. Summarize the EMNIST handwritten-letter experiment: architecture, accuracy change, and preprocessing requirements.
13. How does self-supervised next-token prediction fit the supervised-learning framework?
14. In collaborative filtering, why is a missing rating not a negative rating?
15. Name three pitfalls in supervised-learning practice and how to avoid them.
