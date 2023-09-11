---
layout: post
title: "Linear Regression"
date: 2020-02-08 16:00:00 +0800
tags: [machine-learning, regression]
---

# Linear Regression - Cost Function Intuition

### Single Variable

Let h<sub>&theta;</sub>(x) be the hypothesis which predicts the value of target Y

h<sub>&theta;</sub>(x) = &theta;<sub>o</sub> + &theta;<sub>1</sub>x

Our goal is to choose &theta;<sub>o</sub> and &theta;<sub>1</sub> such that the error between h<sub>&theta;</sub>(x) and the actual target Y is minimized. Intuitively, the function of **Mean Square Error** comes to mind.

Below is the cost function J(&theta;), where **_m_** is the number of training set:

![oneval-cost-func](/assets/img/oneval-cost-func.png)

### Multiple Variable

Applying this to a more general problem with multi-variables:

h<sub>&theta;</sub>(x) = &theta;<sub>o</sub> + &theta;<sub>1</sub>x<sub>1</sub> + &theta;<sub>2</sub>x<sub>2</sub> +...+ &theta;<sub>n</sub>x<sub>n</sub> = &theta;<sup>T</sup>x

where

- &theta;<sup>T</sup>x is 1 by (n+1) vector
- x is (n+1) by 1 vector
- x<sub>o</sub> = 1

![vector-form](/assets/img/vector-form.png)

# Gradient Decent Intuition

Gradient Decent is the method used to find &theta; such that the cost function J(&theta;) is minimized.
The intuition can be understood using a simplied version of h(&theta;)

Assume h<sub>&theta;</sub>(x) = &theta;<sub>1</sub>x and we have following 3 data sets:

| x   | y   |
| :-- | :-- |
| 9   | 50  |
| 0   | -10 |
| -10 | -34 |

J(&theta;) = ![cost-function.png](/assets/img/cost-function.png)

Example, if we let &theta;<sub>1</sub> = 2,

J(&theta;<sub>1</sub>) = [ (9 * &theta;<sub>1</sub> - 50)<sup>2</sup> + (0 * &theta;<sub>1</sub> - (-10))<sup>2</sup> + ((-10) * &theta;<sub>1</sub> - (-34))<sup>2</sup> ] / 6 = 220

Below is the visualization of &theta; and J(&theta;), when &theta; is from [0, 7.8] with 0.2 increament:
![cost-fun-visual.png](/assets/img/cost-fun-visual.png)

Such graph indicates that the cost function is a **convex function** which means it's a single bowl shape with global minimum. This is a nice feature which means no matter where we initialize the values of parameters &theta;, gradient decent with appropriate learning rate (&alpha;) will always converge and reach the global minimu.

# Gradient Decent Algorithm

Reference taken from [Andrew Ng's ML Course on Coursera](https://www.coursera.org/learn/machine-learning/)
Here is the formal equation of Gradient Decent, using **Batch Gradient Decent**

![gradient-decent.png](/assets/img/gradient-decent.png)

Key points:

- x<sup>(i)</sup> is the ith row from the training set
- x<sub>j</sub> is jth feature (column), and x<sub>0</sub> is 1
- &alpha; is the learning rate, how big each step is

### about &alpha;

If &alpha; is too small, gradient decent takes long time and many iterations to converge.
If &alpha; is too big, gradient decent will overshoot the global minimum and fail to converge.
To know if &alpha; is good, typically one could plot J(&theta;) as function of number of iteration.
The value of J(&theta;) should decrease quickly and evetually flattern

# Normal Equation

Instead of taking many iterations, normal equation is able to solve the value of &theta;<sup>T</sup> in a single step.
&theta; = (X<sup>T</sup>X)<sup>-1</sup>X<sup>T</sup>y

- X<sup>-1</sup> is the inverse of matrix X
- y is the target

# Gradient Decent vs Normal Equation

Normal Equation does not require any iteration, nor does it require one to choose the learning rate &alpha;

However, the cost of the Normal Equation is O(n<sup>3</sup>) where n is the number of features, while gradient decent is O(kn<sup>2</sup>)Thus, when data set has huge number of features, eg 10000, it's too costly to solve by normalization function. Instead, gradient decent would still be able to solve in reasonable amount of time.

# Factors that speed-up G.D!

gradient decent works best when all feature are in the same range:

- between [-1, 1] or,
- between [-0.5, 0.5]

Two techniques can be used:

- feature scaling:
- mean normalization

![feature-scaling](/assets/img/feature-scaling.png)

Where μi is the average
si is the range or standard deviation
