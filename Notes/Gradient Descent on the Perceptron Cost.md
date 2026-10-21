This explains **how** the weights are changed to reduce the cost $J(\mathbf{w})$.

**Key concepts:**

- This is a cost function vs. weight graph.
- To reduce the cost function, we need to change the weights.

---
## 1. The graph: cost vs. weight

The curve is the cost $J(w)$ on the vertical axis against a weight $w$ on the horizontal axis. It is a bowl shape, and the **minimum of the bowl is the best weight**, where the cost is lowest. The target is the point marked $w_x$ on the axis.

Three starting positions are marked:

| Point | Weight | Where it sits | Tangent slope |
|---|---|---|---|
| A | $w_1$ | Far right of the minimum | $g_1$ (steep, positive) |
| B | $w_2$ | Right of the minimum, closer | $g_2$ (gentle, positive) |
| C | $w_3$ | Left of the minimum | $g_3$ (**negative**) |

Each $g$ is the **gradient**, the slope of the tangent line at that point. The coloured arrows on the axis show the direction each weight must move to reach $w_x$:

- **Blue** (from $w_1$) and **green** (from $w_2$) point **left**.
- **Yellow** (from $w_3$) points **right**.

The gradient tells us which way to move the weight.

---
## 2. The update at each point

**At point A:**

$$
w_x = w_1 - g_1
$$

**At point B:**

$$
w_x = w_2 - g_2
$$

**At point C** (the slope $g_3$ is negative, so $-g_3$ is a positive number):

$$
w_x = w_3 + (-g_3) = w_3 - g_3
$$

The notes show the last line twice: first as "$+(-g_3)$" to show that a negative slope pushes the weight **right**, then simplified to "$-g_3$". All three cases follow **one rule**:

$$
\boxed{w_{\text{new}} = w_{\text{old}} - \text{gradient}}
$$

**Why subtract the gradient?**

- Positive slope (right of the minimum): cost rises as $w$ increases, so we should **decrease** $w$.
- Negative slope (left of the minimum): cost falls as $w$ increases, so we should **increase** $w$.
- Subtracting the slope does both automatically. This is moving **opposite to the gradient**.

**Step size:** $|g_1| > |g_2|$, so the jump from A is bigger than the jump from B (the blue arrow is longer than the green one). Near the minimum the slope approaches 0, so the steps shrink and the weight settles smoothly.

## 3. The gradient of the cost

The cost for misclassified samples is $J(\mathbf{w}) = -\sum \mathbf{w}^T\mathbf{x}\,d$. Differentiating with respect to $\mathbf{w}$:

$$
\frac{\partial J(\mathbf{w})}{\partial \mathbf{w}} = \frac{\partial}{\partial \mathbf{w}}\Big(-\mathbf{w}_{(n)}^T\,\mathbf{x}_{(n)}\,d_{(n)}\Big) = -\mathbf{x}_{(n)}\,d_{(n)}
$$

For a single sample, $\mathbf{x}$ and $d$ do not depend on $\mathbf{w}$, so only $\mathbf{w}^T$ is differentiated, leaving $-\mathbf{x}\,d$.

---
## 4. The weight update rule

Substituting the gradient into "new = old − gradient" and adding a **learning rate** $\eta$:

$$
\mathbf{w}_{(n+1)} = \mathbf{w}_{(n)} - \eta\Big(-\mathbf{x}_{(n)}\,d_{(n)}\Big)
$$

The two minus signs cancel:

$$
\mathbf{w}_{(n+1)} = \mathbf{w}_{(n)} + \eta\,\mathbf{x}_{(n)}\,d_{(n)} \longleftarrow \text{1 weight update per sample}
$$

The note "**1 weight / sample**" means this version updates the weights after **each misclassified sample**.

**Why the plus sign makes sense:** after the update, the misclassified sample's score $\mathbf{w}^T\mathbf{x}\,d$ changes by

$$
\eta\,\mathbf{x}^T\mathbf{x}\,d^2 = \eta\,\|\mathbf{x}\|^2 > 0
$$

since $d^2 = 1$. The score moves in the positive direction, toward the correct side of the boundary. This is what we want, because misclassified samples have $\mathbf{w}^T\mathbf{x}\,d < 0$.

---
## 5. The batch version

The **batch perceptron** accumulates the correction from **all** misclassified samples and updates once:

$$
\mathbf{w}_{(n+1)} = \mathbf{w}_{(n)} + \eta \sum_{\mathbf{x}\in\mathcal{X}} \mathbf{x}_{(n)}\,d_{(n)}
$$

where $\mathcal{X}$ is the **set of incorrectly classified samples**.

| | Per-sample update | Batch update |
|---|---|---|
| Formula | $\mathbf{w} + \eta\,\mathbf{x}\,d$ | $\mathbf{w} + \eta\sum_{\mathcal{X}}\mathbf{x}\,d$ |
| Updates per pass | One for each misclassified sample | One in total |
| Uses | A single sample at a time | The whole misclassified set |

Correctly classified samples are **not** in $\mathcal{X}$, so they contribute nothing. Only mistakes move the weights.

---
## 6. Learning rate $\eta$

The sketch uses "$w - g$" for simplicity, but in practice we use $w - \eta g$:

- **Too large:** the weight can overshoot the minimum and bounce across the bowl.
- **Too small:** the weight creeps toward the minimum and training is very slow.

---
## 7. Summary

1. Start with random weights and compute $\mathbf{w}^T\mathbf{x}$ for every sample.
2. Find the misclassified set $\mathcal{X}$, where $\mathbf{w}^T\mathbf{x}\,d < 0$.
3. Compute the cost $J(\mathbf{w})$.
4. Compute the gradient $-\sum \mathbf{x}\,d$ and update $\mathbf{w}$ opposite to it.
5. Repeat. Each update moves the weight down the bowl toward the minimum, so fewer samples are misclassified and $J$ falls toward 0.

**Note:** the bowl in the sketch is a conceptual picture. The real perceptron cost is piecewise linear and convex, and it reaches exactly 0 only if the data is **linearly separable**.
