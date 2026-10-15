We take the log of `Volume` to fix two problems with the raw numbers: 
1. It is extremely skewed
2. It grows over the decades

---

## **1. Volume is heavily right-skewed**

Most days have ordinary volume, but a few days (crashes, earnings, index rebalancing) have *volume several times higher*[^1]. A histogram of raw `Volume` shows a tall bar near the low end and a long tail stretching far to the right. Those few huge values dominate:
- **Logistic regression** is sensitive to the size of inputs, so a handful of spike days would pull the coefficient toward them.
- **Scaling doesn't fix it.** `RobustScaler` changes the center and spread, but it keeps the shape, so the long tail stays.

![[Pasted image 20261005072649.png]]

---

## **2. The log compresses large values and spreads out small ones**

$$\text{Log Volume}_t = \ln(1 + \text{Volume}_t)$$

|Raw volume|Log volume|
|---|---|
|1,000,000|13.8|
|2,000,000|14.5|
|10,000,000|16.1|
|50,000,000|17.7|

A 50x range in raw volume becomes a spread of about 4 units. The distribution ends up much closer to symmetric, which suits a linear model.

---

## **3. Differences in log volume mean percentage changes**

$$\ln V_t - \ln V_{t-1} = \ln\!\left(\frac{V_t}{V_{t-1}}\right)$$
So `Log_Volume_Change` is the (log) percentage change in trading activity from one day to the next. A jump from 1M to 2M shares and one from 10M to 20M both count as "volume doubled", which is the comparison you want. On raw volume, the second jump would look ten times larger.

---

## **4. Why `log1p` and not `log`**

`np.log1p(x)` computes $\ln(1 + x)$. It handles a volume of exactly 0 without error, whereas `np.log(0)` gives $-\infty$. For CAT the volume is almost certainly never zero, but `log1p` is a safe default.

**Why this matters for your data**

Volume also has a long-term drift (CAT traded far fewer shares in the 1960s than it does today), so raw volume is partly non-stationary like the price. The log reduces that effect, and the day-to-day change in log volume removes it almost entirely.

**A quick way to see it yourself**

```python
fig, axes = plt.subplots(1, 2, figsize=(11, 4))
axes[0].hist(df["Volume"], bins=60)
axes[0].set_title("Raw Volume")
axes[1].hist(df["Log_Volume"], bins=60)
axes[1].set_title("Log Volume")
plt.tight_layout()
plt.show()
```

Use this as a before-and-after in your report. The first plot should look like a steep cliff with a long tail, and the second like a rounder bell shape.

**For your report:** _"Trading volume is heavily right-skewed, so a log transform (log1p) was applied to compress extreme spikes and make the distribution closer to symmetric. The day-to-day change in log volume represents the percentage change in trading activity."_

[^1]: [[Reason for the Volume being higher at some points]]
