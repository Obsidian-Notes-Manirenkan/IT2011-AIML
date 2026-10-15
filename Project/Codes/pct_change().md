```python
df['Return'] = df['Adj Close'].pct_change()
```

This line creates a new column called `Return` that holds each day's percentage change in `Adj Close` compared with the previous row.

---

**What `pct_change()` does**

For each row, it calculates:

$$r_t = \frac{P_t - P_{t-1}}{P_{t-1}}$$

where $P_t$ is today's `Adj Close` and $P_{t-1}$ is the value in the row directly above it. It's the same as writing `df['Adj Close'] / df['Adj Close'].shift(1) - 1`.

---

**Example**

|Date|Adj Close|Return|
|---|---|---|
|Day 1|100.0|NaN|
|Day 2|102.0|0.02|
|Day 3|101.0|-0.0098|
|Day 4|103.0|0.0198|

For Day 2 the calculation is $\frac{102 - 100}{100} = 0.02$, a 2% rise. For Day 3 it's $\frac{101 - 102}{102} \approx -0.0098$, a 0.98% fall.

---

**Things to know**

- **The first row is `NaN`.** There's no earlier price to compare against. That's one of the rows the notebook drops later.
- **It compares to the previous row, not the previous calendar day.** The data only has trading days, so a Monday return compares against Friday's close.
- **The data must be sorted by date first.** If the rows were out of order, the returns would be wrong. Your notebook sorts by `Date` before this step.
- **Values are fractions, not percentages.** 0.02 means 2%. Multiply by 100 if you want to display it as a percentage.
- **It uses `Adj Close`, not `Close`.** The adjusted price accounts for dividends and stock splits, so a split doesn't appear as a fake crash.

---

**Why it's the foundation for the other features**

`Return` feeds several of the later features: the lagged returns, the rolling volatility and the target itself (`Return.shift(-1) > 0`). It is also the quantity the extreme-return check looked at (Black Monday at about -21.6%).