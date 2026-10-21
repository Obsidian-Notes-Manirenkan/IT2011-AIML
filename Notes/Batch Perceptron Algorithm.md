![[Pasted image 20261019151325.png]]

---
# Batch Perceptron Algorithm: Walkthrough of Your Notes

## 1. The setup (top-right box)

The table shows a training set of **100 samples** being fed in. Each sample has:

|Column|Meaning|
|---|---|
|$x_1, x_2$|Input features|
|$y_{(n)}$|**Predicted** output (from the current weights)|
|$d_{(n)}$|**Truth**, the actual label|

The weights start **random**. The note on the right shows the weighted sum being computed as $x_1 w_1 + x_2 w_2$, with $w_1, w_2$ marked "random". In vector form:

$$  
\mathbf{w}^T\mathbf{x} = w_1 x_1 + w_2 x_2  
$$

The subscript $(n)$ on $\mathbf{w}_{(n)}$ is the **iteration index**, since the weights change as training proceeds.

The two example rows are:

|$x_1$|$x_2$|Predicted $y$|Truth $d$|$y \cdot d$|
|---|---|---|---|---|
|1|1.5|$+1$|$-1$|$-1$|
|2|2.5|$-1$|$+1$|$-1$|

Both rows are **misclassified** because prediction and truth disagree. The bracket and "$< 0$" show that for misclassified samples the product of predicted and actual is negative.

---
## 2. Decision rule (top-left)

$$  
\mathbf{w}_{(n)}^T\mathbf{x}_{(n)} > 0 \rightarrow C_1\ (\text{labelled } -1)  
$$

$$  
\mathbf{w}_{(n)}^T\mathbf{x}_{(n)} < 0 \rightarrow C_2 \ (\text{labelled } +1)  
$$

The **sign of $\mathbf{w}^T\mathbf{x}$** decides the class. This is your lecturer's labelling convention, with $C_1 \to -1$ and $C_2 \to 1$. Many textbooks use the opposite assignment, but the algorithm works the same either way as long as you stay consistent.

---
## 3. The misclassification condition

The wavy underline on $\mathbf{w}^T\mathbf{x}$ marks it as the **predicted** side, and the arrow on $d$ is labelled **Actual**:

$$  
\underbrace{\mathbf{w}_{(n)}^T\mathbf{x}_{(n)}}_{\text{predicted sign}} \cdot \underbrace{d_{(n)}}_{\text{actual}} < 0 \quad \checkmark \quad \text{(for all misclassified samples)}  
$$

**Why this works:**

- If the prediction and the actual label have the **same sign**, the product is **positive**, so the sample is correct.
- If they have **opposite signs**, the product is **negative**, so the sample is misclassified.

Flipping the sign gives a quantity that is positive for each misclassified sample (the "1 sample" note):

$$  
-\left(\mathbf{w}_{(n)}^T\mathbf{x}_{(n)}d_{(n)}\right) > 0  
$$
---
## 4. The cost function

Summing that positive quantity over all misclassified samples gives the **cost function** (the "Cost Function" label with the upward arrow):

$$  
J(\mathbf{w}) = -\sum_{\mathbf{x}\in\mathcal{X}} \mathbf{w}_{(n)}^T\mathbf{x}_{(n)}d_{(n)}  
$$

where $\mathcal{X}$ is the **set of misclassified samples**, and $\mathbf{x} \in \mathcal{X}$ under the sigma means the sum runs only over those samples. I've included the minus sign from the line above, since without it the sum would be negative.

**Properties:**

- Each term is positive, so $J(\mathbf{w}) \ge 0$.
- If nothing is misclassified, the sum is empty and $J(\mathbf{w}) = 0$, the best case.

---
## 5. The numeric examples (right side)

Your notes use two scenarios:

|Total samples|Misclassified|Effect|
|---|---|---|
|100|25|25 positive terms in the sum|
|100|50|50 positive terms, so a larger $J(\mathbf{w})$|

The "25 → 50" written above the sigma shows the number of terms growing. This leads to the final conclusion at the bottom:

$$  
\text{no. of misclassified samples} \uparrow {} \Rightarrow J(\mathbf{w}) \uparrow  
$$

So **training means reducing the number of misclassified samples**, which drives $J(\mathbf{w})$ down toward 0.

---
## 6. Why it's called "batch"

The cost $J(\mathbf{w})$ is computed over **all misclassified samples from the whole dataset (all 100) at once**, rather than one sample at a time. The weights are then updated once per pass.

The update rule isn't written in this image, but it follows directly from the cost. The gradient is:

$$  
\nabla J(\mathbf{w}) = -\sum_{\mathbf{x_{(n)}}\in\mathcal{X}} \mathbf{x_{(n)}}d_{(n)}  
$$

and gradient descent gives:

$$  
\mathbf{w}_{(n+1)} = \mathbf{w}_{(n)} - \eta\nabla J(\mathbf{w}) = \mathbf{w}_{(n)} + \eta \sum_{\mathbf{x}\in\mathcal{X}} \mathbf{x}d  
$$

where $\eta$ is the learning rate.

---
## Full algorithm summary

1. Initialise $w_1, w_2$ randomly.
2. Pass **all samples** through the model and compute $\mathbf{w}^T\mathbf{x}$ for each.
3. Identify the misclassified set $\mathcal{X}$, where $\mathbf{w}^T\mathbf{x}\cdot d < 0$.
4. Compute $J(\mathbf{w})$.
5. Update the weights using the sum over $\mathcal{X}$.
6. Repeat until $\mathcal{X}$ is empty ($J = 0$) or a max iteration count is reached.

**Note:** the perceptron only converges to $J = 0$ if the data is **linearly separable**.