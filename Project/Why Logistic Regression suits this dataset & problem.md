### 1. Suitability to the problem type

**The problem is binary classification.** The target is *1 (high-volatility day)* or *0 (calm day)*. Logistic regression is designed for this: it models the probability of class 1 (high-volatility day) directly.

$$P(y_t = 1 \mid \mathbf{x}_t) = \frac{1}{1 + e^{-(\beta_0 + \beta_1 x_{t,1} + \dots + \beta_k x_{t,k})}}$$

Because it outputs a **probability**, it fits a risk-management use case. You can rank days by risk, move the cutoff to favor recall or precision, and draw the ROC curve. A model that only outputs hard labels would not allow this.

**The classes are balanced.** The threshold is the training median, so the train set is 50/50 (test 50.2%). Logistic regression works well without special handling such as resampling or `class_weight`, and accuracy is a fair metric next to ROC-AUC.

---
### 2. Suitability to the dataset

|Dataset property|Why logistic regression fits|
|---|---|
|**Tabular, numeric features only** (19 engineered features, no categoricals)|No encoding needed. Linear models work naturally on numeric inputs.|
|**Moderate size** (11,680 train rows, 2,921 test rows)|Plenty of rows for 19 parameters (about 600 rows per feature), so overfitting risk is low.|
|**Features have a roughly monotone link to the target**|The notebook's correlation plot shows `HL_Range_5`, `Volatility_60`, `HL_Range`, `Volatility_20` all positively related to tomorrow's volatility. A linear effect on the log-odds is a reasonable first approximation.|
|**Correlated features** (the volatility windows, the two MA ratios)|L2 regularization is built into the model and shares weight among correlated features, which stabilizes the coefficients.|
|**Scaled inputs**|Logistic regression is sensitive to feature scale. The group's `MinMaxScaler` inside the Pipeline handles this without leakage.|

The reason the features carry signal at all is **volatility clustering**: big moves tend to follow big moves. The features (recent volatility, intraday range,  absolute returns) are direct measures of recent turbulence, so a linear combination of them is a sensible predictor.

---
### 3. Practical suitability

- **Interpretability.** Each coefficient gives an odds ratio: $\text{odds ratio}_j = e^{\beta_j}$. For example, `HL_Range_5` has an odds ratio of about 3.88, meaning that moving from its training minimum to its maximum multiplies the odds of a high-volatility day by about 3.9. This lets you explain _why_ the model predicts what it does, which matters in finance and for a viva.
- **Stable and fast.** It converges reliably, trains in seconds, and is not sensitive to $C$ (CV AUC ranges only 0.5956 to 0.5989 across the grid).
- **A strong baseline.** With 6 members each training one model, logistic regression is the simple, linear reference against which non-linear models (trees, SVM, neural nets) can be compared.
- **Fits the evaluation setup.** It works cleanly inside a `Pipeline` with `TimeSeriesSplit`, so scaling is re-fit per fold with no leakage.

---
### 4. Evidence that it fits

|Model|Accuracy|ROC-AUC|
|---|---|---|
|Majority baseline|0.4978|0.500|
|Logistic regression (tuned)|0.6268|0.681|

It beats the baseline by about 13 accuracy points, and the predicted probability tracks real rolling volatility around 2008 and March 2020 in the notebook's last plot. So the linear form captures real structure.

---
### 5. Where it is not a perfect fit

Mention these in the viva, because they show you understand the model's limits:

- **It is linear.** It cannot capture interactions such as "large gap _and_ high volume", or U-shaped effects. Signed features like `Return` and `Momentum_10` get near-zero coefficients partly because big falls and big rallies both raise volatility, which a single linear coefficient cannot represent.
- **Multicollinearity.** The volatility and range features overlap, so individual coefficients should not be over-interpreted.
- **`MinMaxScaler` is sensitive to outliers.** Black Monday (−21.6%) stretches the range of `Return`, squeezing typical days into a narrow band. This is accepted because the group uses one common scaler.
- **Non-stationarity.** One set of coefficients is applied across 1962 to 2020, but market regimes change. A few test rows also fall outside the training range (for example, 1.4% of rows for `Volatility_60`).
- **Modest ceiling.** Test ROC-AUC of 0.68 means some skill but not a strong predictor. Tomorrow's move size is still mostly noise.
- **Single stock.** The data is only CAT, not the whole NASDAQ universe, so conclusions do not automatically generalize to other tickers.

---
### Short viva-style summary

> Logistic regression suits this task because the target is binary and balanced, the features are numeric and moderately sized, and volatility clustering gives the features a roughly monotone relationship with the target. It outputs probabilities for risk ranking, is interpretable through odds ratios, handles correlated features through L2 regularization, and works leak-free in a scaled Pipeline with time-series CV. Its limits are linearity and sensitivity to outliers under MinMaxScaler, which is why it serves as a baseline for the group's non-linear models.