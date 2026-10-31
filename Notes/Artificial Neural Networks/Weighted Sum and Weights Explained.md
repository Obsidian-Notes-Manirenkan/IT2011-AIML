## Part 1: The Weighted Sum Equation

This equation is the **weighted sum** (the "linear combiner") of neuron $k$. It's the first step a neuron does before any activation function is applied:

$$u_k = \sum_{j=1}^{m} w_{kj}\, x_j$$

***

### What each symbol means

- $x_j$ is the $j$-th input signal to the neuron, where $j$ runs from $1$ to $m$. In a dataset, these are your features.
- $w_{kj}$ is the weight on the connection from input $j$ into neuron $k$. The first subscript says which neuron the weight belongs to, and the second says which input it multiplies.
- $m$ is the number of inputs.
- $\sum_{j=1}^{m}$ means "add up the $m$ terms, one for each input".
- $u_k$ is the result, called the linear combiner output.

***

### The intuition

Each weight says how much its input matters to this neuron. A large positive weight means the input pushes the neuron strongly toward firing, a negative weight pushes against it, and a weight near zero means the input is mostly ignored. The neuron multiplies each input by its importance and adds everything up into one number.

***

### A quick numeric example

Say neuron $k$ has three inputs and weights:

$$x = (2,\ 1,\ 3), \qquad w_k = (0.5,\ -1,\ 0.2)$$

$$u_k = (0.5)(2) + (-1)(1) + (0.2)(3) = 1 - 1 + 0.6 = 0.6$$

This is also the **dot product** of the weight vector and the input vector:

$$u_k = \mathbf{w}_k^T \mathbf{x}$$

***

### Where it fits in the full neuron

The bias and the activation function come after this step:

$$v_k = u_k + b_k, \qquad y_k = \varphi(v_k)$$

So the pipeline is: weighted sum $\rightarrow$ add bias $\rightarrow$ pass through the activation function (a step or signum function for the perceptron).

The reference sheet's earlier version of this line used $x_k$, which was a typo. The input must be indexed by $j$, because each term uses a different input, not the same $x_k$ repeated.

***

## Part 2: Understanding $w_{kj}$

Think of $w_{kj}$ as a **label for one specific connection**. The two subscripts work like an address:

- **$k$** is the neuron the connection goes **into** (the receiver).
- **$j$** is the input the connection comes **from** (the sender).

So $w_{kj}$ means "the weight on the line from input $j$ to neuron $k$".

***

### A concrete picture

Say you have 3 inputs ($x_1, x_2, x_3$) and 2 neurons ($k = 1, 2$). Every input connects to every neuron, so there are $2 \times 3 = 6$ separate weights:

| | from $x_1$ | from $x_2$ | from $x_3$ |
|---|---|---|---|
| **into neuron 1** | $w_{11}$ | $w_{12}$ | $w_{13}$ |
| **into neuron 2** | $w_{21}$ | $w_{22}$ | $w_{23}$ |

Each row belongs to one neuron. For example, $w_{23}$ is the weight on the connection from input 3 into neuron 2.

***

### How it plugs into the equation

For neuron 2 ($k = 2$), the sum uses only row 2:

$$u_2 = \sum_{j=1}^{3} w_{2j}\, x_j = w_{21}x_1 + w_{22}x_2 + w_{23}x_3$$

The $k$ stays fixed because you're computing one neuron's output. The $j$ changes as the sum steps through the inputs.

***

### Why two subscripts are needed

If you wrote just $w_j$, you couldn't tell which neuron the weight belongs to, and every neuron needs its own set of weights. Two neurons can treat the same input very differently, for example $w_{21}$ large and $w_{11}$ small.

***

### The single perceptron case

A perceptron is a single neuron, so there's only one value of $k$. In that case people often drop it and write $w_j$ or $w_i$, and the equation becomes:

$$u = \sum_{j=1}^{m} w_j\, x_j$$

The $k$ only matters once you have a layer with multiple neurons, like in the multi-layer networks later in the reference sheet, where all the weights collect into a matrix $W$ whose entries are exactly these $w_{kj}$.
