---
layout: post
title: "Cost Function"
date: 2020-02-08 16:00:00 +0800
tags: [machine-learning, data-science]
# img: "/assets/img/machine.jpg"
# description:
---
# Cost Function Intuition
### Single Variable
Let h<sub>&theta;</sub>(x) be the hypothesis which predicts the value of target Y

h<sub>&theta;</sub>(x) = &theta;<sub>o</sub> + &theta;<sub>1</sub>x

Our goal is to choose &theta;<sub>o</sub> and &theta;<sub>1</sub> such that the error between h<sub>&theta;</sub>(x) and the actual target Y is minimized. Intuitively, the function of **Mean Square Error** comes to mind.

Below is the cost function J(&theta;), where **_m_** is the number of training set:

![oneval-cost-func](/blog/assets/img/oneval-cost-func.png)

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

x | y
:--|:--
9 | 50
0 | -10
-10 | -34

J(&theta;) = ![cost-function.png](/assets/img/cost-function.png)

Example, if we let &theta;<sub>1</sub> = 2,

J(&theta;<sub>1</sub>) = [ (9 * &theta;<sub>1</sub> - 50)<sup>2</sup> + (0 * &theta;<sub>1</sub> - (-10))<sup>2</sup> + ((-10) * &theta;<sub>1</sub> - (-34))<sup>2</sup> ] / 6 = 220

Below is the visualization of &theta; and J(&theta;), when &theta; is from [0, 7.8] with 0.2 increament:
![cost-fun-visual.png](/assets/img/cost-fun-visual.png)


# Normalization Function


# Gradient Decent vs Normalization Function


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



![vector-form](/assets/img/vector-form.png)