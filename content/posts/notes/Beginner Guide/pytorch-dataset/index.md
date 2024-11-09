---
title: Customize your PyTorch Dataset
seo_title: Customize your PyTorch Dataset
summary: A guide to customize your PyTorch Dataset. This is the first step for your PyTorch project.
description:
slug: bg/pytorch-dataset
author: FlammingFrost
math: false # set to true to enable KaTeX rendering

draft: false # set to false to publish
date: 2024-03-06
lastmod: 2023-10-28 # both date and lastmod will show in the post's footer

feature_image:
feature_image_alt:

categories:
  - Cheet sheet
tags:
  - PyTorch
series: 
  - Beginner's Guide
toc: true # set to true to enable a Table of Contents
related: true # set to true to enable Related Posts section
social_share: true # set to true to enable Social Sharing buttons
newsletter: false # set to true to enable Newsletter section, at the bottom of the page
disable_comments: false # set to true to disable comments for a specific post
---

> When I want to test my model on my own dataset, I always need to write a series of codes to preprocess, load, and transform the data. To work with PyTorch, I need to write a class that inherits from `torch.utils.data.Dataset` and implement the `__len__` and `__getitem__` methods. This is the first step for your PyTorch project. In this post, I will show you how to customize your PyTorch Dataset.

## Introduction
In Pytorch, a batch of data is sample from a `dataloader` in every iteration. The `dataloader` is a Python iterator that allows your models to load data in parallel. 

A `dataloader` is created by passing a `Dataset` object to the `torch.utils.data.DataLoader` class. The `Dataset` object can be **map-style** or **iterable-style** (I haven't used the latter yet). The construction of a map-style dataset always involves specifying the path of the data and the labels. The loading of the data (i.e., images, text, etc.) and the transformation of the data are done in the acquisition of the data.

Technically, all you need to do is implement the `__len__` and `__getitem__` methods in your `Dataset` class. The `__len__` method returns the size of the dataset, and the `__getitem__` method returns a sample from the dataset at a given index. 