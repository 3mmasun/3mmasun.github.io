---
layout: post
title: "Logistic Regression"
date: 2020-02-13 15:00:00 +0800
tags: [machine-learning, Classification]
# img: "/assets/img/machine.jpg"
description: Basics of logistic regression
---

Logistic Regression is a classification problem whose target / output is a set of discrete values.

# Binary Classification

In binary classification, the output of Y has only two values, usually 0 and 1.

- 0: the negative case, absence of the observed outcome
- 1: the positive case, the presence of the intended outcome

Logistic function of binary classification is call **Sigmoid Function**, its charateristic includes:

- x ranges from +∞ to -∞
- y ranges from 0 to 1
- 'S' shaped

![sigmoid](/assets/img/sigmoid.png)

## Logistic Function Equation

#### h<sub>&theta;</sub>(x) = g(&theta;<sup>T</sup>x) = 1 / (1 - e<sup>-&theta;<sup>T</sup>x</sup>) when g(z) = 1 / (1 - e<sup>-z</sup>)

h<sub>&theta;</sub>(x) = P(y=1\|x;&theta;) = 1 - P(y=0\|x;&theta;), in other words, h<sub>&theta;</sub>(x) will give us the probability that our output is 1.

P(y=1\|x;&theta;) + P(y=0\|x;&theta;) = 1

## Translate probability to discrete values

Assume this is how we will translate the P into 0 and 1:

- y = 1 if h<sub>&theta;</sub>(x) >= 0.5
- y = 0 if h<sub>&theta;</sub>(x) < 0.5

Since h<sub>&theta;</sub>(x) = g(&theta;<sup>T</sup>x), for h<sub>&theta;</sub>(x) >= 0.5 means &theta;<sup>T</sup>x >= 0, thus:

- y = 1 if &theta;<sup>T</sup>x >= 0
- y = 0 if &theta;<sup>T</sup>x < 0

Solving the equation we get the **Decision Boundary**

### Decision Boundary is not a property of the data set, but a property of the hypothesis and parameters.

## Cost Function

The original sigmoid function is non-linear thus will not have global minimum. Log function solves the problem.

![logistic-cost](/assets/img/logistic-cost.png)

### Intuition

If we correctly predict the outcome, then the cost will nearly 0

If we wrongly predict the outcome, the cost will be close to infinity

|                         If y=1                          |                         If y=0                          |
| :-----------------------------------------------------: | :-----------------------------------------------------: |
| ![logistic-cost-pos](/assets/img/logistic-cost-pos.png) | ![logistic-cost-neg](/assets/img/logistic-cost-neg.png) |

### Gradient Decent for Cost Function of Logistic Regression

![logistic-gd](/assets/img/logistic-gd.png)

Reference: [Machine Learning by Andrew](https://www.coursera.org/learn/machine-learning/supplement/bgEt4/cost-function)
