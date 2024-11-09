---
title: Loss Functions
seo_title: Loss Functions
summary: "Loss Functions define what a model learns. Different loss casts different focus on the model's learning process."
description:
slug: ML-intro/loss
author: FlammingFrost
math: true # set to true to enable KaTeX rendering

draft: true # set to false to publish
date: 2023-08-22
lastmod: 2023-08-22 # both date and lastmod will show in the post's footer

feature_image:
feature_image_alt:

categories:
  - Machine Learning
  - Tutorial

tags:
  - ML
  - Basic
series: 
  - Machine Learning Intro

toc: true # set to true to enable a Table of Contents
related: true # set to true to enable Related Posts section
social_share: true # set to true to enable Social Sharing buttons
newsletter: false # set to true to enable Newsletter section, at the bottom of the page
disable_comments: false # set to true to disable comments for a specific post
---

# Introduction to Loss Functions
Here lists some common loss functions used in machine learning. Loss functions define what a model learns. Different loss casts different focus on the model's learning process. This post will give the mathematical definition of these loss functions and their applications.

*Tips: You can browse the table of content on your right side*

## $L_2$ Loss
$L_2$ loss is he most common loss function used in regression problems. It is simple and differentiable. It is defined as:
$$
L_2 = \frac{1}{2} \sum_{i=1}^{n} (y_i - \hat{y_i})^2
$$
where $y_i$ is the ground truth and $\hat{y_i}$ is the prediction. The $\frac{1}{2}$ is used to make the derivative of the loss function simpler.

Note that $L_2$ loss is a comparison between two scalars, for example, your predicted price and ground truth. 

However, it can make no sense to compare two vectors, even you add them up (because the scales can be different). In this case, though the property "lower is better" still be kept, it's hard to interpret the meaning of loss. A more proper way is to weight the loss of each component, if they have different meanings, in the form like:
$$
L_2=\frac{1}{2} \sum_{d}^D w_d \cdot L_d
$$

## Cross-entroyp

## KL (Kullback-Leibler) divergence

