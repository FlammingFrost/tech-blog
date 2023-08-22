---
title: How to Evaluate the Performance of ML Models
seo_title: How to Evaluate the Performance of ML Models
summary: "Maching learning basically have 2 tasks: regression and classification. This post will introduce how to evaluate the performance of ML models in these 2 tasks."
description:
slug: ML-intro/evaluate
author: FlammingFrost
math: true # set to true to enable KaTeX rendering

draft: true # set to false to publish
date: 2023-08-22
lastmod: 2023-08-22 # both date and lastmod will show in the post's footer

feature_image:
feature_image_alt:

categories:
  - ML
  - Tutorial

tags:
  - Machine Learning
  - Basic Concepts
series: 
  - Machine Learning Intro

toc: true # set to true to enable a Table of Contents
related: true # set to true to enable Related Posts section
social_share: true # set to true to enable Social Sharing buttons
newsletter: false # set to true to enable Newsletter section, at the bottom of the page
disable_comments: false # set to true to disable comments for a specific post
---

# How to Evaluate the Performance of ML Models
 Machine learning basically have 2 tasks: regression and classification. This post will introduce how to evaluate the performance of ML models in these 2 tasks.

## Regression
**Preliminary concepts:**

In regression, model predictions are continuous values. Usually, $y\in\mathbb{R}$.

> Notation: $y_i$ is the actual value of the $i$th sample, $\hat{y_i}$ is the predicted value of the $i$th sample, $n$ is the number of samples.
### Mean Squared Error (MSE) and Root Mean Squared Error (RMSE)
MSE is the arithmetic mean of the squares of the errors.
$$
MSE = \frac{1}{n}\sum_{i=1}^{n}(y_i-\hat{y_i})^2
$$
RMSE is the square root version of MSE. It is the standard deviation of the residuals (prediction errors).
$$
RMSE = \sqrt{MSE}
$$
### Mean Absolute Error (MAE)
MAE is the average of the absolute differences between predictions and actual values.
$$
MAE = \frac{1}{n}\sum_{i=1}^{n}|y_i-\hat{y_i}|
$$
### Mean Absolute Percentage Error (MAPE)
MAPE is the average of the absolute percentage difference between predictions and actual values.
$$
MAPE = \frac{1}{n}\sum_{i=1}^{n}\frac{|y_i-\hat{y_i}|}{y_i}
$$
It can be sensitive to outliers.

## Classification
**Preliminary concepts:**

Test set are supposed to have limited and known labels, said $y_i\in\mathbb{C}$, where $\mathbb{C}$ is the set of all possible labels.

> Notation: $y_i$ is the actual label of the $i$th sample, $\hat{y_i}$ is the predicted label of the $i$th sample, $n$ is the number of samples.

### TP, TN, FP and FN
TP, TN, FP and FN classify the predictions into 4 categories for a binary classification problem.
- TP: True Positive, the number of positive samples that are correctly predicted as positive.
$$
TP = \frac{N(\text{Pred Positive}\cap\text{Actual Positive})}{N(\text{Actual Positive})}
$$
- TN: True Negative, the number of negative samples that are correctly predicted as negative.
$$
TN = \frac{N(\text{Pred Negative}\cap\text{Actual Negative})}{N(\text{Actual Negative})}
$$
- FP: False Positive, the number of negative samples that are incorrectly predicted as positive.
$$
FP = \frac{N(\text{Pred Positive}\cap\text{Actual Negative})}{N(\text{Actual Negative})}
$$
- FN: False Negative, the number of positive samples that are incorrectly predicted as negative.
$$
FN = \frac{N(\text{Pred Negative}\cap\text{Actual Positive})}{N(\text{Actual Positive})}
$$

The relationship between TP, TN, FP and FN is shown in the following table.

|  | Actual Positive | Actual Negative |
| -------- | -------- | -------- |
| Pred Positive | TP | FP |
| Pred Negative | FN | TN |

### Accuracy
Accuracy is the proportion of correct predictions among all predictions.
$$
Accuracy = \begin{cases}
\frac{TP+TN}{TP+TN+FP+FN} & \text{Binary Classification}\\\\\\\\
\frac{\sum_{i=1}^{n}I(y_i=\hat{y_i})}{n} & \text{Multi-class Classification}
\end{cases}
$$

### Precision
Precision is the proportion of correct positive predictions among all positive predictions.
$$
Precision = \frac{TP}{TP+FP}
$$
In multi-class classification, precision is calculated for each class. The average of all classes' precision is the precision of the model.

### Recall
Recall is the proportion of correct positive predictions among all actual positive samples.
$$
Recall = \frac{TP}{TP+FN}
$$
Multi-class classification takes the average.

### F1 Score
F1 score is the harmonic mean of precision and recall.
$$
F1 = \frac{2}{\frac{1}{Precision}+\frac{1}{Recall}} = \frac{2\times Precision\times Recall}{Precision+Recall}
$$
F1 score considers both precision and recall. It is a better metric than accuracy when the dataset is **imbalanced**.

---

### Top-k Accuracy
In classification, the model is supposed to predict possibilities, or scores, for each class. Top-k accuracy means that if the true label is in the top-k predicted labels, the prediction is correct.