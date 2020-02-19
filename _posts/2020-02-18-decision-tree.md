---
layout: post
title: "Decision Tree"
date: 2020-02-14 15:00:00 +0800
tags: [machine-learning, classification]
# img: "/assets/img/machine.jpg"
description: Explore the ways a classifier can be evaluated
---

# What is Decision Tree

Decision Tree is like a flow chart, at the top the tree there is a _ROOT_, where things start. At the bottom there are leaves.
Below is a visualization of a Decision Tree.

![max depth 3](/assets/img/heart-3d.png)

## Gini impurity

The Gini impurity score tells how well the criteria splits the instances.

- G<sub>i</sub> = 0.49 means it does not separate the training instances very well
- G<sub>i</sub> = 0.0 means it separates the training instances perfectly

![gini](/assets/img/gini.png)

## How Decision Tree works?

1. calculate gini impurity for each feature, using all the records availabe
2. select feature with lowest gini impurity as the root
3. repeat step 1-2 for each node until

- no more records
- further seperation increases gini score
- stop criteria met

### Data preparation

- Feature Scaling: Because Decision Tree looks at individual feature at a time, there is generally no need for feature scaling
- Feature Imputation
  - categorical: pick majority, predict using another high correlation column
  - numerical: mean or medium

# Overfitting issue in DT

Below is a decision tree build with no restriction. Clearly the second tree is having an over fitting problem.

![no restriction](/assets/img/heart-no-res.png)

A few way to overcome this:

- min sample leaves
- max depth: how deep the decision tree will be

# Code Example
[kaggle Heart Disease Dataset](https://www.kaggle.com/johnsmith88/heart-disease-dataset)

```python
# training decision tree
from sklearn.tree import DecisionTreeClassifier
tree_clf = DecisionTreeClassifier(max_depth=5, min_samples_leaf=2)
tree_clf.fit(x_train, y_train)
```

```python
# confusion metrix
from sklearn.metrics import confusion_matrix
from sklearn.metrics import plot_confusion_matrix
fig, ax=plt.subplots(figsize=(15,10))
plot_confusion_matrix(tree_clf_3d, x_test, y_test, ax=ax)
```

![confusion-dt](/assets/img/confusion-dt.png)

```python
# other score
from sklearn.metrics import confusion_matrix
from sklearn.metrics import plot_confusion_matrix
fig, ax=plt.subplots(figsize=(15,10))
plot_confusion_matrix(tree_clf_3d, x_test, y_test, ax=ax)

# output
#               precision    recall  f1-score   support
#
#            0       0.81      0.90      0.85        29
#            1       0.90      0.81      0.85        32
#
#     accuracy                           0.85        61
#    macro avg       0.85      0.85      0.85        61
# weighted avg       0.86      0.85      0.85        61
```

```python
# roc curve
from sklearn.metrics import roc_auc_score, roc_curve
roc_score=roc_auc_score(y_test, y_pred)
fpr,tpr,thresholds = roc_curve(y_test, tree_clf_3d.predict_proba(x_test)[:,1])
plt.plot([0,1], [0,1], "red")
plt.plot(fpr, tpr)
```

![roc-dt](/assets/img/roc-dt.png)
