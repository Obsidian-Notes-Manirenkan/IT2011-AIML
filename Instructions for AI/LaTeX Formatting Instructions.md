# LaTeX and Markdown Formatting Instructions for AI

## 1. General Formatting Principles

- Format all mathematical notes using standard Markdown and LaTeX syntax.
    
- Ensure compatibility with Obsidian's built-in MathJax renderer.
    
- Prioritize readability, consistency, simplicity, and maintainability.
    
- Preserve the original meaning and mathematical accuracy of the content.
    
- Do not unnecessarily rewrite, shorten, or remove explanations, examples, or calculations.
    
- Use proper Markdown headings, paragraphs, lists, tables, and blockquotes where appropriate.
    
- Avoid HTML, unusual Unicode mathematical symbols, and nonstandard formatting when an equivalent Markdown or LaTeX solution exists.
    
- Keep mathematical expressions properly formatted and visually separated from explanatory text.
    

## 2. Inline Mathematical Expressions

Use single dollar signs (`$...$`) for mathematical expressions that appear within a sentence.

**Correct:**

```
The weight is represented by $w_i$, and the input is represented by $x_i$.
```

**Rendered output:**

The weight is represented by $w_i$, and the input is represented by $x_i$.

Additional examples:

```
The bias is $b = -5$.

Since $v > 0$, the neuron produces a positive output.

The input vector is $\mathbf{x} = [x_1, x_2, x_3]$.
```

### Rules

- Use inline mathematics for variables, short equations, mathematical symbols, and expressions embedded in sentences.
    
- Do not use display equations for simple variables or short expressions that fit naturally within a sentence.
    
- Always place mathematical expressions inside `$...$` when they require mathematical typesetting.
    
- Do not insert unnecessary spaces immediately inside the dollar-sign delimiters.
    

## 3. Display Mathematical Equations

Use double dollar signs (`$$...$$`) for equations that deserve their own line.

**Correct:**

```
$$
v = w_1x_1 + w_2x_2 + w_3x_3 + b
$$
```

**Rendered output:**

$$  
v = w_1x_1 + w_2x_2 + w_3x_3 + b  
$$

### Rules

- Place display equations on separate lines.
    
- Insert a blank line before and after each display equation.
    
- Put the opening and closing `$$` delimiters on separate lines.
    
- Keep each equation visually separated from the surrounding text.
    
- Use display equations for important formulas, multi-step calculations, derivations, and final results.
    
- Avoid placing explanatory prose inside mathematical delimiters.
    
- Avoid combining unrelated equations inside a single display block.
    

## 4. Mathematical Operators and Symbols

Use proper LaTeX commands instead of manually typing mathematical symbols wherever practical.

|Mathematical purpose|Preferred LaTeX syntax|Example|
|---|---|---|
|Multiplication|`\times`|$a \times b$|
|Division|`\div`|$a \div b$|
|Fraction|`\frac{a}{b}`|$\frac{a}{b}$|
|Square root|`\sqrt{x}`|$\sqrt{x}$|
|Summation|`\sum_{i=1}^{n}`|$\sum_{i=1}^{n} x_i$|
|Subscript|`x_i`|$x_i$|
|Superscript|`x^2`|$x^2$|
|Greater than or equal to|`\geq`|$x \geq 0$|
|Less than or equal to|`\leq`|$x \leq 0$|
|Approximately equal to|`\approx`|$x \approx 1.4$|
|Not equal to|`\neq`|$x \neq 0$|
|Positive or negative|`\pm`|$\pm x$|
|Absolute value|`\lvert x \rvert`|$\lvert x \rvert$|
|Parentheses|`\left( ... \right)`|$\left( a+b \right)$|
|Brackets|`\left[ ... \right]`|$\left[ a+b \right]$|
|Set braces|`\{ ... \}`|${1,2,3}$|
|Greek letters|`\alpha`, `\beta`, `\theta`|$\alpha,\beta,\theta$|
|Infinity|`\infty`|$\infty$|
|Therefore|`\therefore`|$\therefore$|

### Additional Rules

- Use `\cdot` or `\times` for multiplication when appropriate. Prefer `\times` when explaining elementary arithmetic.
    
- Use `\frac{a}{b}` for fractions in display equations.
    
- Use `\text{...}` for ordinary words appearing inside mathematical expressions.
    
- Use `\quad` or `\qquad` to introduce intentional horizontal spacing inside equations.
    
- Use `\phantom{...}` only when alignment or spacing genuinely requires it.
    
- Avoid manually inserting spaces to imitate mathematical formatting.
    

## 5. Subscripts, Superscripts, and Variables

Use braces when a subscript or superscript contains more than one character.

**Correct:**

```
x_1
x_{10}
w_i
w_{input}
x^2
x^{n+1}
```

**Incorrect:**

```
x10
winput
xn+1
```

### Rules

- Use subscripts to distinguish indexed variables, such as `$x_1$`, `$x_2$`, and `$x_3$`.
    
