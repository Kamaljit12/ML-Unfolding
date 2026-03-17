Excellent — now we’re stepping into *core ML theory*.  
I’ll take you deep, but keep it structured so you can *build intuition + math + implementation*.

## `1. BIAS vs VARIANCE (DEEP DIVE)`

🔹 Core Idea:
We are trying to approximate a true function:

y = f(x) + noise

But our model learns:
ŷ = f̂(x)

🔹 Error Decomposition (VERY IMPORTANT):

Expected Error =
Bias² + Variance + Irreducible Error

👉 This is the most important equation in ML.

## `🔹 BIAS`

Bias = error due to wrong assumptions

Example:
- Using linear model for non-linear data

👉 High Bias:
- Underfitting
- Model too simple

## `🔹 VARIANCE`

Variance = how much model changes with different data

👉 High Variance:
- Overfitting
- Model memorizes training data

## `🔹 TRADEOFF`

- Simple model → High Bias, Low Variance
- Complex model → Low Bias, High Variance

👉 Goal:
Find balance (sweet spot)

## `🔹 INTUITION GRAPH`

::contentReference[oaicite:0]{index=0}


Think:
- Linear model trying to fit this → high bias
- Very complex model → overfits noise → high variance

## `🔹 RESEARCH INSIGHT`

Modern ML (Deep Learning):
- Very low bias
- Controlled variance via:
  - Regularization
  - Dropout
  - Data augmentation

## `2. PCA (FROM SCRATCH UNDERSTANDING)


🔹 Problem:
Features are correlated → redundant info

Example:
Height (cm), Height (inch)

## `🔹 GOAL:`

- Reduce dimensions
- Keep maximum information (variance)

## ` 🔹 INTUITION:

Imagine data cloud:

Instead of x, y axes →
Rotate axes to align with maximum spread

These new axes = Principal Components

## `🔹 STEPS (MATHEMATICAL)`

1. Center data:
X = X - mean

2. Compute covariance matrix:
C = (1/n) XᵀX

3. Eigen decomposition:
C v = λ v

- v = direction (principal component)
- λ = variance along that direction

4. Sort eigenvalues (descending)

5. Project data:
X_new = X · V

## `🔹 WHY IT WORKS:`

Eigenvectors = directions of maximum variance

## `🔹 FROM SCRATCH CODE (NUMPY)`

```
# Python
import numpy as np

def pca(X, k):
    # Step 1: mean center
    X_meaned = X - np.mean(X, axis=0)

    # Step 2: covariance matrix
    cov = np.cov(X_meaned, rowvar=False)

    # Step 3: eigen decomposition
    eigenvalues, eigenvectors = np.linalg.eigh(cov)

    # Step 4: sort
    idx = np.argsort(eigenvalues)[::-1]
    eigenvectors = eigenvectors[:, idx]

    # Step 5: select top k
    eigenvectors = eigenvectors[:, :k]

    # Step 6: project
    return np.dot(X_meaned, eigenvectors)
```
