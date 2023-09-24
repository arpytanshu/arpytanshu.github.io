---
title: "Logistic Regression"
date: 2023-09-24T22:59:13+05:30
draft: false
math: true
ShowToc: true # To show ToC add following to page-variables
TocOpen: true # To keep Toc Open by default on a post add following to page-variables
---


## Analogy
The goal of **Linear Regression** is to model the relationship b/w the dependant variable $(y)$ and the independant variable $(x)$ using linear models.  


## Linear Models
A model is linear when it can be written in this format:
$$ Response = constant + parameter * predictor + ... + parameter * predictor $$
That is, when each term (in the model) is either a constant or the product of a parameter and a predictor variable.  
A linear model is such that the dependant variable $(y)$ is a linear function of the parameters $\beta s$, and not necessarily of the data $(x)$.

[Reference 1](https://stats.stackexchange.com/questions/8689/what-does-linear-stand-for-in-linear-regression  )  
[Reference 2](http://blog.minitab.com/blog/adventures-in-statistics/what-is-the-difference-between-linear-and-nonlinear-equations-in-regression-analysis)  
[Reference 3](https://ocw.mit.edu/courses/18-05-introduction-to-probability-and-statistics-spring-2014/resources/mit18_05s14_reading25/) (section 3 & 4)

## Modelling
The goal of **Logistic Regression** is to model the log odds of the occurence of an event to be a linear combination of the independant variables.  
$$\log (\frac{p}{1-p}) = \beta_0 + \beta_1 x_1 + ... + \beta_n x_n$$
$\therefore$ the probability of occurence of the event will be deduced as:
$$ z = beta_0 + \beta_1 x_1 + ... + \beta_n x_n $$
$$ \log (\frac{p}{1-p}) = z $$
$$ \frac{p}{1-p} = e^z $$
$$ p (1+e^z)= e^z $$
$$ p = \frac{1}{1+e^{-z}} $$

i.e. probability of occurence of the event is the sigmoid of the linear combination of the independant variables.
$$ p = \frac{1}{1+e^{-(\beta_0 + \beta_1 x_1 + ... + \beta_n x_n)}} $$

The function $S(z) = \frac{1}{1+e^{-z}}$, popularly known as the Sigmoid function, is the inverse of the Logit $(\log \frac{p}{1-p})$ and has no direct role to play in Logistic Regression. It just happens to be there, as an effect of modelling the logit.

### Bottomline:
Logistic Regression is a Linear Model, where instead of modelling a relationship between x & y, we model relationship the $xs$ and the log odds of some event.


## Negative Log Likelihood of Bernoulli

Since we are modelling the occurrence of some event with probability p, and non-occurrence with probability $(1-p)$.  
This is essentially the $Bernoulli(p)$ distribution, where:  
- event occurs i.e. $y=1$ with probability $p$.  
- event doesn't occurs i.e. $y=0$ with probability $1-p$.

i.e. the true underlying behaviour of occurence of event is a $Bernoulli(p)$ (conditional), and we want the probabilities from the model to belong to the same family of distribution. 
$\therefore$ we do a MLE for the parameter $p$ assuming the underlying distribution is $Bernoulli(p)$


The likelihood of the Binomial is the probability:
$$P(y | p) = (p)^{y_k} \cdot (1-p)^{1-y_k}$$

The Joint probability over the data samples look like as shown below. These are the product of the individual probabilities, assuming the samples were independant of wach other. This probability is the conditional Likelihood function of the Bernoulli Distribution $\because$ $p$ is a function of $\beta s$ and $xs$ 
$$P(y_1, y_2, ..., y_n | p) = P(Y | \beta , X) =  \prod_{i=1}^{n} (p)^{y_i} \cdot (1-p)^{1-y_i}$$

This conditional thing is coming from the the conditional maximum Likelihood estimator, and forms the basis of most supervised learning. $\theta_{ML} = argmax_{\theta} P(Y|X;θ)$ (ref: equn (5.62) from the DeepLearning Book.)

The corresponding negated log likelihood is: ( log is applied to prevent numerical overflow due from product of a lot of probabilities in range 0-1) 
$$- \sum_{i=1}^{n} y_i \cdot \log p + (1-y_i) \cdot \log (1-p)$$

This negated log-likelihood of the Bernoulli Distribution is popularly known as the Binary Cross Entropy Loss. 

MLE says if we minimize this negated log likelihood, (or maximize the log-likelihood) we shall end up w/ the required optimal $p$. In our case, this $p$ is a function of $\beta s$ and $xs$. i.e. we will end up with a set of optimal coefficients $\beta s$ for the linear combination of the independant variables $xs$.

