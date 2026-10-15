Here's a worked example with a few days of prices, comparing simple and log returns side by side.

**Setup:** a stock's `Adj Close` over 4 days

|Day|Adj Close|Simple return|Log return|
|---|---|---|---|
|0|$100.00|n/a|n/a|
|1|$102.00|+2.000%|+1.980%|
|2|$99.96|−2.000%|−2.020%|
|3|$104.96|+5.002%|+4.880%|

**Computing day 1:**

$$r_1^{\log} = \ln\!\left(\frac{102}{100}\right) = \ln(1.02) \approx 0.0198$$

**Computing day 2:**

$$r_2^{\log} = \ln\!\left(\frac{99.96}{102}\right) = \ln(0.98) \approx -0.0202$$

Notice that a +2% move and a −2% move don't produce symmetric log returns (+1.98% vs −2.02%). That's expected, and it actually reflects reality: after a 2% gain, you need a slightly _smaller_ than 2% drop to... wait, you actually need a 2% drop of the _new higher price_ to land at $99.96, which is a loss of $2.04 in dollar terms, and the log return captures that asymmetry.

---

**The key property: log returns add up**

Total log return over days 1 to 3, just by adding:

$$0.0198 + (-0.0202) + 0.0488 = 0.0484$$

Now check it directly from the start and end prices:

$$\ln\!\left(\frac{104.96}{100}\right) = \ln(1.0496) \approx 0.0484 \quad \checkmark$$

They match exactly. This works because logs turn products into sums:

$$\ln\!\left(\frac{P_1}{P_0}\right) + \ln\!\left(\frac{P_2}{P_1}\right) + \ln\!\left(\frac{P_3}{P_2}\right) = \ln\!\left(\frac{P_3}{P_0}\right)$$

All the middle prices cancel out.

**Simple returns don't add up**

Adding the simple returns gives:

$$2\% + (-2\%) + 5.002\% = 5.002\%$$

But the true total return is:

$$\frac{104.96}{100} - 1 = 4.96\%$$

These differ. To combine simple returns correctly, you have to multiply: $(1.02)(0.98)(1.05002) - 1 = 4.96\%$.

**Converting back to a price**

If you have a total log return, you recover the simple return with:

$$\text{simple return} = e^{\,r^{\log}} - 1 = e^{0.0484} - 1 \approx 4.96\%$$

**In pandas** (since you'll likely compute this in your preprocessing):

```python
import numpy as np

df["log_return"] = np.log(df["Adj Close"] / df["Adj Close"].shift(1))
```

`shift(1)` lines up each day with the previous day's price, and the first row becomes `NaN` because there's no prior day, so you'd drop it with `df.dropna()`.

One correction to my commentary above: the sentence about "asymmetry" was muddled. The simple explanation is just that the −2% day started from a higher base ($102), so its dollar loss was larger ($2.04) and its log return slightly more negative than the +1.98% gain.