# Comparison of Signum & Sigmoid

A clear comparison between the Signum function and the Sigmoid function.

---

## Are They Different?

Yes, they are completely different activation functions.

---

## Comparison Table

| Feature               | [[Signum Function]]                                                      | Sigmoid Function                              |
| --------------------- | ------------------------------------------------------------------------ | --------------------------------------------- |
| **Type**              | Hard threshold (binary)                                                  | Soft / smooth                                 |
| **Output range**      | Only two values: usually $-1$ or $+1$ (sometimes $0$ or $1$)             | Continuous values between $0$ and $1$         |
| **Shape**             | Sharp step (jumps suddenly)                                              | Smooth S-shaped curve                         |
| **Differentiable?**   | No (not differentiable at 0)                                             | Yes (fully differentiable)                    |
| **Used for**          | Classic Perceptron, hard decisions                                       | Modern neural networks, probabilistic outputs |
| **Mathematical form** | $\text{sign}(v) = \begin{cases} +1 & v \geq 0 \\ -1 & v < 0 \end{cases}$ | $\sigma(v) = \dfrac{1}{1 + e^{-v}}$           |

---

## Simple Intuition

- **Signum** → Makes a hard “Yes / No” decision (like a light switch that is either fully ON or fully OFF).
- **Sigmoid** → Gives a soft probability-like value (like a dimmer switch that can be anywhere between OFF and ON).

---

## Summary

They are totally different activation functions with different purposes.
