![[Pasted image 20261014212749.png]]

![[Pasted image 20261014213119.png]]

![[Pasted image 20261014213217.png]]

![[Pasted image 20261018175045.png]]

![[Pasted image 20261018175523.png]]

---

# Parts of Perceptron
[[Weighted Sum and Weights Explained]]
[[Bias]]
[[Activation Function]]

---

[[Batch Perceptron Algorithm]]

---

# Real-World Perceptron Example: Automated Loan Approval

An artificial neuron (perceptron) is the fundamental computational unit of an Artificial Neural Network (ANN). This guide demonstrates step-by-step how a single neuron evaluates inputs, weights, bias, and activation functions to make an automated binary decision.

---

## 1. Problem Definition

A bank wants to automate preliminary evaluations for personal loan applications. The task is a **binary classification** problem:

$$\text{Decision } y = \begin{cases} 1 & \text{Approve Loan} \\ 0 & \text{Reject Loan} \end{cases}$$

---

## 2. Neuron Architecture & Components

```
Inputs (x_i)       Synaptic Weights (w_i)
  [Credit Score]   x₁ ────► (w₁ = +4.0) ──┐
  [Income Level]   x₂ ────► (w₂ = +3.0) ──┼──► Summing Junction (Σ) ──► [v = u + b] ──► Activation φ(·) ──► Output (y)
  [Existing Debt]  x₃ ────► (w₃ = -5.0) ──┘           ▲
                                                      │
                                               Bias (b = -0.40)
```

### A. Input Features ($x_i$)
The raw application features are normalized into numeric values between $0$ and $1$:
* **$x_1 = 0.85$** (Credit Score: strong credit history)
* **$x_2 = 0.70$** (Monthly Income: above average income)
* **$x_3 = 0.90$** (Existing Debt: high existing debt obligations)

### B. Synaptic Weights ($w_i$)
Weights determine the **significance, direction, and magnitude** of each feature's contribution:
* **$w_1 = +4.0$** (Excitatory / Positive): High credit score strongly supports loan approval.
* **$w_2 = +3.0$** (Excitatory / Positive): Higher income provides additional security.
* **$w_3 = -5.0$** (Inhibitory / Negative): High existing debt acts as a severe risk penalty.

### C. Bias ($b$)
The bias acts as an adjustment or threshold-shifting parameter ($y = mx + c$ analogy, where $c$ corresponds to bias). 
* **$b = -0.40$**: Represents baseline bank stringency or risk aversion. If all inputs were zero ($x = 0$), the neuron would produce a negative score, defaulting to a rejection.

---

## 3. Step-by-Step Mathematical Computation

### Step 1: Linear Combination / Dot Product ($\sum$)
The summing junction aggregates all weighted inputs into a single linear combination $u_k$:

$$u_k = \sum_{j=1}^{m} w_{kj} x_j = (\mathbf{w} \cdot \mathbf{x})$$

$$u = (x_1 \cdot w_1) + (x_2 \cdot w_2) + (x_3 \cdot w_3)$$
$$u = (0.85 \times 4.0) + (0.70 \times 3.0) + (0.90 \times -5.0)$$
$$u = 3.40 + 2.10 - 4.50$$
$$u = +1.00$$

### Step 2: Incorporating the Bias ($b$)
The bias is added to the weighted sum to produce the net induced local field (pre-activation signal) $v$:

$$v = u + b$$
$$v = 1.00 + (-0.40) = +0.60$$

---

## 4. Applying the Activation Function ($\phi$)

The pre-activation value ($v = +0.60$) is passed to an activation function to generate the final prediction.

### Case A: Classic Perceptron (Step Function / Signum)
For a hard boundary:

$$y = \begin{cases} 1 & \text{if } (\mathbf{w} \cdot \mathbf{x} + b) \ge 0 \\ 0 & \text{otherwise} \end{cases}$$

Since $v = +0.60 \ge 0$:
$$\mathbf{y = 1 \quad (\text{Loan Approved})}$$

### Case B: Probabilistic Model (Sigmoid Function)
When the bank requires a confidence level rather than an all-or-nothing output, it uses the Sigmoid function $\sigma(v)$:

$$\sigma(v) = \frac{1}{1 + e^{-v}}$$
$$\sigma(0.60) = \frac{1}{1 + e^{-0.60}} \approx \frac{1}{1 + 0.5488} \approx 0.6456$$

$$\mathbf{y \approx 64.6\% \text{ probability of successful loan repayment}}$$

---

## 5. Other Everyday Real-World Examples

The identical formulation ($\sum w_i x_i + b \rightarrow \phi$) powers numerous binary classification tasks across domains:

| Application | Input Features ($x$) | Weights Significance ($w$) | Binary Decision ($y$) |
| :--- | :--- | :--- | :--- |
| **Email Spam Detection** | Word frequencies ("lottery", "urgent", sender reputation) | Large positive weights on trigger keywords, negative weights on trusted senders | $1$: Spam<br>$0$: Ham (Inbox) |
| **Medical Screening** | Blood glucose, systolic BP, age, BMI | Positive weights for risk-factor elevations | $1$: Disease Present<br>$0$: Healthy |
| **Fraud Detection** | Transaction size, distance from home, device IP mismatch | High positive weight on unusual geographic shifts or off-hour large transactions | $1$: Flag Transaction<br>$0$: Approve Transaction |