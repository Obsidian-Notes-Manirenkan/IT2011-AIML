- `Close` and `Adj Close` carry almost the same information. They differ only by a dividend adjustment factor that grows as we go further back in time, so keeping both adds redundancy (multicollinearity) without adding signal.
	- "Without adding signal" means the extra column doesn't give the model any new, useful information to learn from.
- `Adj Close` is the better one to keep for modeling because it reflects total return. A raw `Close` shows artificial drops on dividend dates, which a model could mistake for real price moves.

---

**What it leaves unresolved**

Once `Close` is gone, `Open`, `High`, and `Low` are still on the raw price scale while `Adj Close` is on the adjusted scale. That's the mismatch I mentioned before (1.60 versus 0.137 in the first row). We can fix it by putting all four on the adjusted scale, using the factor we already have in the data:
$$f_t = \frac{\text{Adj Close}_t}{\text{Close}_t}, \qquad \text{Open}^{adj}_t = f_t \cdot \text{Open}_t$$
The order matters here. If we drop `Close` first, we lose the information needed to compute the factor.

---

**One caveat**

Whether dropping it is right also depends on our prediction target. If we're predicting the next day's price or trend direction, build the target from `Adj Close` (for example, the next day's return), so features and target stay on the same basis.

So I'd keep dropping `Close`, but move the drop after the adjustment step.
