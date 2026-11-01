![[Pasted image 20261031163717.png]]

---

# Avoiding Overfitting

1. [[Adding Dropouts]]
2. [[Early Stopping]]

---

# How to identify whether the model is overfitting or not by using a diagram?

![[file-201b2183f96625ec2b4e6241a86d1eff.png]]

### How to read the diagram

- **Epochs 1 to 6:** both errors fall together, so the model is learning real patterns (underfitting turning into a good fit).
- **Around epoch 6:** validation error is at its minimum. This is the best point to stop training (early stopping).
- **After epoch 6:** training error keeps decreasing, but validation error starts to rise. The growing gap between the two curves is the sign of overfitting.

### Rule of thumb for the answer sheet

- Low training error and high validation/test error means the model is overfitting.
- High error on both means underfitting.
- Low error on both, with a small gap, means a good fit.