---
layout: post
title: "Machine Learning"
date: 2020-02-03 16:00:00 +0300
tags: [machine-learning, data-science]
---

## What is Machine Learning (ML)?

Machines as we know, are good at computation. In terms of computation, there are 3 elements involved:

- Input
- Function
- Output

Typically, computation applies a **given function** on **given input**, and return some kind of **output**. However in Machine Learning, **Input and Output are given**, and the job of the machine is to figure out the **Function** which describes the relationship between them, also known as **model**, or **_h_** for **_hypothesis_**

## Are all Machine Learning the same?

NO. There are mainly 2 types of Machine Learning:
- Supervised-learning
- Unsupervised-learning

### More on supervised-learning
In supervised-learning, input and output are provided. The job is to figure out the relationship between them.
Supervised-learning can be futher categorized into Regression problem and Classification problem.

#### Regression
When the output is a continous number. Eg:

- predicting price of the house
- predicting a person's income by certain age

#### Classification
when the output is discrete, we can think of them as categories. Eg:

- classify the spam emails
- determine whether a person has diabetes

Sometimes, the result of regression problem can be used to solve a classification problem. Eg, given the predicted price of the house, whether one could sell it successfully. That's also known as **Logistic Regression**

### More on unsupervised-learning

In unsupervised-learning, only a set of inputs are given. There is no output.
The goal is usually finding clusters or groups that are closely related given certain inputs. Eg:

- given 10000 articles, put them into groups with similar topics