- Use superscripts for powers, such as `$x^2$` and `$x^3$`.
    
- Use braces for multi-character indices and exponents.
    
- Keep variable names consistent throughout the document.
    
- Do not confuse a variable's subscript with a multiplication or exponent.
    

## 6. Multi-Step Calculations

When presenting calculations, show the steps in a logical sequence.

Use explanatory text followed by a display equation for each significant step.

**Preferred format:**

```
First, calculate the weighted contribution of the temperature.

$$
w_1x_1 = 0.8 \times 28 = 22.4
$$

Next, calculate the weighted contribution of the chance of rain.

$$
w_2x_2 = -1.5 \times 10 = -15
$$

Finally, calculate the total weighted sum.

$$
v = 22.4 - 15 - 1 - 5
$$

Therefore,

$$
\boxed{v = 1.4}
$$
```

### Rules

- Present calculations in the order in which they are performed.
    
- Include intermediate steps when they help explain the reasoning.
    
- Do not skip essential arithmetic or algebraic transformations.
    
- Keep explanatory sentences outside mathematical delimiters.
    
- Use `\boxed{...}` to highlight important final answers.
    
- Do not box every intermediate result.
    
- Verify arithmetic and algebra before formatting the final output.
    

## 7. Aligned Equations

When several equations form a derivation, use the `aligned` environment inside a display-math block.

**Preferred format:**

```
$$
\begin{aligned}
v &= w_1x_1 + w_2x_2 + w_3x_3 + b \\
  &= 22.4 - 15 - 1 - 5 \\
  &= 1.4
\end{aligned}
$$
```

### Rules

- Use `&` to mark alignment points, typically before the equality sign.
    
- Use `\\` to separate lines.
    
- Keep related calculations in the same aligned block.
    
- Use separate display blocks when different calculations need individual explanations.
    
- Do not use aligned equations for unrelated mathematical expressions.
    

## 8. Cases and Piecewise Functions

Use the `cases` environment for piecewise functions, conditional definitions, and threshold-based rules.

**Preferred format:**

```
$$
f(v) =
\begin{cases}
1, & \text{if } v > 0 \\
0, & \text{if } v \leq 0
\end{cases}
$$
```

### Rules

- Use `\begin{cases}` and `\end{cases}` for piecewise expressions.
    
- Use `&` to separate each expression from its condition.
    
- Use `\\` to separate cases.
    
- Wrap explanatory words in `\text{...}`.
    
- Ensure that every case is mathematically meaningful and clearly defined.
    

## 9. Vectors, Matrices, and Mathematical Notation

Use appropriate LaTeX notation for structured mathematical objects.

### Vectors

```
$$
\mathbf{x} =
\begin{bmatrix}
x_1 \\
x_2 \\
x_3
\end{bmatrix}
$$
```

### Matrices

```
$$
A =
\begin{bmatrix}
a_{11} & a_{12} \\
a_{21} & a_{22}
\end{bmatrix}
$$
```

### Rules

- Use `\mathbf{x}` for bold vector notation when appropriate.
    
- Use `\begin{bmatrix}` and `\end{bmatrix}` for matrices and column vectors.
    
- Use `&` to separate columns and `\\` to separate rows.
    
- Choose notation appropriate to the mathematical subject.
    
- Do not introduce vector or matrix notation when the original explanation does not require it.
    

## 10. Mathematical Text and Units

Use `\text{...}` for words and units within mathematical expressions.

**Correct:**

```
$$
T = 28\,^\circ\text{C}
$$
```

```
$$
s = 5\,\text{km/h}
$$
```

```
$$
P(\text{rain}) = 10\%
$$
```

### Rules

- Use `\text{...}` for units and ordinary words inside mathematical expressions.
    
- Use `\,` to create a small space between a numerical value and its unit.
    
- Use `^\circ` for the degree symbol.
    
- Preserve the distinction between numerical values, variables, units, and percentages.
    
- Do not italicize ordinary descriptive words as though they were mathematical variables.
    

## 11. Markdown Headings and Document Structure

Organize notes using a clear heading hierarchy.

**Preferred structure:**

```
# Main Topic

## Subtopic

### Explanation

#### Additional Details
```

### Rules

- Use a single `#` heading for the main topic.
    
- Use `##` for major sections.
    
- Use `###` for subsections.
    
- Use `####` only when an additional level is genuinely necessary.
    
- Do not skip heading levels without a good reason.
    
- Leave a blank line between headings and surrounding content.
    
- Use descriptive headings that communicate the subject of each section.
    
- Avoid decorative emojis in headings.
    
- Do not use headings merely to emphasize individual sentences.
    

## 12. Tables Containing Mathematical Expressions

Use Markdown tables for structured comparisons, input values, calculations, and summaries.

**Preferred format:**

```
| Input | Meaning | Value |
|:---:|---|---:|
| $x_1$ | Temperature ($^\circ\text{C}$) | $28$ |
| $x_2$ | Chance of rain (%) | $10$ |
| $x_3$ | Wind speed ($\text{km/h}$) | $5$ |
```

