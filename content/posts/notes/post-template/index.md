---
title: Post Template
seo_title: Post Template
summary: Summary shown on the post list.
description: A brief guide to post template. # not sure about the usage
slug: post-template
author: FlammingFrost
math: true # set to true to enable KaTeX rendering

draft: false # set to false to publish
date: 2020-11-16T21:21:46-05:00
lastmod: 2023-11-16 # both date and lastmod will show in the post's footer

feature_image: "ai.jpg"
feature_image_alt: "Artificial Intelligence"

categories:
  - Math
  - Templates
tags:
  - Markdown
  - Figures
  - Math
series: 
  - Templates

toc: true # set to true to enable a Table of Contents
related: true # set to true to enable Related Posts section
social_share: true # set to true to enable Social Sharing buttons
newsletter: false # set to true to enable Newsletter section, at the bottom of the page
disable_comments: false # set to true to disable comments for a specific post
---

Mathematical notation in a Hugo project can be enabled by using third party JavaScript libraries.

In this example we will be using [KaTeX](https://katex.org/).

- Create a partial under `/layouts/partials/math.html`.
- Within this partial reference the [Auto-render Extension](https://katex.org/docs/autorender.html) or host these scripts locally.
- Include the partial in your templates like so:  

```go-html-template
{{ if or .Params.math .Site.Params.math }}
{{ partial "math.html" . }}
{{ end }}
```

- To enable KaTex globally set the parameter `math` to `true` in a project's configuration.
- To enable KaTex on a per page basis include the parameter `math: true` in content files.

**Note:** Use the online reference of [Supported TeX Functions](https://katex.org/docs/supported.html)

<!-- {{< math.inline >}}
{{ if or .Page.Params.math .Site.Params.math }} -->
<!-- KaTeX -->
<!-- <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/katex.min.css" integrity="sha384-zB1R0rpPzHqg7Kpt0Aljp8JPLqbXI3bhnPWROx27a9N0Ll6ZP/+DiW/UqRcLbRjq" crossorigin="anonymous">
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/katex.min.js" integrity="sha384-y23I5Q6l+B6vatafAwxRu/0oK/79VlbSz7Q9aiSZUvyWYIYsd+qj+o24G5ZU2zJz" crossorigin="anonymous"></script>
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/contrib/auto-render.min.js" integrity="sha384-kWPLUVMOks5AQFrykwIup5lo0m3iMkkHrD0uJ4H5cjeGihAutqP0yW0J6dpFiVkI" crossorigin="anonymous" onload="renderMathInElement(document.body);"></script>
{{ end }}
{{</ math.inline >}} -->

# Markdown Syntax
# H1
## H2
### H3
#### H4
##### H5
###### H6

## Emphasis

`*italic*` *italic*

`_italic_` _italic_

`**bold**` **bold**

`__bold__` __bold__

`~~strikethrough~~` ~~strikethrough~~

## Lists

### Unordered

`* Item 1` * Item 1
`* Item 2` * Item 2
`* Item 3` * Item 3

### Ordered

`1. Item 1` 1. Item 1
`2. Item 2` 2. Item 2
`3. Item 3` 3. Item 3

## Links

`[Link](https://example.com)` [Link](https://example.com)

`[Link with title](https://example.com "Example Title")` [Link with title](https://example.com "Example Title")

## Images

`![Image](image.jpg)` 

![Image](ai.jpg)

`![Image with title](ai.jpg "Example Title(ai.jpg)")` 

![Image with title](ai.jpg "Example Title(ai.jpg)")

## Code

### Inline

`Inline code` Inline code

### Block

```
Block code
```

## Tables

```
| Header 1 | Header 2 |
| -------- | -------- |
| Cell 1   | Cell 2   |
| Cell 3   | Cell 4   |
```

| Header 1 | Header 2 |
| -------- | -------- |
| Cell 1   | Cell 2   |
| Cell 3   | Cell 4   |

## Blockquotes

`> Blockquote`

> Blockquote

## Horizontal Rules

`---`

---

## Footnotes

`[^1]` [^1]

`[^1]: Footnote text.`

shown at the bottom of the page.

[^1]: Footnote text.

## Abbreviations

`The HTML specification is maintained by the W3C.`
The HTML specification is maintained by the W3C.

`*[HTML]: Hyper Text Markup Language`
*[HTML]: Hyper Text Markup Language

`The HTML specification is maintained by the W3C.`
The HTML specification is maintained by the W3C.

## Definition Lists

```
Term 1
: Definition 1

Term 2
: Definition 2
```

Term 1
: Definition 1

Term 2
: Definition 2

## Task Lists

```
- [x] Task 1
- [x] Task 2
- [ ] Task 3
```

- [x] Task 1
- [x] Task 2
- [ ] Task 3

## Emoji

```
:smile:
```

:smile:
for more emoji codes visit [Emoji Cheat Sheet](https://www.webfx.com/tools/emoji-cheat-sheet/)
## Subscript and Superscript

`H~2~O` H~2~O

`X^2^` X^2^

## Inserted and Deleted Text

`++Inserted++` ++Inserted++

`~~Deleted~~` ~~Deleted~~

## Math 

### inline

`$a^2 + b^2 = c^2$` $a^2 + b^2 = c^2$

### block

```
$$
a^2 + b^2 = c^2
$$
```

$$
a^2 + b^2 = c^2
$$

# This is the end of the post
