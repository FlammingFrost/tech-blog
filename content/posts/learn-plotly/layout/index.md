---
title: Layout Setting for Plotly
seo_title: Layout Setting for Plotly
summary: Canva size, axis, inset, multi-plot, and more
description:
slug: plotly/layout
author: FlammingFrost
math: false # set to true to enable KaTeX rendering

draft: false # set to false to publish
date: 2024-11-14
lastmod: 2024-11-14

feature_image:
feature_image_alt:

categories:
  - Plotly
tags:
  - Visualization
series: 
  - Plotly Learning Log
toc: true # set to true to enable a Table of Contents
related: true # set to true to enable Related Posts section
social_share: true # set to true to enable Social Sharing buttons
newsletter: false # set to true to enable Newsletter section, at the bottom of the page
disable_comments: false # set to true to disable comments for a specific post
---

## Table of Contents
- [Table of Contents](#table-of-contents)
- [Overview](#overview)
- [Canva Size](#canva-size)
- [Plot in specific area](#plot-in-specific-area)
- [Code Example](#code-example)
  - [Canva Size (Example)](#canva-size-example)
  - [Plot in specific area (Example)](#plot-in-specific-area-example)
- [View My Interactive Chart](#view-my-interactive-chart)

## Overview
This post talks about the layout setting for Plotly. Specifically, the layout setting can be evoked by

```python
layout = go.Layout(**kwargs)
fig = go.Figure(data=data, layout=layout)
# i.e. plot(fig)
```
where `**kwargs` is a series of settings.

## Canva Size
The canva size can be set by:
- `width`. In pixels (e.g. `width=800`)
- `height`. In pixels (e.g. `height=600`)
- `autosize`. A boolean. If `True`, the canva will be resized automatically to fit dimensions that are not explicitly set.
- `margin`. A dictionary with keys `l`, `r`, `t`, `b`, `pad` (e.g. `margin=dict(l=20, r=20, t=20, b=20, pad=4)`)

[Example](#canva-size-example)

## Plot in specific area
This can be combined to create multiple plots of different sizes in the same figure.

In `trace`, the `xaxis` and `yaxis` can be set to `x1`, `x2` ("x" + integer) and `y1`, `y2` ("y" + integer) to specify the plot area.

In `layout`, set a group of `xaxis` and `yaxis` to match those in `trace`. Specifically,

| `trace` | `layout` |
| --- | --- |
| `xaxis1` or `xaxis` | `x1` or `x` |
| `xaxis2` | `x2` |
| `xaxisN` | `xN` |
| Similar for `yaxis` | Similar for `y``

In `layout` these axis should be **anchor**ed to its counterpart in `trace` by `domain` like

```python
trace = go.Scatter(
    ...
    xaxis='x2',
    yaxis='y2'
)
layout = go.Layout(
    xaxis2=dict(
        domain=[0.6, 1],
        anchor='y2' # Note that it is 'y2' not 'x2'
    ),
    yaxis2=dict(
        domain=[0.6, 1],
        anchor='x2' # Note that it is 'x2' not 'y2'
    )
)
```

[Example](#plot-in-specific-area)




## Code Example

### Canva Size (Example)

```python
layout = go.Layout(
    height=2000,
    autosize=True,
    margin=dict(l=20, r=20, t=20, b=20, pad=4)
)
```

This should enable a canvas that has fixed height and variable width. (e.g. Zooming out in browser -> both dim pixels increase -> (But height pixels fixed) Plot are "longers")

### Plot in specific area (Example)

```python
trace1 = go.Scatter(
    x=[1, 2, 3],
    y=[4, 5, 6],
    xaxis='x1',
    yaxis='y1'
)
trace2 = go.Scatter(
    x=[1, 2, 3],
    y=[4, 5, 6],
    xaxis='x2',
    yaxis='y2'
)
layout = go.Layout(
    xaxis1=dict(
        domain=[0, 0.5],
        anchor='y1'
    ),
    yaxis1=dict(
        domain=[0, 0.5],
        anchor='x1'
    ),
    xaxis2=dict(
        domain=[0.5, 1],
        anchor='y2'
    ),
    yaxis2=dict(
        domain=[0.5, 1],
        anchor='x2'
    )
)
```

## View My Interactive Chart

<iframe src="plot/testplot.html" width="800" height="600" style="border:none;"></iframe>

ddsfs

[Click here to view the chart](plots/testplot.html)
