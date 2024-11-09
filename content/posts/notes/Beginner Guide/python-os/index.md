---
title: Cheetsheet for Python os module
seo_title: Cheetsheet for Python os module
summary: Some useful commands for Python os module, especially IO operations and file system operations.
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
  - Python
series: 
  - Beginner's Guide
toc: true # set to true to enable a Table of Contents
related: true # set to true to enable Related Posts section
social_share: true # set to true to enable Social Sharing buttons
newsletter: false # set to true to enable Newsletter section, at the bottom of the page
disable_comments: false # set to true to disable comments for a specific post
---

## File and Directory Access
### `os.walk()`
`os.walk(directory)` returns a generator that yields a 3-tuple of the form `(dirpath, dirnames, filenames)`.
- `dirpath` is a string, the path to the directory.
- `dirnames` is a list of the names of the *subdirectories* in `dirpath`.
- `filenames` is a list of the names of the *non-directory files* in `dirpath`.

Here is an example:

Suppose we have the following directory structure:
```
├── train
│   ├── class1
│   │   ├── images
│   │   │   ├── img1.JPEG
│   │   │   ├── img2.JPEG
│   │   │   └── ...
│   │   └── class1_boxes.txt
│   ├── class2
│   │   ├── images
│   │   │   ├── img3.JPEG
│   │   │   ├── img4.JPEG
│   │   │   └── ...
│   │   └── class2_boxes.txt
│   └── ...

And we use `os.walk()` to traverse the `train` directory:
```python
import os

num_images = 0

for root, dirs, files in os.walk(self.train_dir):
    print(f"Current directory: {root}")
    print(f"Subdirectories: {dirs}")
    print(f"Files: {files}")
    for f in files:
        if f.endswith(".JPEG"):
            num_images += 1

print(f"Total number of .JPEG images: {num_images}")
```


## Solution to A unclear GPU memory occupancy
#### Problem description
I'm training a deep learning model using PyTorch, and I load the data using `DataLoader`, with `num_workers` set to a non-zero value.
The python program is stopped (killed by `kill` command), but the GPU memory is still occupied. The program is not running, but the GPU memory is not released. When we try to run the program again, we get the following error message:
```
RuntimeError: CUDA out of memory. 
```

#### Possible causes
The program starts and accerates the data loading process by using multiple processes. When the program is stopped, the processes are not terminated properly, and the GPU memory is not released. However, the multiple processes are still running in the background, and they occupy the GPU memory.
This is not a normal behavior, and it may be caused by busy resources or other reasons.

#### Solution
1. Check if the problem is caused by these data loading processes. Run the following command:
```bash
pgrep -u usrname python
```
this command will list all the processes that are running by the user `usrname` (i.e. root). If there are multiple processes that are running, they look like:
```bash
usrname  3650247 F...m python
usrname  3650310 F...m python
usrname  3650373 F...m python
usrname  3650436 F...m python
usrname  3650499 F...m python
usrname  3650562 F...m python
usrname  3650625 F...m python
usrname  3650688 F...m python
```
which corresponds to the username, process ID, and the command that is running. If you see multiple processes that are running, you can kill them by running:
```bash
pkill -u usrname -f python
```
this command will kill all the processes that are running by the user `usrname` and the command is `python`. Be careful when you run this command, as it will kill all python processes, including the others that are running in the background. So make sure you only kill the processes that are not needed.
