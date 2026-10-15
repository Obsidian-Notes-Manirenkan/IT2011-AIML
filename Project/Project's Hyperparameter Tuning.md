```python
param_grid = {"model__C": [0.01, 0.1, 1, 10, 100, 1000]}

grid = GridSearchCV(
    make_pipe(),
    param_grid=param_grid,
    cv=TimeSeriesSplit(n_splits=5),
    scoring="roc_auc",
    n_jobs=-1,
)

grid.fit(X_train, y_train)

best_C = grid.best_params_["model__C"]
print("Best C:", best_C)
print("Best cross-validated ROC-AUC:", round(grid.best_score_, 4))
print()

if best_C in (param_grid["model__C"][0], param_grid["model__C"][-1]):
    print("Warning: the best C is at the edge of the grid. Consider extending the grid.")

log_reg_tuned = grid.best_estimator_

# Mean CV score for every C that was tried
cv_table = (pd.DataFrame(grid.cv_results_)[["param_model__C", "mean_test_score", "std_test_score", "rank_test_score"]]
            .rename(columns={"param_model__C": "C", "mean_test_score": "Mean CV ROC-AUC", "std_test_score": "Std", "rank_test_score": "Rank"})
            .round(4))

cv_table
```

---

Best C: **0.1**  
Best cross-validated ROC-AUC: **0.5989**

| C       | Mean CV ROC-AUC | Std    | Rank |
| ------- | --------------- | ------ | ---- |
| 0.01    | 0.5956          | 0.0203 | 6    |
| 0.10    | 0.5989          | 0.0218 | 1    |
| 1.00    | 0.5979          | 0.0216 | 2    |
| 10.00   | 0.5965          | 0.0216 | 4    |
| 100.00  | 0.5967          | 0.0214 | 3    |
| 1000.00 | 0.5964          | 0.0218 | 5    |

---

