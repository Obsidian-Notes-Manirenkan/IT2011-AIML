# Why Do Neurons Multiply Inputs by Weights and Add Them?

## Everyday Scenario: Should I Go for a Walk?

Imagine a simple decision-making neuron that helps you decide whether to go outside for a walk. It considers three pieces of information:

|Input|Meaning|Value Today|
|---|---|---|
|$x_1$|Temperature ($^\circ\text{C}$)|$28$|
|$x_2$|Chance of rain (%)|$10$|
|$x_3$|Wind speed (km/h)|$5$|

You care about these factors differently:

- **Temperature:** You love warm weather, so it has a high positive weight.
    
- **Chance of rain:** You dislike rain, so it has a negative weight.
    
- **Wind speed:** Wind does not bother you much, so it has a small negative weight.
    

Therefore, we assign the following weights:

$$  
w_1 = +0.8 \qquad \text{(temperature)}  
$$

$$  
w_2 = -1.5 \qquad \text{(chance of rain)}  
$$

$$  
w_3 = -0.2 \qquad \text{(wind speed)}  
$$

We also introduce a **bias**:

$$  
b = -5  
$$

The negative bias represents your reluctance to go outside. You need a reasonably good reason to go for a walk.

---

## Step-by-Step Calculation

### Step 1: Multiply Each Input by Its Weight

Each input is multiplied by its corresponding weight to determine how much it contributes to the final decision.

**Temperature contribution:**

$$  
w_1x_1 = 0.8 \times 28 = 22.4  
$$

**Chance of rain contribution:**

$$  
w_2x_2 = -1.5 \times 10 = -15  
$$

**Wind speed contribution:**

$$  
w_3x_3 = -0.2 \times 5 = -1  
$$

The resulting contributions are:

| Factor         | Calculation      | Contribution |
| -------------- | ---------------- | ------------ |
| Temperature    | $0.8 \times 28$  | $+22.4$      |
| Chance of rain | $-1.5 \times 10$ | $-15$        |
| Wind speed     | $-0.2 \times 5$  | $-1$         |

Each weighted input represents the influence of one factor on the decision.

---
### Step 2: Add the Weighted Inputs and Bias

The neuron combines all the weighted inputs by adding them together and then adding the bias.

The general formula is:

$$  
v = \sum_{i=1}^{n} w_i x_i + b  
$$

For our example, this becomes:

$$  
v = w_1x_1 + w_2x_2 + w_3x_3 + b  
$$

Substituting the values:

$$  
v = (0.8 \times 28) + (-1.5 \times 10)  
$$

$$  
\phantom{v = {} } + (-0.2 \times 5) + (-5)  
$$

Therefore,

$$  
v = 22.4 - 15 - 1 - 5  
$$

$$  
\boxed{v = 1.4}  
$$

The final score is positive, indicating that the combined evidence favors going for a walk.

---
### Step 3: Apply an Activation Function

For this simple example, we use a threshold-based decision rule:

$$  
f(v) =  
\begin{cases}  
1, & \text{if } v > 0 \  
0, & \text{if } v \leq 0  
\end{cases}  
$$

Here:

- $1$ means **go for a walk**.
    
- $0$ means **do not go for a walk**.
    

Since

$$  
v = 1.4 > 0  
$$

the neuron produces:

$$  
\boxed{f(v) = 1}  
$$

**Decision: Yes, go for a walk!**

---

## What Happens If We Do Not Add the Weighted Inputs?

Without summation, we would have three separate contributions:

$$  
+22.4,\qquad -15,\qquad -1  
$$

The neuron would not have a single combined score representing the overall influence of all three factors.

Consider what might happen if we evaluated each factor independently:

- **Temperature only:** We might always go for a walk whenever the weather is warm, even when it is pouring rain.
    
- **Rain only:** We might never go outside if there is any chance of rain, even on an otherwise perfect day.
    
- **Wind only:** We might ignore the temperature and rain completely, despite their importance.
    

Each approach ignores information from the other inputs.

By adding the weighted inputs, the neuron combines all the evidence into one overall score.

For example, the positive contribution from the temperature is:

$$  
+22.4  
$$

The combined negative contributions from rain, wind, and bias are:

$$  
-15 - 1 - 5 = -21  
$$

The final result is:

$$  
v = 22.4 - 21 = 1.4  
$$

The positive contribution outweighs the negative contributions, so the neuron decides to go for a walk.

---

## Why Is Summation Important in a Neural Network?

The weighted sum allows a neuron to combine multiple inputs while accounting for their individual influences.

The calculation can be expressed as:

$$  
\boxed{v = \sum_{i=1}^{n} w_i x_i + b}  
$$

Where:

- $v$ is the weighted sum before applying the activation function.
    
- $x_i$ is the $i$-th input.
    
- $w_i$ is the weight associated with the $i$-th input.
    
- $n$ is the total number of inputs.
    
- $b$ is the bias.
    

The weights determine how strongly each input contributes to the result:

- **Positive weight:** A larger input increases the weighted sum.
    
- **Negative weight:** A larger input decreases the weighted sum.
    
- **Zero weight:** The input contributes nothing to the weighted sum.
    

The bias shifts the weighted sum independently of the input values, helping the neuron determine when its output should change.

The activation function then transforms the weighted sum into the neuron's output.

---
## Key Takeaway

**Multiplication determines each input's contribution, while summation combines those contributions into a single score.**

Without summation, the neuron would not combine the evidence from its different inputs into one overall result.

This is the fundamental idea behind a simple artificial neuron: it uses weights to determine the influence of each input, adds the weighted inputs together, incorporates a bias, and applies an activation function to produce an output.