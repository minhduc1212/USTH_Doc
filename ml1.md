# Machine Learning 1: Comprehensive Study Guide
**Authored by: Your Machine Learning Professor**

## Table of Contents
1. [Introduction to Supervised Learning](#1-introduction-to-supervised-learning)
2. [Linear Regression: Predicting Continuous Values](#2-linear-regression-predicting-continuous-values)
3. [Logistic Regression: Binary Classification](#3-logistic-regression-binary-classification)
4. [Optimization: Gradient Descent & Newton’s Method](#4-optimization-gradient-descent--newtons-method)
5. [Regularization: Solving Overfitting](#5-regularization-solving-overfitting)
6. [Model Evaluation: Measuring Performance](#6-model-evaluation-measuring-performance)
7. [Artificial Neural Networks: The Foundation of Deep Learning](#7-artificial-neural-networks-the-foundation-of-deep-learning)

---

## 1. Introduction to Supervised Learning
In **Supervised Learning**, we teach a computer by showing it examples. Each example has an **input (x)** and a known **correct answer (y)**.
*   **Analogy:** Think of a student (the model) learning from a textbook where the answers are in the back. By seeing enough problems and their solutions, the student learns the underlying "logic" to solve new problems they haven't seen before.

---

## 2. Linear Regression: Predicting Continuous Values
Linear Regression is used when we want to predict a specific number (e.g., house prices, stock values).

### The Hypothesis Function
The simplest form is a straight line:
$$h_\theta(x) = \theta_0 + \theta_1x$$
*   **$\theta_0$ (Bias/Intercept):** Where the line hits the y-axis.
*   **$\theta_1$ (Weight/Slope):** How much $y$ changes for every 1 unit of $x$.
*   **Intuition:** If you are predicting house prices based on size, $\theta_0$ might be the base price of the land, and $\theta_1$ is the cost per square meter.

### The Cost Function: Mean Squared Error (MSE)
To find the "best" line, we need to measure how "wrong" our current line is.
$$E(\theta) = \frac{1}{2m} \sum_{i=1}^{m} (h_\theta(x^{(i)}) - y^{(i)})^2$$
*   **$m$:** Number of training examples.
*   **$(h_\theta(x) - y)$:** The **error** (Prediction - Actual).
*   **Square ($^2$):** We square the error to make it positive (so negative and positive errors don't cancel out) and to penalize large errors more heavily.
*   **$\frac{1}{2m}$:** We divide by $m$ to get the average error and by $2$ to make the math easier during calculus (it cancels out the square).

### Practical Numerical Example (Linear Regression)
**Data:** 1 house, 50m², Price 2.5 Billion VND.
**Model:** Let's start with $\theta_0 = 0$ and $\theta_1 = 0.1$.
1.  **Predict:** $h(50) = 0 + 0.1(50) = 5.0$ Billion.
2.  **Calculate Error:** $5.0 - 2.5 = 2.5$ Billion error.
3.  **Cost:** $E = \frac{1}{2(1)} (2.5)^2 = 3.125$.
*The goal of the algorithm is now to change $\theta$ to make this number smaller.*

---

## 3. Logistic Regression: Binary Classification
Logistic Regression is used for **Yes/No** questions (e.g., Is this email spam? Is this house in District A?).

### The Sigmoid Function
Linear lines can predict values like -500 or +1,000,000, which doesn't make sense for "Yes/No". We use the **Sigmoid Function** to squash any number into a range between **0 and 1**.
$$g(z) = \frac{1}{1 + e^{-z}}$$
Our hypothesis becomes:
$$h_\theta(x) = g(\theta^T x) = \frac{1}{1 + e^{-\theta^T x}}$$
*   **Interpretation:** $h_\theta(x)$ is the **probability** that the answer is "Yes" (1). If $h_\theta(x) = 0.7$, there is a 70% chance it is positive.

### Decision Boundary
*   Predict $y=1$ if $h_\theta(x) \geq 0.5$ (which happens when $\theta^T x \geq 0$).
*   Predict $y=0$ if $h_\theta(x) < 0.5$.

---

## 4. Optimization: Gradient Descent & Newton’s Method
How does the model actually "learn"? It iterates to find the minimum of the Cost Function.

### Gradient Descent
$$ \theta_j := \theta_j - \alpha \frac{\partial}{\partial \theta_j} E(\theta) $$
*   **$\alpha$ (Learning Rate):** The "step size". If it's too big, you might overstep the minimum. If it's too small, it takes forever to learn.
*   **$\frac{\partial}{\partial \theta_j} E(\theta)$:** The "direction". It tells us which way is "downhill".
*   **Analogy:** You are on a dark mountain and want to find the valley. You feel the slope with your feet and take a step in the steepest downward direction.

### Newton's Method (Alternative)
Instead of taking many small steps, Newton's method uses calculus to find the minimum faster.
$$\theta^{t+1} = \theta^t - H^{-1} \Delta_\theta E$$
*   **$H$ (Hessian Matrix):** Contains the second derivatives (the curvature of the hill).
*   **Comparison:**
    | Feature | Gradient Descent | Newton's Method |
    | :--- | :--- | :--- |
    | **Speed** | Needs many iterations | Very few iterations |
    | **Complexity** | Simple $O(n)$ | Expensive $O(n^3)$ |
    | **Scaling** | Good for large feature sets | Best for small feature sets |

---

## 5. Regularization: Solving Overfitting
Sometimes a model learns the "noise" or "accidental details" of the training data instead of the actual pattern. This is **Overfitting**.

*   **Underfitting:** The model is too simple (High Bias).
*   **Overfitting:** The model is too complex (High Variance).

### The Solution: Penalizing Complexity
We add a "penalty" to the cost function for having large weights ($\theta$):
$$E(\theta)_{reg} = E(\theta) + \frac{\lambda}{2m} \sum_{j=1}^{n} \theta_j^2$$
*   **$\lambda$ (Regularization Parameter):** Controls the tradeoff. 
    *   If $\lambda$ is huge, the model becomes too simple (underfitting).
    *   If $\lambda$ is 0, the model stays overfitted.
*   **Intuition:** It forces the model to keep weights small, making the prediction curve "smoother" and less likely to wig out over single data points.

---

## 6. Model Evaluation: Measuring Performance

### Regression Metrics
1.  **MAE (Mean Absolute Error):** Average of the raw errors.
2.  **MSE (Mean Squared Error):** Highlights large errors.
3.  **$R^2$ (Coefficient of Determination):** How much of the variance is explained by the model (1.0 is perfect).

### Classification Metrics (The Confusion Matrix)
| | Predicted 1 | Predicted 0 |
| :--- | :--- | :--- |
| **Actual 1** | True Positive (TP) | False Negative (FN) |
| **Actual 0** | False Positive (FP) | True Negative (TN) |

*   **Accuracy:** $\frac{TP + TN}{Total}$ (Overall correctness).
*   **Precision:** $\frac{TP}{TP + FP}$ (When I say "Yes", how often am I right?).
*   **Recall (Sensitivity):** $\frac{TP}{TP + FN}$ (Of all the actual "Yes" cases, how many did I catch?).
*   **F1-Score:** $2 \cdot \frac{Precision \cdot Recall}{Precision + Recall}$ (A balance of both).

---

## 7. Artificial Neural Networks
Inspired by the human brain, ANNs use layers of "neurons" to learn complex, non-linear patterns.

### The Single Neuron (Perceptron)
It takes inputs ($x$), multiplies them by weights ($w$), adds them up, and passes them through an **Activation Function**.
1.  **Net Input:** $z = \sum w_i x_i = w^T x$
2.  **Output:** $a = f(z)$

### Popular Activation Functions
*   **Sigmoid:** Used for probabilities (0 to 1).
*   **ReLU (Rectified Linear Unit):** $f(z) = \max(0, z)$. The industry standard for hidden layers because it's fast and prevents the model from "dying" during training.

### How it Trains: Backpropagation
1.  **Forward Pass:** Data flows through the layers to get a prediction.
2.  **Calculate Error:** Compare prediction to the actual label.
3.  **Backward Pass:** Use the **Chain Rule** from calculus to distribute the error back through the weights, telling each neuron how much it needs to change to improve the overall result.

---
**Study Tip:** Remember that ML is an iterative process. You Build -> Evaluate -> Regularize -> Repeat until your validation error is minimized!