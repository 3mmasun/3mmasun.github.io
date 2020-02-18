---
layout: post
title: "Metrics used to evaluate a classifier"
date: 2020-02-13 15:00:00 +0800
tags: [machine-learning, data-science]
# img: "/assets/img/machine.jpg"
description: Explore the ways a classifier can be evaluated
---

# Terms and Metrics

## Accuracy

Among _all predictions_, how many did we get it right?

> Accuracy = (TP+TN) / ( TP+TN+FP+FN )

## Precision

Among all the POSTIVE predictions, how many are correct?

> Precision = TP / ( TP+ NP )

## Recall (aka Sensitivity, aka True Postive Rate)

Among all POSITIVE samples, how many did we get it right?

> Recall = TP / ( TP+FN )

None of the scores alone can determine how good a model performs. There is always a trade off between precision and recall.

![recall-over-precision](/assets/img/recall-vs-precision.png)

### When do we prefer high precision?

When we cannot affort to miss out any positive cases. Eg, detecting whether a video is safe for children.

Another way of thinking is that, we are more _reluctant_ to label things as POSITIVE

### When do we prefer high recall?

When we can affort some mistakes in our predictions for TRUE cases. Eg, video that detects shoplifters, we rather to have some false alarms than to miss out any potential shoplifters.

Another way of thinking is that, we are more _willing_ to label things as POSITIVE

## F1 score

The harmonic mean of Precision and Recall.
It's a score that can tell you how both Precision and Recall are doing.

![F1](/assets/img/F1.png)

A harmonic mean give much more weight to a low value, here is why:

- (1 / precision) ranges from 0 to 1, same for (1 / recall)
- high _precision_ of nearly 0.99 could mean that recall might fall below 0.1
- if recall is 0.1, then (1 / recall) become very large, and thus the entire F1 score becomes small

### When do we get high F1 score?

When both recall and precision are high!
Thus, F1 is a better evaluation simply because the score tell how both recall and precision are doing.

## ROC - AUC

Receiver operating characteristic (ROC) curve is ploting TPR (TruePositiveRate) against FPR (FalsePostiveRate).

> FPR (aka Specificty) = 1 - TrueNegativeRate = 1 - [ TN / (TN + FP) ]

A perfect classifier would have the Area Under Curve (AUC) equal to 1 whereas a random classifier would have AUC equal to 0.5

![roc-auc](/assets/img/roc-auc.png)
