# Machine Learning 1

## Table of Contents
- [Lecture 2: Linear Regression](#lecture-2-linear-regression)
- [Lecture 3: Logistic Regression](#lecture-3-logistic-regression)
- [Lecture 4: Regularization](#lecture-4-regularization)
- [Lecture 6: Artificial Neural Network](#lecture-6-artificial-neural-network)
- [Lecture 4: Model Evaluation](#lecture-4-model-evaluation)
- [Lab Practice 1: Linear Regression Implementation](#lab-practice-1-linear-regression-implementation)

---

## Lecture 2: Linear Regression
**Lecturer:** Dr. Le Huu Ton  
**Date:** Hanoi, 09/2016

---

### 1. Review of Machine Learning
In the standard machine learning workflow, the process is structured as follows:
- **Training Data:** A set of examples used to train the model.
- **System to train $h$ (hypothesis):** The learning algorithm that processes training data to find the best hypothesis function.
- **Input ($X$):** The features or predictors.
- **Output ($Y$):** The target variable or response.
- **Hypothesis Function ($h$):** For each input $x$, the system outputs a prediction $y = h(x)$.

---

### 2. Introduction to Linear Regression
Linear Regression assumes that the output $y$ is a linear function of the input $x$.

#### 2.1. Training Data Example
Consider the housing prices in Hanoi:

| Size ($m^2$) | Price (billion VND) |
| :--- | :--- |
| 30 | 2.5 |
| 43 | 3.4 |
| 25 | 1.8 |
| 51 | 4.5 |
| 40 | 3.2 |
| 20 | 1.6 |

**Table 1: Training data of housing price in Hanoi**

#### 2.2. Notation
- $(x, y)$: Denotes a single training example.
- $(x^{(i)}, y^{(i)})$: Denotes the $i^{th}$ training example in the dataset.
- $x$: Features (input).
- $y$: Response (output).

#### 2.3. Hypothesis Function
The hypothesis for simple linear regression (one feature) is defined as:
$$h(x) = a \cdot x + b$$
Where:
- $a, b$: Coefficients (parameters) of the model that need to be learned.
- $x$: Input feature.
- $y$: Predicted output.

---

### 3. Objective and Cost Function
The objective of linear regression is to learn the coefficients $a$ and $b$ such that the error (cost function) for the training data is minimized. This is an optimization problem.

#### 3.1. Error for a Single Training Data Point
The error $e^{(i)}$ for the $i^{th}$ training example is defined as:
$$e^{(i)} = \frac{1}{2}(h(x^{(i)}) - y^{(i)})^2 = \frac{1}{2}(ax^{(i)} + b - y^{(i)})^2$$

#### 3.2. Total Cost Function ($E$)
The cost function $E$ (often denoted as $J(a, b)$) is the average of the errors across all $m$ training examples:
$$E = \frac{1}{m}(e^{(1)} + e^{(2)} + \dots + e^{(m)}) = \frac{1}{m} \sum_{i=1}^{m} e^{(i)}$$
Substituting the individual errors:
$$E = \frac{1}{2m} \sum_{i=1}^{m} (h(x^{(i)}) - y^{(i)})^2$$
$$E = \frac{1}{2m} \sum_{i=1}^{m} (ax^{(i)} + b - y^{(i)})^2$$

---

### 4. Gradient Descent Algorithm
Gradient Descent is an iterative optimization algorithm used to find the minimum of a function.

#### 4.1. The Idea
1. Start with random values for $a$ and $b$.
2. In many steps, modify $a$ and $b$ simultaneously such that the cost function $E$ is reduced.

#### 4.2. Update Rules
The parameters are updated using the following formulas:
$$a := a - \alpha \frac{\partial}{\partial a} E(a, b)$$
$$b := b - \alpha \frac{\partial}{\partial b} E(a, b)$$
Where:
- $\alpha$: Learning rate (a small positive number).
- $\frac{\partial}{\partial a} E(a, b)$: Partial derivative of the cost function with respect to $a$.
- $\frac{\partial}{\partial b} E(a, b)$: Partial derivative of the cost function with respect to $b$.

#### 4.3. Calculating Derivatives
Given the cost function $E = \frac{1}{2m} \sum_{i=1}^{m} (ax^{(i)} + b - y^{(i)})^2$, and the calculus rule $\frac{\partial}{\partial x}(f(x)^2) = 2f(x) \cdot \frac{\partial}{\partial x}f(x)$:

**Partial derivative with respect to $a$:**
$$\frac{\partial}{\partial a} E(a, b) = \frac{1}{m} \sum_{i=1}^{m} (ax^{(i)} + b - y^{(i)}) \cdot x^{(i)}$$

**Partial derivative with respect to $b$:**
$$\frac{\partial}{\partial b} E(a, b) = \frac{1}{m} \sum_{i=1}^{m} (ax^{(i)} + b - y^{(i)})$$

#### 4.4. Summary of Gradient Descent Steps
1. Calculate the cost function.
2. Select random initial values for coefficients $a, b$.
3. While (not converged) do:
   - Update $a$: $a := a - \alpha \frac{1}{m} \sum_{i=1}^{m} (h(x^{(i)}) - y^{(i)})x^{(i)}$
   - Update $b$: $b := b - \alpha \frac{1}{m} \sum_{i=1}^{m} (h(x^{(i)}) - y^{(i)})$

---

### 5. Gradient Descent Variations
- **Batch Gradient Descent:** Computes the gradient using the entire dataset in every step.
- **Stochastic Gradient Descent (SGD):**
  - Randomly reorder the training data.
  - Update $a, b$ using only one training example at a time.
  - Step 1: Use $(x^{(1)}, y^{(1)})$ to update $a, b$.
  - Step 2: Use $(x^{(2)}, y^{(2)})$ to update $a, b$, and so on.
- **Mini-Batch Gradient Descent:** Computes the gradient for a small subset of $t$ examples at a time ($1 < t < m$).
  - Example: For 1000 data points, update using data 1-10, then 11-20, etc.

---

### 6. Convergence and Learning Rate ($\alpha$)
- If $\alpha$ is too large, the cost function may increase or fail to converge (oscillate).
- Gradient Descent works if the cost function decreases at each step.
- **Conditions for Convergence:**
  - Cost function value is smaller than a predefined threshold.
  - After a sufficiently large number of steps.
  - The decrease in the cost function between steps is less than a predefined threshold.

---

### 7. Exercise: Manual Gradient Descent Step
**Problem Statement:**
Given the data in Table 1, starting at $a=0$ and $b=0$ with learning rate $\alpha=0.01$:
1. What is the initial cost function?
2. Calculate the values of $a$ and $b$ after the first iteration.
3. Confirm if the cost function is reduced.

**Solution:**
**1. Initial Cost Function $E$ at $a=0, b=0$:**
$m=6$. Data points $(x,y)$: $(30, 2.5), (43, 3.4), (25, 1.8), (51, 4.5), (40, 3.2), (20, 1.6)$
$h(x) = 0x + 0 = 0$
$E = \frac{1}{12} [2.5^2 + 3.4^2 + 1.8^2 + 4.5^2 + 3.2^2 + 1.6^2] = \frac{54.1}{12} \approx 4.508$

**2. First Iteration Updates:**
$\frac{\partial E}{\partial a} = \frac{1}{6} \sum_{i=1}^6 (0 - y^{(i)})x^{(i)} = \frac{1}{6} [-75 - 146.2 - 45 - 229.5 - 128 - 32] = \frac{-655.7}{6} \approx -109.283$
$\frac{\partial E}{\partial b} = \frac{1}{6} \sum_{i=1}^6 (0 - y^{(i)}) = \frac{1}{6} [-2.5 - 3.4 - 1.8 - 4.5 - 3.2 - 1.6] = \frac{-17}{6} \approx -2.833$
New $a = 0 - (0.01 \cdot -109.283) = 1.09283$
New $b = 0 - (0.01 \cdot -2.833) = 0.02833$

**3. Confirm reduction:**
New $E$ with $a=1.09283, b=0.02833$ is $\approx 679.7$. The cost increased significantly, so it did not reduce. This indicates the learning rate $\alpha=0.01$ is too high for this scale of features.

---

### 8. Multi-Feature Representation
When there are multiple input features, we represent them as vectors and matrices.

#### 8.1. Example Data with More Inputs
| Size ($m^2$) | No. of floors | No. of rooms | Price (billion VND) |
| :--- | :--- | :--- | :--- |
| 30 | 3 | 6 | 2.5 |
| 43 | 4 | 8 | 3.4 |
| 25 | 2 | 3 | 1.8 |
| 51 | 4 | 9 | 4.5 |
| 40 | 3 | 5 | 3.2 |
| 20 | 1 | 2 | 1.6 |

**Notation:**
- $x^{(i)}$: The input vector of the $i^{th}$ training example.
- $x_j^{(i)}$: The value of the $j^{th}$ feature for the $i^{th}$ training example.

#### 8.2. Matrix Representation
Hypothesis: $h(x) = \theta_0 + \theta_1 x_1 + \theta_2 x_2 + \dots + \theta_n x_n$

Let $x_0 = 1$ (intercept term).
Input vector $x = \begin{bmatrix} 1 \\ x_1 \\ \vdots \\ x_n \end{bmatrix}$, Parameter vector $\theta = \begin{bmatrix} \theta_0 \\ \theta_1 \\ \vdots \\ \theta_n \end{bmatrix}$.
Hypothesis: $h(x) = \theta^T x$

#### 8.3. Cost Function for Multiple Features
$$E(\theta) = \frac{1}{2m} \sum_{i=1}^{m} (h_\theta(x^{(i)}) - y^{(i)})^2 = \frac{1}{2m} \sum_{i=1}^{m} (\theta^T x^{(i)} - y^{(i)})^2$$

#### 8.4. Gradient Descent Update
$$\theta_j := \theta_j - \alpha \frac{\partial}{\partial \theta_j} E(\theta)$$
$$\theta_j := \theta_j - \alpha \frac{1}{m} \sum_{i=1}^{m} (\theta^T x^{(i)} - y^{(i)})x_j^{(i)}$$

---

### 9. Normal Equations
The Normal Equation is an analytical method to find the optimal $\theta$ that minimizes the cost function without iteration.

#### 9.1. Objective
Solve $\frac{\partial}{\partial \theta} E(\theta) = 0$.
Specifically, $\forall j \in \{0, 1, \dots, n\}, \frac{\partial}{\partial \theta_j} E(\theta) = 0$.

#### 9.2. Solution
Given $m$ examples with $n$ inputs, construct:
- Matrix $X$ ($m \times (n+1)$): Each row is an input vector $(x^{(i)})^T$.
- Vector $Y$ ($m \times 1$): Contains all output values $y^{(i)}$.

$$X = \begin{bmatrix} (x^{(1)})^T \\ (x^{(2)})^T \\ \vdots \\ (x^{(m)})^T \end{bmatrix}, Y = \begin{bmatrix} y^{(1)} \\ y^{(2)} \\ \vdots \\ y^{(m)} \end{bmatrix}$$
The closed-form solution is:
$$\theta = (X^T X)^{-1} X^T Y$$

#### 9.3. Exercise: Normal Equation Calculation
**Data:**
$x = [3, 2, 1]^T$, $y = [0, 1, 2]^T$
Including $x_0 = 1$:
$X = \begin{bmatrix} 1 & 3 \\ 1 & 2 \\ 1 & 1 \end{bmatrix}, Y = \begin{bmatrix} 0 \\ 1 \\ 2 \end{bmatrix}$

**Solution:**
1. $X^T X = \begin{bmatrix} 1 & 1 & 1 \\ 3 & 2 & 1 \end{bmatrix} \begin{bmatrix} 1 & 3 \\ 1 & 2 \\ 1 & 1 \end{bmatrix} = \begin{bmatrix} 3 & 6 \\ 6 & 14 \end{bmatrix}$.
2. $\text{det}(X^T X) = 3(14) - 6(6) = 6$.
3. $(X^T X)^{-1} = \frac{1}{6} \begin{bmatrix} 14 & -6 \\ -6 & 3 \end{bmatrix} = \begin{bmatrix} 7/3 & -1 \\ -1 & 1/2 \end{bmatrix}$.
4. $X^T Y = \begin{bmatrix} 1 & 1 & 1 \\ 3 & 2 & 1 \end{bmatrix} \begin{bmatrix} 0 \\ 1 \\ 2 \end{bmatrix} = \begin{bmatrix} 3 \\ 4 \end{bmatrix}$.
5. $\theta = \begin{bmatrix} 7/3 & -1 \\ -1 & 1/2 \end{bmatrix} \begin{bmatrix} 3 \\ 4 \end{bmatrix} = \begin{bmatrix} 3 \\ -1 \end{bmatrix}$.
The hypothesis is $h(x) = 3 - x$.

---

### 10. Polynomial Regression
Polynomial regression models the relationship between $x$ and $y$ as an $n^{th}$ degree polynomial.
$h(x) = \theta_0 + \theta_1 x + \theta_2 x^2 + \dots + \theta_n x^n$

This can be mapped back to linear regression by defining new features:
$x_1 = x, x_2 = x^2, \dots, x_n = x^n$
Then $h(x) = \theta_0 + \theta_1 x_1 + \theta_2 x_2 + \dots + \theta_n x_n$.

---

### 11. Feature Rescale (Feature Scaling)
**Objective:** Scale all features to the same range to speed up gradient descent convergence.
**Popular scales:** $[0, 1]$ or $[-0.5, 0.5]$.

**Methods:**
- **Simple Scaling:** $x = \frac{x}{\max(x)}$
- **Mean Normalization:** $x = \frac{x - \text{mean}(x)}{\max(x)}$ (or more commonly $x = \frac{x - \mu}{\sigma}$)

---
**References:**
[Stanford OpenCourseWare - Machine Learning](http://openclassroom.stanford.edu/MainFolder/VideoPage.php?course=MachineLearning&video=02.4-LinearRegressionI-GradientDescent&speed=100)

---

## Lecture 3: Logistic Regression
**Lecturer:** Dr. Le Huu Ton  
**Date:** Hanoi, 2020

---

### 1. Classification
Classification is a type of supervised learning where the output variable $y$ can only take discrete values (categories).

#### 1.1. Binary Classification Example
Predicting house location based on price:
- $y = 0$: Thanh Xuan district (Negative class)
- $y = 1$: Hoan Kiem district (Positive class)
- $y \in \{0, 1\}$

| Price (billion VND) | Location | $y$ |
| :--- | :--- | :--- |
| 2.5 | Thanh Xuan | 0 |
| 3.5 | Thanh Xuan | 0 |
| 5.6 | Hoan Kiem | 1 |
| 2.2 | Thanh Xuan | 0 |
| 6.9 | Hoan Kiem | 1 |
| 9.6 | Hoan Kiem | 1 |

#### 1.2. Why Linear Regression fails for Classification?
Linear regression ($h(x) = \theta^T x$) is not suitable for classification because:
- Its output can be $> 1$ or $< 0$.
- It is sensitive to outliers, which can significantly shift the decision boundary even if the classification of most points remains clear.

---

### 2. Hypothesis Representation
We need a hypothesis function such that $0 \le h(x) \le 1$.

#### 2.1. Logistic Function (Sigmoid Function)
The hypothesis is defined as:
$$h_\theta(x) = g(\theta^T x)$$
Where $g(z)$ is the **Sigmoid function** or **Logistic function**:
$$g(z) = \frac{1}{1 + e^{-z}}$$
Substituting $z = \theta^T x$:
$$h_\theta(x) = \frac{1}{1 + e^{-\theta^T x}}$$

#### 2.2. Interpretation
The output $h_\theta(x)$ is interpreted as the **probability** that $y=1$ given input $x$, parameterized by $\theta$:
$$h_\theta(x) = P(y=1 | x; \theta)$$
**Example:** If $h_\theta(x) = 0.65$, there is a 65% chance the house is located in Hoan Kiem district.

---

### 3. Decision Boundary
The decision boundary is the line (or surface) that separates the area where we predict $y=1$ from the area where we predict $y=0$.

- Predict $y=1$ if $h_\theta(x) \ge 0.5$
  - Since $g(z) \ge 0.5$ when $z \ge 0$, this corresponds to $\theta^T x \ge 0$.
- Predict $y=0$ if $h_\theta(x) < 0.5$
  - This corresponds to $\theta^T x < 0$.

#### 3.1. Linear Decision Boundary Example
If $h_\theta(x) = g(\theta_0 + \theta_1 x_1 + \theta_2 x_2)$ and $\theta = [-3, 1, 1]^T$:
Decision boundary is $-3 + x_1 + x_2 = 0 \Rightarrow x_1 + x_2 = 3$.
Predict $y=1$ if $x_1 + x_2 \ge 3$.

#### 3.2. Non-linear Decision Boundary Example
By using polynomial features, we can create complex boundaries:
$h_\theta(x) = g(\theta_0 + \theta_1 x_1 + \theta_2 x_2 + \theta_3 x_1^2 + \theta_4 x_2^2)$
If $\theta = [-1, 0, 0, 1, 1]^T$, the decision boundary is $-1 + x_1^2 + x_2^2 = 0 \Rightarrow x_1^2 + x_2^2 = 1$ (a circle).

---

### 4. Cost Function
The squared error cost function used in linear regression is **non-convex** for logistic regression, meaning it has many local minima. We need a **convex** cost function to ensure gradient descent finds the global minimum.

#### 4.1. Logistic Regression Cost Function
For a single training example $(x, y)$:
$$\text{Cost}(h_\theta(x), y) = \begin{cases} -\log(h_\theta(x)) & \text{if } y=1 \\ -\log(1 - h_\theta(x)) & \text{if } y=0 \end{cases}$$

This can be written in a single line:
$$\text{Cost}(h_\theta(x), y) = -y \log(h_\theta(x)) - (1 - y) \log(1 - h_\theta(x))$$

#### 4.2. Total Cost Function ($E(\theta)$)
The overall cost function is the average cost over $m$ training examples:
$$E(\theta) = -\frac{1}{m} \sum_{i=1}^{m} [y^{(i)} \log h_\theta(x^{(i)}) + (1 - y^{(i)}) \log(1 - h_\theta(x^{(i)}))]$$

---

### 5. Gradient Descent for Logistic Regression
To minimize $E(\theta)$, we use the gradient descent update rule:
$$\theta_j := \theta_j - \alpha \frac{\partial}{\partial \theta_j} E(\theta)$$

#### 5.1. Derivation of the Gradient
Using the properties of the sigmoid function ($g'(z) = g(z)(1-g(z))$) and the derivative of $\log(z)$ ($\frac{1}{z}$):
$$\frac{\partial}{\partial \theta_j} E(\theta) = \frac{1}{m} \sum_{i=1}^{m} (h_\theta(x^{(i)}) - y^{(i)})x_j^{(i)}$$

*Note: Surprisingly, this update rule looks identical to linear regression, but the definition of $h_\theta(x)$ is different (sigmoid vs linear).*

#### 5.2. Exercise: Manual Step
Starting with $\theta_0 = 0, \theta_1 = 0, \alpha = 0.001$:
Calculate the values after the first iteration using the data in Section 1.1.

**Solution:**
Data: $x = [2.5, 3.5, 5.6, 2.2, 6.9, 9.6]$, $y = [0, 0, 1, 0, 1, 1]$. $m=6$.
At $\theta=[0,0]^T$, $h(x) = g(0) = 0.5$ for all $x$.
$\frac{\partial E}{\partial \theta_0} = \frac{1}{6} \sum (0.5 - y^{(i)}) = \frac{1}{6} [0.5+0.5-0.5+0.5-0.5-0.5] = 0$.
$\frac{\partial E}{\partial \theta_1} = \frac{1}{6} \sum (0.5 - y^{(i)})x^{(i)} = \frac{1}{6} [1.25+1.75-2.8+1.1-3.45-4.8] = \frac{-6.95}{6} \approx -1.1583$.
New $\theta_0 = 0 - 0.001(0) = 0$.
New $\theta_1 = 0 - 0.001(-1.1583) = 0.0011583$.

---

### 6. Newton's Method
Newton's method is an alternative optimization algorithm that typically converges in fewer iterations than gradient descent.

#### 6.1. The Idea
To find where $f(\theta) = 0$ (in our case, where the derivative of the cost function is zero):
$$\theta^{(t+1)} = \theta^{(t)} - \frac{f(\theta^{(t)})}{f'(\theta^{(t)})}$$

Applying this to minimize the cost function $E(\theta)$, we set $f(\theta) = E'(\theta)$:
$$\theta^{(t+1)} = \theta^{(t)} - \frac{E'(\theta^{(t)})}{E''(\theta^{(t)})}$$

#### 6.2. Multidimensional Newton's Method
$$\theta := \theta - H^{-1} \nabla_\theta E$$
Where:
- $\nabla_\theta E$: Gradient vector (first derivatives).
- $H$: **Hessian Matrix** (second derivatives).

**Hessian Matrix Definition:**
$H_{ij} = \frac{\partial^2 E}{\partial \theta_i \partial \theta_j}$
For Logistic Regression:
$$\nabla_\theta E = \frac{1}{m} \sum_{i=1}^{m} (h_\theta(x^{(i)}) - y^{(i)})x^{(i)}$$
$$H = \frac{1}{m} \sum_{i=1}^{m} [h_\theta(x^{(i)})(1 - h_\theta(x^{(i)})) x^{(i)} (x^{(i)})^T]$$

#### 6.3. Comparison: Newton's Method vs Gradient Descent

| Feature | Gradient Descent | Newton's Method |
| :--- | :--- | :--- |
| **Implementation** | Simpler | More complex |
| **Hyperparameters** | Need to choose $\alpha$ | No $\alpha$ needed |
| **Convergence** | Slower (more iterations) | Faster (fewer iterations) |
| **Computation Cost** | Low per iteration ($O(n)$) | High per iteration ($O(n^3)$ for $H^{-1}$) |
| **Scalability** | Good for large $n$ ($> 1000$) | Best for small $n$ |

---

### 7. Exercise: Hessian Matrix
**Problem:** Compute the Hessian matrix and derivative vector at $\theta_0 = 0, \theta_1 = 0$ for the following data:
Prices: 2.5, 3, 6, 2, 7, 10.
Locations ($y$): 0, 0, 1, 0, 1, 1.

**Solution:**
Data: $x = [2.5, 3, 6, 2, 7, 10]$, $y = [0, 0, 1, 0, 1, 1]$. $m=6$.
At $\theta=0$, $h=0.5$.
1. Gradient $\nabla E$:
$\frac{\partial E}{\partial \theta_0} = \frac{1}{6} \sum (0.5 - y^{(i)}) = 0$.
$\frac{\partial E}{\partial \theta_1} = \frac{1}{6} \sum (0.5 - y^{(i)})x^{(i)} = \frac{1}{6} [1.25+1.5-3+1-3.5-5] = \frac{-7.75}{6} \approx -1.2917$.
$\nabla E = \begin{bmatrix} 0 \\ -1.2917 \end{bmatrix}$.
2. Hessian $H$:
$H_{jk} = \frac{1}{6} \sum 0.5(1-0.5) x_j^{(i)} x_k^{(i)} = \frac{0.25}{6} \sum x^{(i)} (x^{(i)})^T$.
$\sum 1 = 6$.
$\sum x = 2.5+3+6+2+7+10 = 30.5$.
$\sum x^2 = 6.25+9+36+4+49+100 = 204.25$.
$H = \frac{0.25}{6} \begin{bmatrix} 6 & 30.5 \\ 30.5 & 204.25 \end{bmatrix} = \begin{bmatrix} 0.25 & 1.2708 \\ 1.2708 & 8.5104 \end{bmatrix}$.

---
**References:**
- [Stanford Machine Learning - Andrew Ng](http://openclassroom.stanford.edu/MainFolder/CoursePage.php?course=MachineLearning)
- [Andrew Ng Slides on Generalized Linear Models](https://www.google.com.vn/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&sqi=2&ved=0ahUKEwjNt4fdvMDPAhXIn5QKHZO1BSgQFggfMAE&url=https%3A%2F%2Fdatajobs.com%2Fdata-science-repo%2FGeneralized-Linear-Models-%5BAndrew-Ng%5D.pdf)

---

## Lecture 4: Regularization
**Lecturer:** Dr. Le Huu Ton  
**Date:** Hanoi, 2018

---

### 1. The Overfitting Problem
Overfitting and underfitting are two common issues when training machine learning models.

#### 1.1. Definitions
- **Underfitting:** Refers to a model that can neither model the training data nor generalize to new data. It has poor performance on both. This usually happens when the model is too simple (high bias).
- **Overfitting:** Happens when a model learns the detail and noise in the training data to the extent that it negatively impacts the performance on new data. The model performs extremely well on training data but fails to generalize (high variance).

#### 1.2. Visual Examples (Linear Regression)
- **Underfit:** $h_\theta(x) = \theta_0 + \theta_1 x$ (A straight line trying to fit a curved pattern).
- **OK (Just Right):** $h_\theta(x) = \theta_0 + \theta_1 x + \theta_2 x^2$.
- **Overfit:** $h_\theta(x) = \theta_0 + \theta_1 x + \theta_2 x^2 + \theta_3 x^3 + \theta_4 x^4 + \dots$ (A wavy line that passes through every training point).

#### 1.3. Visual Examples (Logistic Regression)
- **Underfit:** $h_\theta(x) = g(\theta_0 + \theta_1 x_1 + \theta_2 x_2)$.
- **OK:** $h_\theta(x) = g(\theta_0 + \theta_1 x_1 + \theta_2 x_2 + \theta_3 x_1^2 + \theta_4 x_2^2 + \theta_5 x_1 x_2)$.
- **Overfit:** Very complex boundary with many polynomial terms.

---

### 2. Regularization
Regularization is a technique used to solve the overfitting problem by reducing the magnitude (values) of the coefficients $\theta_j$.

- Small values for coefficients $\theta_0, \theta_1, \dots, \theta_n$ lead to a "simpler" hypothesis $h(x)$.
- Simpler models are less prone to overfitting.

#### 2.1. Modified Cost Function
We add a **regularization component** to the cost function to penalize large parameter values:
$$E(\theta) = \frac{1}{2m} \left[ \sum_{i=1}^{m} (h_\theta(x^{(i)}) - y^{(i)})^2 + \lambda \sum_{j=1}^{n} \theta_j^2 \right]$$
Where:
- $\lambda$: Regularization parameter (controls the trade-off between fitting the data and keeping parameters small).
- $n$: Number of features.
- Note: Usually, we do not regularize $\theta_0$ (the intercept).

#### 2.2. The effect of $\lambda$
- If $\lambda$ is extremely large, the algorithm results in **underfitting** because it forces all $\theta_j \approx 0$ (except $\theta_0$).
- If $\lambda$ is zero, the model may **overfit**.

---

### 3. Regularization with Linear Regression

#### 3.1. Gradient Descent Updates
Repeat until converged:
1. For $j=0$ (no regularization):
   $$\theta_0 := \theta_0 - \alpha \frac{1}{m} \sum_{i=1}^{m} (h_\theta(x^{(i)}) - y^{(i)})x_0^{(i)}$$
2. For $j=1, 2, \dots, n$:
   $$\theta_j := \theta_j - \alpha \left[ \frac{1}{m} \sum_{i=1}^{m} (h_\theta(x^{(i)}) - y^{(i)})x_j^{(i)} + \frac{\lambda}{m} \theta_j \right]$$

This can be rewritten as:
$$\theta_j := \theta_j (1 - \alpha \frac{\lambda}{m}) - \alpha \frac{1}{m} \sum_{i=1}^{m} (h_\theta(x^{(i)}) - y^{(i)})x_j^{(i)}$$
Since $(1 - \alpha \frac{\lambda}{m})$ is slightly less than 1, this "shrinks" $\theta_j$ in each step.

#### 3.2. Normal Equation with Regularization
The analytical solution becomes:
$$\theta = (X^T X + \lambda L)^{-1} X^T Y$$
Where $L$ is an $(n+1) \times (n+1)$ matrix:
$$L = \begin{bmatrix} 0 & 0 & \dots & 0 \\ 0 & 1 & \dots & 0 \\ \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \dots & 1 \end{bmatrix}$$
(Identity matrix with the top-left element as 0).

---

### 4. Regularization with Logistic Regression

#### 4.1. Cost Function
$$E(\theta) = -\frac{1}{m} \sum_{i=1}^{m} [y^{(i)} \log h_\theta(x^{(i)}) + (1 - y^{(i)}) \log(1 - h_\theta(x^{(i)}))] + \frac{\lambda}{2m} \sum_{j=1}^{n} \theta_j^2$$

#### 4.2. Gradient Descent
The update rules are the same as in Linear Regression (Section 3.1), but with $h_\theta(x) = g(\theta^T x)$.

#### 4.3. Newton's Method with Regularization
Update rule: $\theta := \theta - H^{-1} \nabla_\theta E$

**Modified Gradient Vector ($\nabla_\theta E$):**
- $\frac{\partial E}{\partial \theta_0} = \frac{1}{m} \sum (h_\theta(x^{(i)}) - y^{(i)})x_0^{(i)}$
- $\frac{\partial E}{\partial \theta_j} = \frac{1}{m} \sum (h_\theta(x^{(i)}) - y^{(i)})x_j^{(i)} + \frac{\lambda}{m} \theta_j$ (for $j \ge 1$)

**Modified Hessian Matrix ($H$):**
$$H = \frac{1}{m} \sum_{i=1}^{m} [h_\theta(x^{(i)})(1 - h_\theta(x^{(i)})) x^{(i)} (x^{(i)})^T] + \frac{\lambda}{m} L$$
Where $L$ is the same matrix as in Section 3.2.

---

### 5. Exercises

#### 5.1. Regularization Effect
**Question:** What if $\lambda$ is set to an extremely large number?
**Answer:** The algorithm results in underfitting. Small parameters $\theta_j$ ($j \ge 1$) will be penalized heavily, forcing them toward zero and making the model too simple.

#### 5.2. Iteration Calculation
**Problem:** Given data:
- Size: 30, 40, 20, 50, 40, 20
- Floors: 3, 4, 2, 4, 3, 1
- Prices: 2, 3, 2, 5, 3, 2
At one iteration: $\theta_0=1, \theta_1=2, \theta_2=1, \alpha=6, \lambda=10, m=6$.
Calculate the values of $\theta$ after this iteration using the regularized update rule.

**Solution:**
1. Predictions $h(x) = 1 + 2x_1 + x_2$:
$h = [64, 85, 43, 105, 84, 42]$.
2. Errors $h-y$:
$h-y = [62, 82, 41, 100, 81, 40]$.
3. Sum of errors: $\sum (h-y) = 406$.
4. $\theta_0$ update: $\theta_0 := 1 - 6(406/6) = 1 - 406 = -405$.
5. $\theta_1$ update: $\theta_1 := 2(1 - 60/6) - (6/6) \sum (h-y)x_1 = 2(-9) - 15000 = -18 - 15000 = -15018$.
($\sum (h-y)x_1 = 62(30)+82(40)+41(20)+100(50)+81(40)+40(20) = 1860+3280+820+5000+3240+800 = 15000$)
6. $\theta_2$ update: $\theta_2 := 1(1 - 60/6) - (6/6) \sum (h-y)x_2 = -9 - 1279 = -1288$.
($\sum (h-y)x_2 = 62(3)+82(4)+41(2)+100(4)+81(3)+40(1) = 186+328+82+400+243+40 = 1279$)

#### 5.3. Newton's Method Exercise
**Problem:** Starting with $\theta_0 = 0, \theta_1 = 0, \alpha = 0.01, \lambda = 10$.
1. Calculate the value of coefficients after the first iteration using gradient descent.
2. Calculate the Hessian matrix and derivative vector for Newton's method using the data:
   Prices: 2.5, 3.5, 5.6, 2.2, 6.9, 9.6
   $y$: 0, 0, 1, 0, 1, 1

**Solution:**
1. Gradient Descent:
$\frac{\partial E}{\partial \theta_1} = -1.1583 + (10/6)(0) = -1.1583$.
$\theta_1 := 0 - 0.01(-1.1583) = 0.011583$. $\theta_0 = 0$.
2. Newton's Method:
$\nabla E = \begin{bmatrix} 0 \\ -1.1583 \end{bmatrix}$.
$H = \frac{0.25}{6} \begin{bmatrix} 6 & 30.3 \\ 30.3 & 201.27 \end{bmatrix} + \frac{10}{6} \begin{bmatrix} 0 & 0 \\ 0 & 1 \end{bmatrix} = \begin{bmatrix} 0.25 & 1.2625 \\ 1.2625 & 10.053 \end{bmatrix}$.

---
**References:**
- [Stanford Machine Learning - Andrew Ng](http://openclassroom.stanford.edu/MainFolder/CoursePage.php?course=MachineLearning)
- [Andrew Ng Slides on Generalized Linear Models](https://www.google.com.vn/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&sqi=2&ved=0ahUKEwjNt4fdvMDPAhXIn5QKHZO1BSgQFggfMAE&url=https%3A%2F%2Fdatajobs.com%2Fdata-science-repo%2FGeneralized-Linear-Models-%5BAndrew-Ng%5D.pdf)

---

## Lecture 6: Artificial Neural Network
**Lecturer:** Dr. Le Huu Ton  
**Date:** Hanoi, 2017

---

### 1. Biological Inspiration
Artificial Neural Networks (ANNs) are loosely inspired by the structure of biological neurons in the brain.
- **Dendrites:** Receives input signals.
- **Cell Body (Nucleus):** Processes signals.
- **Axon:** Transmits the output signal to other neurons via **Axon terminals**.

---

### 2. The Perceptron
A Perceptron mimics the operation of a biological neuron.

#### 2.1. Mathematical Model
- **Inputs:** $x_1, x_2, \dots, x_m$ (and a bias term 1).
- **Weights:** $w_0, w_1, \dots, w_m$.
- **Net Input Function:**
  $$net = 1 \cdot w_0 + x_1 w_1 + x_2 w_2 + \dots + x_m w_m = w^T x$$
- **Activation Function ($f$):** Applied to the net input to produce the output.
  $$y = f(net)$$

#### 2.2. Popular Activation Functions
| Function | Formula | Range |
| :--- | :--- | :--- |
| **Identity** | $f(x) = x$ | $(-\infty, \infty)$ |
| **Binary Step** | $f(x) = \begin{cases} 0 & x < 0 \\ 1 & x \ge 0 \end{cases}$ | $\{0, 1\}$ |
| **Logistic (Sigmoid)** | $f(x) = \frac{1}{1 + e^{-x}}$ | $(0, 1)$ |
| **TanH** | $f(x) = \tanh(x) = \frac{2}{1 + e^{-2x}} - 1$ | $(-1, 1)$ |
| **ReLU (Rectified Linear Unit)** | $f(x) = \max(0, x)$ | $[0, \infty)$ |
| **ArcTan** | $f(x) = \tan^{-1}(x)$ | $(-\pi/2, \pi/2)$ |
| **Softsign** | $f(x) = \frac{x}{1 + |x|}$ | $(-1, 1)$ |

---

### 3. Motivation for Neural Networks
When the number of features is large, using high-order polynomial features in Logistic Regression becomes computationally expensive.
- **Example:** 100 original features $\Rightarrow$ ~5,000 second-order features $\Rightarrow$ ~170,000 third-order features.
- Neural Networks provide a better way to learn complex non-linear relationships.

---

### 4. Neural Network Architecture
Neurons are organized into layers:
- **Layer 1 (Input Layer):** Receives the initial data.
- **Hidden Layers:** Intermediate layers where features are transformed.
- **Layer $L$ (Output Layer):** Produces the final prediction $h_\theta(x)$.

**Notation:**
- $a_i^{(j)}$: "Activation" of unit $i$ in layer $j$.
- $W^{(j)}$: Matrix of weights controlling function mapping from layer $j$ to layer $j+1$.

---

### 5. Forward Propagation
Information flows from the input layer through the hidden layers to the output layer.

**General Equations (Matrix Form):**
- $a^{(1)} = x$ (including bias $x_0 = 1$).
- $z^{(2)} = W^{(1)} a^{(1)}$
- $a^{(2)} = g(z^{(2)})$
- $z^{(3)} = W^{(2)} a^{(2)}$
- $a^{(3)} = g(z^{(3)}) = h(x)$

**Example for 3-layer network (Layer 2 is hidden):**
$$a_1^{(2)} = g(W_{10}^{(1)}x_0 + W_{11}^{(1)}x_1 + W_{12}^{(1)}x_2 + W_{13}^{(1)}x_3)$$
$$a_2^{(2)} = g(W_{20}^{(1)}x_0 + W_{21}^{(1)}x_1 + W_{22}^{(1)}x_2 + W_{23}^{(1)}x_3)$$
$$h(x) = a^{(3)} = g(W_{10}^{(2)}a_0^{(2)} + W_{11}^{(2)}a_1^{(2)} + W_{12}^{(2)}a_2^{(2)} + W_{13}^{(2)}a_3^{(2)})$$

---

### 6. Training Neural Networks

#### 6.1. Cost Function
For regression-like output (MSE):
$$E(W) = \frac{1}{2m} \sum_{i=1}^{m} (y^{(i)} - h(x^{(i)}))^2$$

#### 6.2. Gradient Descent
Update each weight $w$ to minimize $E$:
$$w := w - \alpha \frac{\partial E}{\partial w}$$

---

### 7. Backpropagation Algorithm
Backpropagation is used to calculate the gradients $\frac{\partial E}{\partial w}$ efficiently layer by layer, starting from the last layer.

#### 7.1. Chain Rule Derivation
For a weight $w$ in the network:
$$\frac{\partial E}{\partial w} = \frac{\partial E}{\partial a} \cdot \frac{\partial a}{\partial net} \cdot \frac{\partial net}{\partial w}$$

#### 7.2. Step-by-Step Backprop (Example Updates)
To update an output weight $w_5$ (connected to output $o_1$):
$$\frac{\partial E_{total}}{\partial w_5} = \frac{\partial E_{total}}{\partial out_{o1}} \cdot \frac{\partial out_{o1}}{\partial net_{o1}} \cdot \frac{\partial net_{o1}}{\partial w_5}$$
Where:
- $E_{total} = E_{o1} + E_{o2}$
- $E_{o1} = \frac{1}{2}(\text{target}_{o1} - out_{o1})^2$

To update a hidden weight $w_1$ (connected to hidden unit $h_1$):
$$\frac{\partial E_{total}}{\partial w_1} = \frac{\partial E_{total}}{\partial out_{h1}} \cdot \frac{\partial out_{h1}}{\partial net_{h1}} \cdot \frac{\partial net_{h1}}{\partial w_1}$$
Since $h_1$ affects both outputs $o_1$ and $o_2$:
$$\frac{\partial E_{total}}{\partial out_{h1}} = \frac{\partial E_{o1}}{\partial out_{h1}} + \frac{\partial E_{o2}}{\partial out_{h1}}$$

---

### 8. Exercises

#### 8.1. Manual Forward Pass
**Problem:** Calculate the output of a network with $x_1=1, x_2=0$ and weights:
$w_{13}=2, w_{23}=-3, w_{35}=2$
$w_{14}=1, w_{24}=4, w_{45}=-1$
Using binary step activation: $f(v) = 1$ if $v \ge 0$, else 0.

**Solution:**
Input: $x=[1, 0]$.
$net_3 = 1(2) + 0(-3) = 2 \to a_3 = 1$.
$net_4 = 1(1) + 0(4) = 1 \to a_4 = 1$.
$net_5 = a_3(2) + a_4(-1) = 2 - 1 = 1 \to a_5 = 1$.
Output is **1**.

#### 8.2. Backpropagation Calculation
**Problem:** Given initial weights and training data (as shown in slide 21), perform one step of backpropagation to update the weights.

**Solution:**
1. Forward pass to get all $a^{(l)}$.
2. $\delta_j^{(L)} = (a_j^{(L)} - y_j) a_j^{(L)}(1 - a_j^{(L)})$.
3. $\delta_i^{(L-1)} = (\sum W_{ij} \delta_j^{(L)}) a_i^{(L-1)}(1 - a_i^{(L-1)})$.
4. $\frac{\partial E}{\partial W_{ij}} = a_i \delta_j$.
5. $W := W - \alpha \frac{\partial E}{\partial W}$.

---
**References:**
- [Stanford Machine Learning - Andrew Ng](http://openclassroom.stanford.edu/MainFolder/CoursePage.php?course=MachineLearning)
- [Activation Functions (Wikipedia)](https://en.wikipedia.org/wiki/Activation_function)
- [Step-by-step Backpropagation Example](https://mattmazur.com/2015/03/17/a-step-by-step-backpropagation-example/)

---

## Lecture 4: Model Evaluation
**Lecturer:** Dr. Le Huu Ton  
**Date:** Hanoi, 2017

---

### 1. Model Selection Ideas

#### 1.1. Idea #1: Hyperparameter Tuning on All Data
Choose hyperparameters that work best on the entire dataset. (Warning: This leads to over-optimistic results and poor generalization).

#### 1.2. Idea #2: Train/Test Split
Split data into **Train** and **Test** sets. Choose hyperparameters that work best on the test data.

#### 1.3. Idea #3: Train/Validation/Test Split
Split data into three sets:
- **Training Dataset:** The sample of data used to fit the model.
- **Validation Dataset:** The sample of data used to provide an unbiased evaluation of a model fit on the training dataset while tuning model hyperparameters. The evaluation becomes more biased as skill on the validation dataset is incorporated into the model configuration.
- **Test Dataset:** The sample of data used to provide an unbiased evaluation of a final model fit on the training dataset.

#### 1.4. Idea #4: Cross-Validation
Split data into $k$ folds. Try each fold as validation and average the results.
- Useful for small datasets.
- Not used too frequently in Deep Learning due to computational cost.

---

### 2. Evaluation of Regression Models

#### 2.1. Mean Absolute Error (MAE)
MAE is the sum of the absolute differences between predictions and actual values:
$$MAE = \frac{1}{m} \sum_{i=1}^{m} |y^{(i)} - h(x^{(i)})|$$

#### 2.2. Mean Squared Error (MSE)
MSE measures the average of the squares of the errors—the difference between the real value and the predicted one:
$$MSE = \frac{1}{m} \sum_{i=1}^{m} (y^{(i)} - h(x^{(i)}))^2$$

#### 2.3. R Square ($R^2$)
$R^2$ (Coefficient of Determination) provides an indication of the goodness of fit of a set of predictions to the actual values.

- **Total Sum of Squares ($SS_{tot}$):** Proportional to the variance of the data.
  $$SS_{tot} = \sum_{i=1}^{m} (y^{(i)} - \bar{y})^2$$
  Where $\bar{y} = \frac{1}{m} \sum y^{(i)}$.
- **Residual Sum of Squares ($SS_{res}$):**
  $$SS_{res} = \sum_{i=1}^{m} (y^{(i)} - h(x^{(i)}))^2$$
- **Formula:**
  $$R^2 = 1 - \frac{SS_{res}}{SS_{tot}}$$

---

### 3. Evaluation of Classification Models

#### 3.1. Confusion Matrix
A confusion matrix (or error matrix) is a specific table layout that allows visualization of the performance of an algorithm.

**Example Matrix (Multiclass):**
| Predicted \ Actual | Cat | Dog | Rabbit |
| :--- | :--- | :--- | :--- |
| **Cat** | 5 | 2 | 0 |
| **Dog** | 3 | 3 | 2 |
| **Rabbit** | 0 | 1 | 11 |

**Binary Classification Layout:**
| Known \ Predicted | Positive | Negative |
| :--- | :--- | :--- |
| **Positive** | True Positive (TP) | False Negative (FN) |
| **Negative** | False Positive (FP) | True Negative (TN) |

#### 3.2. Performance Metrics
- **Precision:** The percentage of positive predictions that are correct.
  $$\text{Precision} = \frac{TP}{TP + FP}$$
- **Recall / Sensitivity:** The percentage of positive labeled instances that were predicted as positive.
  $$\text{Recall} = \frac{TP}{TP + FN}$$
- **Specificity:** The percentage of negative labeled instances that were predicted as negative.
  $$\text{Specificity} = \frac{TN}{TN + FP}$$
- **Accuracy:** The percentage of predictions that are correct.
  $$\text{Accuracy} = \frac{TP + TN}{TP + TN + FP + FN}$$
- **F-score (F1-score):** Harmonic mean of precision and recall.
  $$F = 2 \cdot \frac{\text{Precision} \cdot \text{Recall}}{\text{Precision} + \text{Recall}}$$
- **Root Mean Squared Error (RMSE):** Often used in regression but can be used in classification contexts (e.g., comparing predicted probabilities to binary outcomes).
  $$RMSE = \sqrt{\frac{1}{m} \sum (y^{(i)} - h(x^{(i)}))^2}$$

---
**References:**
- [Stanford Machine Learning - Andrew Ng](http://openclassroom.stanford.edu/MainFolder/CoursePage.php?course=MachineLearning)
- [Activation Functions (Wikipedia)](https://en.wikipedia.org/wiki/Activation_function)
- [Step-by-step Backpropagation Example](https://mattmazur.com/2015/03/17/a-step-by-step-backpropagation-example/)

---

## Lab Practice 1: Linear Regression Implementation

### 1. Prerequisites
- **Basic Python:** Recommended tutorial: [W3Schools Python Tutorial](https://www.w3schools.com/python/). Focus on basic syntax, variables, data types, loops, and functions.

### 2. Linear Regression Implementation Task
**Dataset:** Advertising dataset (Sales value for different products based on marketing spend on Television, Radio, and Newspaper).

**Requirements:**
- Implement the Linear Regression algorithm from scratch to predict sales value given the three inputs.
- Calculate the cost function after each iteration.
- Visualize the cost function as a function of the number of iterations to check for convergence.
- Experiment with various values for the learning rate $\alpha$ and the number of iterations.

### 3. Advanced Tasks
- Solve the same advertising problem using the **Normal Equation** method.
- Redo the implementation (Gradient Descent and Normal Equation) including **Regularization**.
