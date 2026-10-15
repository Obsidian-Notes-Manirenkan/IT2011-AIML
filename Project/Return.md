**Return** is the percentage change in a stock's price over a period. It measures how much you gained or lost relative to what you started with, rather than in raw dollars.

---

### **Simple (daily) return**
$$r_t = \frac{P_t - P_{t-1}}{P_{t-1}} = \frac{P_t}{P_{t-1}} - 1$$
where $P_t$ is today's `Adj Close` and $P_{t-1}$ is yesterday's. If a stock goes from \$100 to \$102:
$$r_t = \frac{102 - 100}{100} = 0.02 = 2\%$$
**[[Log return]]**, a common alternative:
$$r_t^{\log} = \ln\!\left(\frac{P_t}{P_{t-1}}\right)$$
For small moves the two are nearly identical. Log returns are popular because they add up across time: the log return over 5 days is the sum of the 5 daily log returns.

---
### **Why we calculate it**

1. **Prices are not comparable across stocks.** A $5 move means something very different for a $20 stock (25%) than for a $2,000 stock (0.25%). Returns put every ticker on the same scale, which matters because your dataset has thousands of them.
2. **Prices are non-stationary; returns are closer to stationary.** A price series trends and drifts, so its mean and variance change over time. Most ML models assume the data's statistical behavior is reasonably stable. Returns fluctuate around a fairly steady mean, which makes patterns easier to learn and reduces the risk of the model just learning "prices go up over time."
3. **It's how we build the target.** Your proposal says you'll predict Up/Down direction. That label comes straight from the sign of the next-day return:
$$  
y_t =  
\begin{cases}  
1 & \text{if } r_{t+1} > 0 \text{ (Up)} \\  
0 & \text{otherwise (Down)}  
\end{cases}  
$$
4. **It makes good features.** Past returns (1-day, 5-day, 20-day), rolling volatility (the standard deviation of returns), and momentum indicators are all derived from returns, and they are typically more informative inputs than raw prices.

This is also why `Adj Close` matters: computing returns from raw `Close` would put fake negative returns on dividend dates, whereas `Adj Close` gives true total returns.