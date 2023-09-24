---
title: "Quotes"
date: 2023-09-10T19:06:41+05:30
draft: true
math: true
---

### *Maximum Likelihood Estimation:*
- The Maximum Likelihood Estimate for the parameter $\theta$ is the value of $\theta$ for which the data is most likely.  
- $likelihood = f({x_1, ..., x_n}|\theta)$
- MLE gives point estimates, since it gives  single value for the unknown parameter.

Process:

- If we have data consisting of values $x_1, x_2, ..., x_n$ drawn from some  distribution, parameterised by $\alpha, \beta$. The question remains: **The distribution corresponding to which $\alpha, \beta$?**
- Each $X_i$ has pdf $f_{X_i}(x_i)$
- Assuming the data points are independant, writing the *joint pdf* is the product of the individual densities:  
$f_{X_i}(x_1, x_2, ..., x_n | \alpha, \beta) = f_{X_i}(x_1) \; f_{X_i}(x_2)\;...\;f_{X_i}(x_n) $  
Writing the joint pdf as a consitional density, since it depends on $\alpha, \beta$. Viewing the data as fixed, and $\alpha, \beta$ as variable, this density is the likelihood function.
- Typically, you would take a log of this likelihood, to avoid numerical overflow due to product of n components which are all in (0, 1). You get the log likelihood function.
- The MLE is the value of $\alpha, \beta$ for which the log likelihood is maximized. Using partial derivatives since we have 2 parameters.  
$\frac{\partial f_{X_i}(x_1, x_2, ..., x_n | \alpha, \beta)}{\partial \alpha} = 0$, 
$\frac{\partial f_{X_i}(x_1, x_2, ..., x_n | \alpha, \beta)}{\partial \beta} = 0$

Nitty Gritty:

- For continuous distributions, the pdf gives the densities. The true probabilities are given by multiplying w/ $dx$: 
$P(X_1, X_2 | \theta) = f_{X_1}(x_1 | \theta)dx_1 \cdot f_{X_2}(x_2 | \theta)dx_2$  
We find that the factors $dx_1, dx_2$ play no role in finding the maximum. So for the MLE we drop it and simply call the density the likelihood: $likelihood = f(x_1, x_2 | \theta)$
