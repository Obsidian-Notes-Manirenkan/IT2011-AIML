Hyperparameter tuning is the process of finding the best "settings" for a machine learning model before it starts learning.

---

### Parameters vs. hyperparameters

- **Parameters** are what the model learns by itself from the data (e.g., the weights in a linear regression or the split points in a decision tree).
- **Hyperparameters** are the settings _you_ choose before training starts. The model can't learn them on its own.

---

#### Analogy

A good analogy is baking a cake. The ingredients' behavior during baking is what the model figures out, but the oven temperature and baking time are settings you pick up front. A bad temperature gives a bad cake no matter how good the recipe is.

---

### Why it matters

The same algorithm can perform very differently depending on these settings:
- Settings that make the model too simple lead to **underfitting**: it misses real patterns.
- Settings that make it too complex lead to **overfitting**: it memorizes noise in the training data and fails on new data.

Tuning aims to find the balance where the model generalizes well to data it hasn't seen.

---

### How tuning is done

1. **Grid Search**: define a list of values for each hyperparameter and try _every_ combination. It's thorough but slow.
2. **Random Search**: try random combinations. It's often just as good as grid search and much faster.
3. **Bayesian Optimization** (e.g., Optuna): use the results of earlier trials to pick smarter combinations to try next.

In all three, each combination is evaluated using **cross-validation**, so you're judging it on data the model wasn't trained on.

---

[[Project's Hyperparameter Tuning]]