#### Disadvantages of Filling with Zero

* **Artificial Crashes:** A stock price of $0 fundamentally dictates that the asset is entirely worthless. Inserting a 0 creates an immediate, catastrophic 100% price drop in your dataset.
* **Distorted Volatility:** Your machine learning algorithm will attempt to learn from this synthetic crash, which will severely skew technical indicators and any momentum features you calculate later, such as Daily Returns.

---
#### Disadvantages of Filling with the Average (Mean)
  
* **Trend Destruction:** Financial data is strictly chronological. If a stock averages \$50 over a five-year period, inserting that \$50 into a missing day during a bull market where the stock was trading at \$150 creates an artificial \$100 plunge.
* **Data Leakage:** Calculating a mean requires aggregating the entire dataset. If you use future prices to calculate an average to fill a past gap, you leak future information into the past, entirely invalidating the model's predictive integrity.