### Rules

- Use standard Markdown table syntax.
    
- Use `$...$` for mathematical expressions inside table cells.
    
- Keep column names concise and descriptive.
    
- Align numerical columns to the right where appropriate.
    
- Do not place display equations using `$$...$$` inside table cells.
    
- Use a separate display equation below the table when a calculation needs more space.
    
- Avoid overly wide tables that are difficult to read on smaller screens.
    

## 13. Lists and Explanatory Text

Use Markdown lists to explain mathematical concepts and procedures.

**Unordered lists:**

```
- A positive weight increases the weighted sum as the input increases.
- A negative weight decreases the weighted sum as the input increases.
- A zero weight contributes nothing to the weighted sum.
```

**Ordered lists:**

```
1. Multiply each input by its corresponding weight.
2. Add the weighted inputs together.
3. Add the bias.
4. Apply the activation function.
```

### Rules

- Use numbered lists when the sequence of steps matters.
    
- Use unordered lists when presenting independent concepts or properties.
    
- Keep each list item focused on one principal idea.
    
- Explain unfamiliar mathematical notation when it first appears.
    
- Do not use mathematical expressions as a substitute for essential verbal explanations.
    

## 14. Important Results and Definitions

Use blockquotes for brief definitions or key conceptual statements when this improves readability.

**Example:**

```
> **Key idea:** Multiplication determines each input's contribution,
> while summation combines the contributions into a single score.
```

Use `\boxed{...}` to highlight important mathematical results.

**Example:**

```
$$
\boxed{v = \sum_{i=1}^{n} w_i x_i + b}
$$
```

### Rules

- Use blockquotes sparingly.
    
- Use bold text for important terminology.
    
- Reserve boxed equations for key formulas, final answers, and essential results.
    
- Avoid excessive bold text, blockquotes, or mathematical highlighting.
    

## 15. Common Formatting Errors to Avoid

Avoid the following mistakes:

### Incorrect: Using display math for ordinary prose

```
$$
\text{The neuron decides to go for a walk.}
$$
```

**Preferred:**

```
The neuron decides to go for a walk.
```

### Incorrect: Omitting braces from multi-character subscripts

```
x_10
```

**Preferred:**

```
x_{10}
```

### Incorrect: Putting a display equation inside a sentence

```
The formula is $$v = wx + b$$ and it determines the score.
```

**Preferred:**

```
The formula is:

$$
v = wx + b
$$

It determines the score.
```

### Incorrect: Using plain-text approximations of mathematical notation

```
v = sum(wi * xi) + b
```

**Preferred:**

```
$$
v = \sum_{i=1}^{n} w_i x_i + b
$$
```

### Incorrect: Using nonstandard delimiters

```
\[ v = wx + b \]
```

**Preferred for this project:**

```
$$
v = wx + b
$$
```

### Incorrect: Using HTML for ordinary mathematical formatting

```
<sub>i</sub>
```

**Preferred:**

```
x_i
```

## 16. Obsidian Compatibility Requirements

- Use standard Markdown headings and lists.
    
- Use `$...$` for inline mathematics.
    
- Use `$$...$$` for display mathematics.
    
- Use MathJax-compatible LaTeX commands.
    
- Avoid unnecessary HTML and external rendering dependencies.
    
- Ensure that equations render correctly in Obsidian Reading View and Live Preview.
    
- Keep Markdown source clean and easy to edit.
    
- Do not use LaTeX commands that require additional packages or unsupported rendering features unless explicitly requested.
    
- Prefer common environments such as `aligned`, `cases`, `bmatrix`, and `pmatrix`.
    
- Keep the source compatible with ordinary Markdown readers wherever practical, recognizing that LaTeX rendering itself requires a compatible renderer.
    

## 17. Final Validation Checklist

Before returning the formatted Markdown file, verify the following:

- The document uses valid Markdown syntax.
    
- Inline mathematical expressions use `$...$`.
    
- Display equations use `$$...$$` on separate lines.
    
- Subscripts and superscripts are correctly formatted.
    
- Mathematical operators use appropriate LaTeX commands.
    
- Multi-line calculations use appropriate alignment.
    
- Piecewise functions use the `cases` environment.
    
- Units and descriptive text are formatted correctly.
    
- Tables follow standard Markdown syntax.
    
- Equations are mathematically correct.
    
- Numerical calculations have been verified.
    
- No essential explanations or examples have been removed.
    
- The document is readable in Obsidian.
    
- The final result contains the complete Markdown content, not merely a description of the changes.
    

## 18. Primary Instruction to the AI

Whenever you create, edit, reformat, or improve a mathematical note, follow all applicable instructions in this document.

Prioritize mathematical correctness, clear explanations, consistent notation, clean Markdown, and reliable Obsidian rendering.

Preserve the author's intended meaning and level of detail. Improve the formatting without unnecessarily changing the content.

Return the complete, ready-to-use `.md` content unless the user requests a different output format.