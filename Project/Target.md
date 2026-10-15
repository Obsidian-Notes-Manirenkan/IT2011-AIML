For each trading day $t$, the label describes **tomorrow**, day $t+1$:
$$  
y_t =  
\begin{cases}  
1 & \text{if } |r_{t+1}| > \tau \\  
0 & \text{otherwise}  
\end{cases}  
$$
where $r_{t+1}$ is tomorrow's daily return:
$$r_{t+1} = \frac{P_{t+1} - P_t}{P_t}$$
and $P$ is the adjusted close. Three pieces make up the label:
- **Return $r_{t+1}$:** the percentage change in CAT's price from today's close to tomorrow's close.
- **Absolute value $|r_{t+1}|$:** the size of that move, ignoring direction. A +3% day and a −3% day both count as "3%".
- **[[Threshold]] $\tau$:** the cutoff between "calm" and "big move". In your notebook, $\tau = 0.00960$, i.e. **0.96%**.

---

### What "high-volatility" means here

Volatility is how much a price moves, regardless of direction. Here it is measured in the simplest way, by the size of one day's move. So the model is **not** predicting whether CAT goes up or down. It predicts whether tomorrow will be **eventful or quiet**.

"High" is also **relative to CAT's own history**. A day with a 1.1% move is labelled high-volatility, even though that is hardly a crash. The word describes "bigger than a typical CAT day in 1962–2008", not "dramatic".

---

### Why the threshold is the median of the training set

1. **Balanced classes.** The median splits the data in half by definition, so the training set is exactly 50% class 1 and 50% class 0 (the notebook shows 0.5000). With balanced classes, accuracy is a fair metric, and the 50% baseline is easy to read.
2. **No leakage.** The threshold is computed only from the training period (1962 to Aug 2008). If it were computed on the full dataset, information from the test period (2008 to 2020) would shape the labels. The notebook splits by time first, then computes $\tau$.
3. **Honest regime shift.** The same fixed $\tau$ is applied to the test set. The test share comes out at 0.5022, so the classes stay balanced there too, even though that period includes the 2008 crisis and COVID.

---

### Why volatility instead of direction

This is the main reason for the switch from the proposal's Up/Down idea.

- **Direction is close to a coin flip.** Whether a stock rises or falls tomorrow is very hard to predict from past prices. This is essentially the intuition behind the efficient market hypothesis. *A direction model usually lands near 50% accuracy, and it is hard to tell skill from luck*.
- **Volatility clusters.** Big moves tend to follow big moves, and calm periods follow calm periods. The notebook's rolling-volatility plot shows this: spikes bunch around 1987, 2008 and 2020. So recent volatility carries real information about tomorrow's volatility.
![[Pasted image 20261005131310.png]]
- **The data backs it up.** In your correlation plot, the top features are all volatility-related (`HL_Range_5`, `Volatility_60`, `HL_Range`, `Volatility_20`), while signed features like `Return` and `MA5_Ratio` sit near zero. Direction features tell the model almost nothing about size.
![[Pasted image 20261005131442.png]]
- **It has real-world use.** Risk management (position sizing, hedging, flagging unusual days) cares about "how big might the move be?" more than "which way?". This ties back to the proposal's "Risk Teams: flagging unusual short-term volatility" use case.

---

### What your results say about the target

|Model|Accuracy|ROC-AUC|
|---|---|---|
|Majority baseline|0.4978|0.500|
|Logistic regression (tuned)|0.6268|0.681|

The model beats the baseline by about 13 points of accuracy, which suggests the target is learnable. It is still far from perfect, which is realistic. The confusion matrix shows 581 false alarms and 509 missed high-volatility days.

![[Pasted image 20261005131734.png]]

---

### Limitations

^0d2cd3

- **Binary labelling loses information.** A day with a 1.0% move and a day with a 20% crash both get label 1. The model cannot tell how big the move is, only that it crosses the line.
- **Days near the threshold are close to noise.** A move of 0.95% versus 0.97% flips the label, yet the two days are nearly identical.
- **One fixed $\tau$ across 58 years.** CAT's typical daily move changed over the decades, so "high-volatility" means different things in 1970 and 2015.
- **Target only describes tomorrow.** It says nothing about direction, so it cannot by itself tell you whether to buy or sell.