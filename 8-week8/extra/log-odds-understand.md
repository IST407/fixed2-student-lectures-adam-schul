# Understanding Log-Odds and Logit Differences in Binary Classification

Let's break down the statement: "In binary classification with softmax, we can represent the log-odds of class 1 versus class 2 as $z = z_1 - z_2$. This is because only the difference between the logits matters for the final probabilities."

## 1. Log-Odds

First, let's understand what log-odds means:
- Odds are the ratio of the probability of an event happening to the probability of it not happening.
- Log-odds are the natural logarithm of the odds.

For binary classification:
- If $p$ is the probability of class 1
- Then $(1-p)$ is the probability of class 2
- The odds of class 1 are $\frac{p}{1-p}$
- The log-odds are $\ln(\frac{p}{1-p})$

## 2. Softmax in Binary Classification

In binary classification with softmax:

$p_1 = \frac{e^{z_1}}{e^{z_1} + e^{z_2}}$ and $p_2 = \frac{e^{z_2}}{e^{z_1} + e^{z_2}}$

where $z_1$ and $z_2$ are the logits for class 1 and class 2 respectively.

## 3. Why the Difference Matters

Now, let's look at the log-odds of class 1:

$\ln(\frac{p_1}{p_2}) = \ln(\frac{e^{z_1}}{e^{z_2}}) = z_1 - z_2$

This shows that the log-odds are indeed equal to the difference between the logits.

## 4. Invariance to Constant Addition

Here's why only the difference matters:
- If we add a constant $c$ to both logits: $z_1' = z_1 + c$ and $z_2' = z_2 + c$
- The new probabilities are:

  $p_1' = \frac{e^{z_1 + c}}{e^{z_1 + c} + e^{z_2 + c}} = \frac{e^c \cdot e^{z_1}}{e^c(e^{z_1} + e^{z_2})} = \frac{e^{z_1}}{e^{z_1} + e^{z_2}} = p_1$

- The probabilities remain unchanged!

## 5. Practical Implication

This property allows us to arbitrarily set one of the logits to zero without changing the probabilities. For instance, if we set $z_2 = 0$:

$p_1 = \frac{e^{z_1}}{e^{z_1} + e^0} = \frac{e^{z_1}}{e^{z_1} + 1} = \sigma(z_1)$

This is exactly the logistic function, showing how softmax reduces to logistic regression in the binary case.

## Conclusion

The statement emphasizes that in binary classification, it's not the absolute values of the logits that determine the probabilities, but rather their difference. This difference represents the log-odds between the two classes and is sufficient to determine the probabilities of both classes.

Understanding this helps in:
1. Seeing the connection between softmax and logistic regression
2. Simplifying calculations in binary classification
3. Interpreting model outputs in terms of relative confidence between classes