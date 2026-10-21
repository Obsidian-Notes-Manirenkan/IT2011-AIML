This page zooms in on **one weight** to show where the "$w - \text{gradient}$" step comes from, starting from a single neuron.

---

## 1. Top-left: the main statement

$$
\text{misclassification} \uparrow \;\;\rightarrow\;\; J(\mathbf{w}) \uparrow
$$

This is the same conclusion as the first page: more misclassified samples means a higher cost. Training moves along the cost curve to a lower point.

---

## 2. Top-right: a single neuron and its cost

The diagram shows one input $x_1$ with weight $w_1$ feeding a node:

$$
y_1 = \phi(x_1 w_1)
$$

where $\phi$ is the activation function (for the perceptron, the sign function). The cost for this one sample is written as

$$
J(w) = w\,x_1\,d_1
$$

The three factors are boxed separately:

| Factor | Meaning |
|---|---|
| $w$ (blue box) | The variable we **differentiate with respect to** |
| $x_1$ (red box) | Input, a constant when differentiating |
| $d_1$ (red box) | Desired (true) label, also a constant |

Because only $w$ is the variable:

$$
\frac{\partial J}{\partial w} = x_1\,d_1
$$

This is why the **blue** $x_1$ appears on the graph as the step size. The gradient is built from the input $x_1$ (the label $d_1 = \pm 1$ only sets the sign).

**Sign note:** the first page had $J(\mathbf{w}) = -\sum \mathbf{w}^T\mathbf{x}\,d$ with a minus sign. This page drops it for simplicity, so the gradient here is $x_1 d_1$ rather than $-x_1 d_1$. The idea is identical.

---

## 3. The graph

- **Vertical axis:** $J(w)$, the cost.
- **Horizontal axis:** $w_1$, the single weight being tuned.
- **Minimum:** the dip marked $w_0$ is the **target weight** where the cost is lowest.

Note that $w_0$ here means the optimal weight and is **not the bias**, despite the similar name in the bias-trick notation.

The curve is drawn with a second bump and dip to the right, so it is **not a clean bowl**. It shows that real cost curves can have several valleys, which is why the starting position matters in gradient descent generally.

Three tangent lines are drawn:

| Point | Position | Tangent slope | Direction to $w_0$ |
|---|---|---|---|
| Right point (dark dot) | Far right of $w_0$ | $g_1$, steep and positive | Move **left** |
| Middle point (red dot, $w_3$) | Just right of $w_0$ | $g_3$, gentle and positive | Move **left**, a short way |
| Left point (red $w_2$) | Left of $w_0$ | Negative, written as $-g_2$ | Move **right** (red arrow) |

The lecturer uses the label $w_2$ for **both** the left and right points. Read them as two different starting positions that share a name.

---

## 4. The equations (bottom-right)

**Blue line, the geometric step:**

$$
w_0 = w_2 - x_1
$$

The blue arrow on the graph labelled $x_1$ runs from the right point back to $w_0$. So the distance to move equals $x_1$, which is the gradient from section 2.

**Circled line, the same step in gradient form (right point):**

$$
w_0 = w_2 - g_1
$$

Putting these together, the gradient $g_1$ and the step $x_1$ are the same quantity:

$$
g_1 \;\leftrightarrow\; x_1 d_1
$$

**Middle point:**

$$
w_0 = w_3 - g_3
$$

The slope $g_3$ is small, so the step is small. The point is already close to the minimum.

**Left point (negative slope):**

$$
w_0 = w_2 - (-g_2) = w_2 + g_2
$$

Here the slope is $-g_2$. Subtracting a negative slope **adds** to the weight and moves it right, which is the red arrow on the graph.

---

## 5. Summary of the rule

All four lines are one rule:

$$
\boxed{w_{\text{new}} = w_{\text{old}} - \text{slope at } w_{\text{old}}}
$$

| Starting point | Slope | Update | Moves |
|---|---|---|---|
| Right of minimum | $+g_1$ | $w - g_1$ | Left |
| Near minimum | $+g_3$ (small) | $w - g_3$ | Left, small step |
| Left of minimum | $-g_2$ | $w - (-g_2) = w + g_2$ | Right |

The step size is proportional to the slope, so the steps shrink near the minimum.

---

## 6. Connecting to the full update rule

Using $\frac{\partial J}{\partial w} = x_1 d_1$ (or $-x_1 d_1$ with the correct sign from the first page) and adding the learning rate $\eta$, which this sketch leaves out:

$$
w_{(n+1)} = w_{(n)} + \eta\,x_1\,d_1
$$

This is the per-sample perceptron update from the previous page. The batch version sums $x\,d$ over all misclassified samples.

---

## Points to remember

- The weight moves **opposite to the slope** to reach the minimum.
- The gradient comes from differentiating $J$ with respect to $w$, which leaves $x_1 d_1$.
- The blue $x_1$ step is a simplified picture, with $\eta$ and the sign of $d_1$ left out.
- A non-convex curve can have local minima, but the perceptron criterion itself is convex.
