---
title: Debugging Python with pdb
seo_title: Debugging Python with pdb
summary: Use pdb to debug python code. Cheat sheet.
description:
slug: bg/pdb
author: FlammingFrost
math: false # set to true to enable KaTeX rendering

draft: false # set to false to publish
date: 2023-10-27
lastmod: 2023-10-27 # both date and lastmod will show in the post's footer

feature_image:
feature_image_alt:

categories:
  - Cheet sheet
tags:
  - python
series: 
  - Beginner's Guide
toc: true # set to true to enable a Table of Contents
related: true # set to true to enable Related Posts section
social_share: true # set to true to enable Social Sharing buttons
newsletter: false # set to true to enable Newsletter section, at the bottom of the page
disable_comments: false # set to true to disable comments for a specific post
---

> Cheat sheet for debugging python code with pdb.

## Start pdb

```python
import pdb
pdb.set_trace()
```

This command will create a breakpoint in your code. When the code reaches this point, it will stop and you will be able to debug it. The cmd line will look like this:

```bash
(Pdb) # here you can type commands, or check the value of variables
```

## pdb commands

### Check the source code

```bash
(Pdb) l # list 11 lines of code around the current line
```

```bash
(Pdb) ll # list the whole function
```

### Step next

| Command | Description |
| --- | --- |
| `n` | step next (will not go into functions) |
| `s` | step into (will go into functions) |
| `r` | step out (will go out of functions) |

### Check variables

```bash
(Pdb) p <variable> # print the value of a variable
```

Actually, you can use any python code here, for example:

```bash
(Pdb) p [x for x in range(10)] # print a list
```

`p` is not necessary, you can just type the code and it will be executed.

### Other commands

| Command | Description |
| --- | --- |
| `c` | continue execution (will stop at the next breakpoint)
| `q` | quit the debugger (will stop the execution) |
| `a` | print the argument list of the current function |
| `whatis <variable>` | print the type of a variable |

## References

- [Python pdb - Zhihu](https://zhuanlan.zhihu.com/p/37294138)
