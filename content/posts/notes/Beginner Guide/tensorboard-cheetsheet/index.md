---
title: Tensorboard Cheet Sheet (SummaryWriter)
seo_title: Tensorboard Cheet Sheet
summary: List some commonly used commands for tensorboard.
description:
slug: bg/tensorboard
author: FlammingFrost
math: false # set to true to enable KaTeX rendering

draft: false # set to false to publish
date: 2023-10-21
lastmod: 2023-10-27 # both date and lastmod will show in the post's footer

feature_image:
feature_image_alt:

categories:
  - Cheet sheet
tags:
  - Tensorboard
series: 
  - Beginner's Guide
toc: true # set to true to enable a Table of Contents
related: true # set to true to enable Related Posts section
social_share: true # set to true to enable Social Sharing buttons
newsletter: false # set to true to enable Newsletter section, at the bottom of the page
disable_comments: false # set to true to disable comments for a specific post
---

> Some commonly used commands for Tensorboard.

## Initialize the writer

### Start the Tensorboard

To start Tensorboard, run the following command in the terminal:

```bash
tensorboard --logdir=/path/to/log --port=6006
```
I always make mistake with the path, so I recommend you to use the absolute path.

The output will be like:
```bash
TensorBoard 2.5.0 at http://localhost:6006/ (Press CTRL+C to quit)
```

Or, you can start Tensorboard from Vscode.

### Initialize the writer

```python
from torch.utils.tensorboard import SummaryWriter
writer = SummaryWriter('runs/exp-1') # the result will be saved in runs/exp-1
writer = SummaryWriter() # the result will be saved in runs/Jul21-10-53-36 like format
writer = SummaryWriter(comment='exp-1') # the result will be saved in runs/Jul21-10-53-36-exp-1 like format
```

### Close the writer

After recording ALL the data, you should close the writer.

```python
writer.close()
```

## Add Log to Tensorboard

### Add scalar

The most common used of Tensorboard is to add scalar. The output will be a curve of your index, such as loss, accuracy vs epoch.

`def add_scalar(tag, scalar_value, global_step=None, walltime=None)`

```python
writer.add_scalar('train/looss', loss, epoch) # Here is an example of adding loss
writer.add_scalar('directory/like/tag', value, index) # Value is the y-axis, index is the x-axis
```

### Add image

`add_image` allows you to add image to Tensorboard. It can be used to visualize the result of your model.

`def add_image(tag, img_tensor, global_step=None, walltime=None, dataformats='CHW')`

```python
writer.add_image('image', image, index) 
# image format: torch.Tensor, numpy.ndarray
# default channel order: (Channel, Height, Width)
# if you want to change the channel order, use the following code
## with argument dataformats:
## "HWC" for (Height, Width, Channel)
## "HW" for (Height, Width)
## "CHW" for (Channel, Height, Width)
# By default, torch.Tensor -> (C,H,W), numpy.ndarray -> (H,W,C)
writer.add_image('image', image, index, dataformats='HWC') 
```
### Add histogram

`add_histogram` allows you to add histogram to Tensorboard. It can be used to visualize the distribution of your model.

`def add_histogram(tag, values, global_step=None, bins='tensorflow', walltime=None, max_bins=None)`

- values: torch.Tensor of Any shape. the histogram is computed over the flattened array. Type==(castable to float64)
- bins

```python
writer.add_histogram('histogram', values, index)
```

### Add Graph

*to be continued*

### Add Hyperparameter Tuning Result

*to be continued*

### Add Embedding

`add_embedding` allows you to add embedding to Tensorboard. It can be used to visualize the result of your model. It provides several ways to visualize the embedding, for example, PCA, t-SNE, etc.

`def add_embedding(tensor, metadata=None, label_img=None, global_step=None, tag='default')`

- tensor: torch.Tensor of shape (n_samples, n_features)
- metadata: list of labels, col1: index, col2: label
- label_img: torch.Tensor of shape (n_samples, C, H, W), this is optional

```python
features = model(images)
labels = targets
writer.add_embedding(features, metadata=labels, label_img=images)
```


## Reference

- [Tensorboard Writer (recommended)](https://pytorch.org/docs/stable/tensorboard.html)
- [Initialize Tensorboard - CSDN](https://blog.csdn.net/jinlong_xu/article/details/71124589)
- [Tensorboard Tutorial - CSDN](https://blog.csdn.net/qq_41764621/article/details/126210936)
- [Tensorboard - Github](https://github.com/tensorflow/tensorboard/blob/master/README.md)
- [Tensorboard Tutorial - Tensorflow](https://www.tensorflow.org/tensorboard/get_started)
