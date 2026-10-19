# Homework 08: Supervised Learning

**Chapter:** 15 (Supervised Learning)
**Related background:** Chapter 2 (utility-based agents), Chapter 6 (local search / gradient descent)
**Estimated time:** 3–4 hours
**Total points:** 100

---

## Instructions

Answer all questions thoroughly. For calculations, show each step. For design questions, justify your choices. Submissions should be typed, with question numbers clearly labeled.

---

## Part A: Foundations of Supervised Learning - 50 points

### Question 1: What Is Supervised Learning? (15 points)

(a) Define supervised learning. Distinguish between classification (discrete target) and regression (continuous target), giving one example of each. (6 points)

(b) Formalize the learning problem: given training examples D = {(x⁽ⁱ⁾, y⁽ⁱ⁾)} drawn from an unknown distribution P(X, Y), the learner chooses a hypothesis h to minimize expected risk. Write the expected risk R(h) and the empirical risk R̂(h), and explain the difference. (6 points)

(c) What is the generalization gap, and why is it the central challenge of supervised learning? (3 points)

### Question 2: Decision Trees (15 points)

(a) Describe how a decision tree is grown top-down (e.g., ID3/C4.5/CART). What criterion is used to select the feature to split on at each node? (6 points)

(b) Define entropy H(Y) and information gain IG(Y, X). (5 points)

(c) Decision trees are interpretable but prone to overfitting. Name two techniques to reduce overfitting in decision trees. (4 points)

### Question 3: Linear Models (10 points)

(a) Write the equation for linear regression: ŷ = w·x + b. Explain what w and b represent. (4 points)

(b) Write the equation for linear (binary) classification using a sign or threshold: ŷ = sign(w·x + b). How does logistic regression differ by producing a probability? (3 points)

(c) Name one limitation of linear models (without feature engineering). (3 points)

### Question 4: Neural Networks and Backpropagation (15 points)

(a) Describe the forward pass of a single neuron: weighted sum, bias, activation function. Name two common activation functions. (5 points)

(b) Distinguish backpropagation from gradient descent: what does each compute or do? (5 points)

(c) Name two loss functions: one appropriate for regression and one appropriate for classification. (5 points)

---

## Part B: Evaluation, Overfitting, and the ML Pipeline - 50 points

### Question 5: Classification Metrics (15 points)

Given the following confusion matrix for a binary classifier (rows = actual, columns = predicted):

|                 | Predicted Negative | Predicted Positive |
| --------------- | ------------------ | ------------------ |
| Actual Negative | 80                 | 10                 |
| Actual Positive | 5                  | 35                 |

(a) Compute accuracy. (3 points)

(b) Compute precision. (3 points)

(c) Compute recall (sensitivity). (3 points)

(d) Compute the F1 score. (3 points)

(e) In a fraud-detection setting, would you prioritize precision or recall? Why? (3 points)

### Question 6: Regression Metrics (10 points)

(a) Define RMSE and R². What does each measure? (6 points)

(b) If a regression model has R² = 0.75, interpret this value. (4 points)

### Question 7: Train/Validation/Test Split and Overfitting (15 points)

(a) Explain why the test set must remain separate from hyperparameter tuning. What is the role of the validation set? (6 points)

(b) What are the signs of overfitting? Name three techniques to reduce overfitting. (6 points)

(c) Explain the bias-variance trade-off in one paragraph: what is bias, what is variance, and how does model complexity affect each? (3 points)

### Question 8: The Supervised Learning Pipeline (10 points)

List the stages of a complete supervised learning pipeline, from problem formulation to deployment. For each stage, give a one-sentence description. (10 points)

### Question 9: Real-World Caveats (10 points)

(a) What is distribution shift, and why does it matter when deploying a trained model? (4 points)

(b) Name two ways that training data can introduce bias into a supervised learning model, and one mitigation strategy for each. (6 points)

---

## Grading Rubric

| Question        | Points        |
| --------------- | ------------- |
| 1               | 15            |
| 2               | 15            |
| 3               | 10            |
| 4               | 15            |
| 5               | 15            |
| 6               | 10            |
| 7               | 15            |
| 8               | 10            |
| 9               | 10            |
| **Total** | **100** |

---

## Suggested Length

A complete submission is approximately 5–7 pages, including calculations, tables, and short essays.
