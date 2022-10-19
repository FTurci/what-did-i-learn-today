---
title: Logistic regression and bias
created: '2022-10-05T13:42:32.512Z'
modified: '2022-10-05T14:17:56.097Z'
---

# Logistic regression and bias

In a simple binary logistic regression model we have a binary dependent variable $Y$ modelled by a constant plus a binary regressor $x$, so that the logistic cumulative distribution function $\Lambda(u)=[1+exp\{-u\}]$ models the probability



$Pr(Y_i = 1 | x_1 =1) = \Lambda (\alpha+\beta x_i)$

Since the logit is the inverse of th logistic function, we have that


$\ln \left(\dfrac{Pr(Y_i = 1 | x_1 =1)}{1-Pr(Y_i = 1 | x_1 =1)}\right)=\alpha+\beta x_i$

Imagine we have a sample of $n$ observations with $n_1$ for $x_i=1$ and $n_0$ for $x_i=0$ with $n_1+n_0=n$

then

$P_{1|1}=\frac{1}{n_1}\sum_{x_i=1}y_i$

$P_{1|0}=\frac{1}{n_0}\sum_{x_i=0}y_i$
