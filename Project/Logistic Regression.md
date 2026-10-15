The model estimates the probability that **tomorrow is a high-volatility day**:
$$P(y_t = 1 \mid x_t) = \frac{1}{1 + e^{-(\beta_0 + \beta_1 x_{t,1} + \dots + \beta_k x_{t,k})}}$$
where $y_t = 1$ means $|r_{t+1}| > \tau$, and $x_t$ holds the 19 features known at the close of day $t$. A day is predicted **high-volatility** when this probability exceeds 0.5.

The model is trained by minimizing the regularized log-loss. With the default L2 penalty:
$$\min_{\beta}\; \frac{1}{2}\lVert\beta\rVert_2^2 + C\sum_{t=1}^{n}\Big[-y_t\log p_t-(1-y_t)\log(1-p_t)\Big]$$
A **smaller $C$ means stronger regularization**.

A majority-class baseline is included as a reference. The model only has value if it beats the baseline.  

**Additional note:** logistic regression is a *linear* model in the (scaled) features. That is a good, interpretable starting point, but it cannot capture interactions such as "high volatility *and* a large gap". This is a useful point for the final comparison with tree-based or other non-linear models from the other members.

---

[[Why Logistic Regression suits this dataset & problem]]