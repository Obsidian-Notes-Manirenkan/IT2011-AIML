```python
# Convert Date and sort chronologically
df['Date'] = pd.to_datetime(df['Date'])
df = df.sort_values('Date').reset_index(drop=True)
```

- **`pd.to_datetime`** converts the `Date` column from strings (`object`) into real datetime values, which you need for sorting, date-based splits, and plotting by date.
- **`sort_values('Date')`** puts the rows in chronological order.
- **`reset_index(drop=True)`** rebuilds a clean 0..n−1 index after sorting and discards the old one

---

> A **chronological split** means training on the past and testing on the future. Most code does that by position, not by looking at the dates, so the row order has to be correct first.

---

## What goes wrong with unsorted rows

Suppose the rows were shuffled or out of order, for example with 2015 rows mixed in among 1970 rows. The first 80% of rows would then contain a random mix of old and recent dates, and the test set would too.

##### That causes two problems:

1. **Future leaks into training.** The model could train on 2018 prices and then be tested on 2016, which is predicting the past from the future. Real trading never allows that.
2. **Scores look better than they are.** Neighboring days have very similar prices, so a model that has seen the days around a test day can nearly interpolate it. The test result would be overly optimistic and would not reflect real forecasting ability.