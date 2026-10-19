# Project 03: Supervised Learning Pipeline for Image Classification

**Chapter applied:** 15 (Supervised Learning)
**Related background:** Chapter 6 (gradient descent/local search), Chapter 2 (utility-based agents)
**Estimated effort:** ~3 pages of written work plus experimental results
**Format:** Written report with experimental results (tables/charts)
**Total points:** 100

---

## 1. Project Overview

In this project you will build and evaluate a supervised learning pipeline for image classification. You will train a model on a labeled image dataset (e.g., handwritten digits or letters such as MNIST, EMNIST, or a subset), preprocess the data, train and tune the model, evaluate it on a held-out test set, and analyze errors and generalization.

You may use a machine learning library (e.g., scikit-learn, PyTorch, TensorFlow, Keras) or implement a simple model from scratch. The deliverable is a written report (approximately three pages) describing the pipeline, experimental results, and analysis.

---

## 2. Learning Objectives

By completing this project, you will be able to:

- Execute a complete supervised learning pipeline: data collection, preprocessing, train/validation/test split, training, tuning, and evaluation.
- Train and compare at least two model types (e.g., logistic regression and a neural network, or k-nearest neighbors and a decision tree).
- Compute and interpret classification metrics (accuracy, precision, recall, F1, confusion matrix).
- Diagnose overfitting using train/validation/test curves.
- Reflect on data quality, bias, and deployment caveats.

---

## 3. Detailed Instructions

### 3.1 Dataset

Choose a labeled image classification dataset. Recommended options:

- **MNIST / EMNIST digits:** 28x28 grayscale images of handwritten digits 0–9 (10 classes).
- **EMNIST letters:** 28x28 grayscale images of handwritten letters A–Z (26 classes).
- **A small custom dataset:** e.g., photos of cats vs. dogs, resized and flattened.

Each image is represented as a feature vector x (pixel intensities, normalized to [0,1]) and a label y (class). You need at least 1,000 labeled examples with a train/validation/test split.

### 3.2 Models to Compare

Train and compare at least two of the following:

1. **Logistic regression / softmax regression** - a linear multiclass classifier.
2. **k-Nearest Neighbors (k-NN)** - a non-parametric instance-based classifier.
3. **Decision tree** - as discussed in Chapter 15.
4. **Multi-layer perceptron (neural network)** - one or two hidden layers with ReLU activations and softmax output, trained via backpropagation and gradient descent.

You must include at least one linear/model-based method and one nonlinear or instance-based method for meaningful comparison.

---

## 4. Step-by-Step Implementation Guide

### Step 1: Data Collection and Inspection (approximately 0.5 page)

Load the dataset and report:

- Number of samples, image dimensions, number of classes.
- Class distribution (are classes balanced?).
- Example: "EMNIST letters: 28x28 = 784 features, 26 classes, ~124,800 training samples."

If classes are imbalanced, note how this may affect accuracy and whether you will use stratified sampling.

### Step 2: Preprocessing (approximately 0.5 page)

Describe and apply preprocessing:

- **Flattening:** convert each 28x28 image to a 784-dimensional vector.
- **Normalization:** divide pixel values by 255 to scale to [0,1].
- **Train/validation/test split:** e.g., 70% train, 15% validation, 15% test, stratified by class.
- **Optional:** data augmentation (small rotations/shifts), dimensionality reduction (PCA).

Emphasize that the same preprocessing must be applied at training and inference time.

### Step 3: Model Training (approximately 0.75 page)

For each model:

- Specify hyperparameters (e.g., k for k-NN; max depth for decision tree; learning rate, hidden layers, epochs for neural network).
- Describe the training procedure:
  - Logistic regression: minimize cross-entropy via gradient descent.
  - Neural network: forward pass → cross-entropy loss → backpropagation → weight update.
- Record training loss/accuracy per epoch.

### Step 4: Hyperparameter Tuning (approximately 0.5 page)

Use the validation set to select hyperparameters. For example:

- k-NN: try k ∈ {1, 3, 5, 7, 9}; pick the k with highest validation accuracy.
- Neural network: try learning rate ∈ {0.001, 0.01, 0.1}; hidden units ∈ {50, 100, 200}.

Do **not** use the test set for tuning. Report the chosen hyperparameters and validation performance.

### Step 5: Final Evaluation on Test Set (approximately 0.75 page)

Evaluate each tuned model on the held-out test set. Report:

- **Accuracy:** correct predictions / total.
- **Confusion matrix:** rows = actual class, columns = predicted class.
- **Precision, recall, F1:** per class and macro-averaged.

Present results in a table:

| Model               | Test Accuracy | Test Precision (macro) | Test Recall (macro) | Test F1 (macro) | Training Time |
| ------------------- | ------------- | ---------------------- | ------------------- | --------------- | ------------- |
| Logistic Regression |               |                        |                     |                 |               |
| k-NN (k=__)         |               |                        |                     |                 |               |
| Neural Network      |               |                        |                     |                 |               |

### Step 6: Overfitting Analysis (approximately 0.75 page)

For at least one model (preferably the neural network or decision tree), plot or describe:

- Training accuracy/loss vs. validation accuracy/loss over epochs or model complexity.
- Identify whether the model is underfitting (high train and test error) or overfitting (low train error, high test error).

Discuss:

- Which model overfit the most?
- What techniques could reduce overfitting (regularization, early stopping, fewer features, more data)?

### Step 7: Error Analysis and Bias Reflection (approximately 0.5 page)

- Examine the confusion matrix: which classes are most often confused? (e.g., in EMNIST, U↔V, O↔Q, I↔L).
- Offer a hypothesis for why these confusions occur (e.g., similar glyph shapes).
- Reflect on data quality and bias (Text Notes 04, 05, 15–18):
  - Are some classes underrepresented?
  - Could preprocessing (e.g., image inversion, centering) introduce systematic error?
  - What would happen if the test distribution shifted (e.g., different handwriting style)?

---

## 5. Deliverables and Formatting

Submit:

1. A written report (~3 pages, single-spaced, 11–12 point font) containing:
   - Dataset description and preprocessing.
   - Model descriptions and hyperparameters.
   - Results table and confusion matrices.
   - Overfitting analysis.
   - Error analysis and bias reflection.
   - Conclusion.
2. (Optional but encouraged) Source code or a notebook as a separate file or appendix.
3. A short bibliography citing the course text (AI, Chapter 15) and lecture notes (Text Notes 03–09, 15–18).

---

## 6. Grading Rubric

| Component                                        | Points        |
| ------------------------------------------------ | ------------- |
| Dataset description and preprocessing            | 15            |
| Model training and tuning (two+ models)          | 25            |
| Test-set evaluation and metrics table            | 20            |
| Overfitting analysis (train vs. validation/test) | 15            |
| Error analysis and bias reflection               | 15            |
| Clarity, formatting, citations                   | 5             |
| **Total**                                  | **100** |

---

## 7. Optional Extensions (for extra credit)

- Implement a model from scratch (logistic regression with gradient descent) and compare to a library implementation.
- Test robustness to distribution shift: train on centered digits, test on shifted/noisy digits.
- Visualize learned weights (e.g., as 28x28 images for a linear classifier) or misclassified examples.
- Compare training time and inference time across models.
