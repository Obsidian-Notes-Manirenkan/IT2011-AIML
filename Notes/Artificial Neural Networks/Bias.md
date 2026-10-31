# Bias in Machine Learning & Neural Networks

![[Pasted image 20261018084218.png]]

---

## 1. What Exactly is Bias?

In Machine Learning and Artificial Neural Networks (ANNs), **bias ($b$)** is an independent, learnable parameter added to the weighted sum of inputs before passing through an activation function.

### Mathematical Formulation
For a single neuron or linear model:
$$u = \sum_{i=1}^{m} w_i x_i + b$$
$$y = \varphi(u) = \varphi\left(\sum_{i=1}^{m} w_i x_i + b\right)$$

Where:
* $x_i$: Input features ($x_1, x_2, \dots, x_m$)
* $w_i$: Synaptic weights ($w_1, w_2, \dots, w_m$) representing the strength or influence of each input
* $b$: **Bias term**, acting as an offset
* $\varphi(\cdot)$: Activation function (e.g., Sigmoid, ReLU, Step function)
* $y$: Final output

### The Intuitive Analogy: Equation of a Line
Think of the classic 2D straight line equation:
$$y = mx + c$$
* $m$ (slope / orientation) $\rightarrow$ corresponds to **Weights ($w$)**
* $c$ ($y$-intercept / vertical shift) $\rightarrow$ corresponds to **Bias ($b$)**

---

## 2. Why Do We Use Bias?

### A. Preventing the Model from Being Trapped at the Origin $(0, 0)$
If you do not include bias ($y = Wx$), then whenever all inputs are zero ($x = 0$), the output **must be zero**:
$$y = W(0) = 0$$

Without bias, any regression line or classification hyperplane is **forced to pass directly through the origin $(0, 0)$**. 

In the real world, relationships rarely pass through $(0, 0)$:
* **House Prices:** An empty plot with 0 sq. ft. living area still has a base land value ($b > 0$).
* **Exam Scores:** A student studying 0 hours does not necessarily score 0%.
* **Classification:** If two classes are located around $(5, 5)$ and $(8, 8)$, a separating line through $(0, 0)$ cannot separate them properly.

### B. Adjusting the Neuron's Firing Threshold
In a biological neuron or artificial perceptron, bias controls **how easily the neuron fires (activates)**:
$$\sum_{i=1}^m w_i x_i + b \ge 0 \iff \sum_{i=1}^m w_i x_i \ge -b$$
* The term **$-b$** acts as the activation **threshold**.
* A **high positive bias** means the neuron activates easily, even with low or zero input.
* A **negative bias** requires strong positive inputs before the neuron can fire.

---

## 3. What Does Bias Do to the Data & Model?

> **Important distinction:** Bias does **not** alter, scale, or transform your raw input data $x$. Instead, it shifts the **model's hypothesis / decision boundary** relative to your data points.

| Component | Role | Geometric Effect |
| :--- | :--- | :--- |
| **Weights ($W$)** | Scale & orientation | **Rotates / tilts** the line or hyperplane (changes the slope). |
| **Bias ($b$)** | Translation / offset | **Shifts / translates** the line or hyperplane across space without changing its angle. |

* In activation functions (like the Sigmoid curve), bias **shifts the curve left or right** along the horizontal axis, allowing the transition region to be positioned wherever the data requires.

---
[[Neuron]]
