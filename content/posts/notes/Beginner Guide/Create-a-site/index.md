---
title: Create A Site by Hugo
seo_title: Create A Site by Hugo
summary: Setting up a Hugo site. Some details and tips.
description:
slug: bg/create-a-site
author: FlammingFrost
math: true # set to true to enable KaTeX rendering

draft: false # set to false to publish
date: 2023-07-29
lastmod:  2023-07-29 # both date and lastmod will show in the post's footer

feature_image:
feature_image_alt:

categories:
  - 
tags:
  - Hugo
series: 
  - Beginner's Guide
toc: true # set to true to enable a Table of Contents
related: true # set to true to enable Related Posts section
social_share: true # set to true to enable Social Sharing buttons
newsletter: false # set to true to enable Newsletter section, at the bottom of the page
disable_comments: false # set to true to disable comments for a specific post
---

# Create A Site by Hugo

In this post, I will share some details and tips about setting up a Hugo site. My three sites are all built by Hugo, and I have some experience to share.

I will share how I create a site in Windows system, and deploy it to GitHub Pages(A free hosting service for static websites).

Specifically, I will talk about the following aspects:

- How to prepare the environment for Hugo
- How to create a new site based on a theme
- How to customize your site
- How to deploy your site
- Some difficulties and solutions

> **Note:** This post is still in progress. I will update it from time to time.

## Prepare the environment

To correctly render most of themes and plugins, you need to install the extended version of Hugo. An installation of go is also required.

### Install Hugo

I recommend to complete the installation using Chocolatey, a package manager for Windows.

Run the following command in PowerShell as administrator:

- Install Chocolatey

```powershell
powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))"

SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
```

- Install Hugo

```powershell
choco install hugo-extended -confirm
```

- Install go

```powershell
choco install golang -confirm
```

### Install Git

Git is required to deploy your site to GitHub Pages. And it is also a good tool for version control.

You can install Git at [Git](https://git-scm.com/downloads).

## Create a new site

To create a new site, you can use the following command:

```bash
hugo new site <site-name>
```
This will create a new site named `<site-name>`(a folder) in the current directory. It contains all basic files and folders for a Hugo site.

After you create a new site, initialize a git repository in the site folder.

```bash
cd <site-name>
git init
```

### Install a theme

You can install a theme by cloning its repository to the `themes` folder. Themes can be found at [Hugo Themes](https://themes.gohugo.io/) or any other places. For example, this site uses theme [hugo-liftoff`](https://github.com/wjh18/hugo-liftoff).

It is recommended to keep the theme as a git submodule. This will make it easier to update the theme. **Note that you should not modify the theme files directly.** Because the submodule will not track the changes you made, and you will lose the changes when you update the theme(git only push the submodule as a link).

```bash
git submodule add url-to-theme themes/theme-name
```

or

```bash
cd themes
git submodule add url-to-theme
```

The `content` folder of you site is currently empty. To play with the theme, you should first read the theme's documentation. It will tell you how to use the theme and how to customize it.

Generally, in `/themes/theme-name/exampleSite`, there is a folder named `content`. You can copy the content folder to the root of your site. Then you can run `hugo server` to see the site in your browser. 

*If you have more than one theme in your `themes` folder, you can specify the theme by `hugo server -t theme-name`.*

## Customize your site

### Post

You should be able to edit post content totally by editing the markdown files in the `/content/post-topic` folder. The markdown file consists of two parts: front matter and content.

The front matter is a set of key-value pairs. It is surrounded by `---`. The front matter of this post is:

```yaml
---
title: Create A Site by Hugo
seo_title: Create A Site by Hugo
summary: Setting up a Hugo site. Some details and tips.
...
# key: value
---
```
or 
```toml
+++
title = "Create A Site by Hugo"
seo_title = "Create A Site by Hugo"
summary = "Setting up a Hugo site. Some details and tips."
...
# key = value
+++
```

The front matter configures the post, and themes differ in the front matter they support. You can find the front matter of a post in the theme's documentation. Or you can simply imitate the front matter of existing posts.

The content is the main part of the post. It is written in markdown. You can find the syntax of markdown at [Markdown Guide](https://www.markdownguide.org/basic-syntax/). The supported markdown syntax may differ in different themes, and they should be just shown by those examples. Again, read the description of the theme carefully whenever you have questions.

### Configuration

#### Config Priorities

In previous hugo version, the configuration is written in `config.toml` or `config.yaml`. The lateset version of hugo uses `hugo.toml/hugo.yaml/hugo.json` instead.

Sometimes there are more than one configuration files, and they have different priorities. The priority is:(from low to high)

1. `config/_default/config.toml`
2. `themes/your-theme-name/config.toml`
3. `config.toml`

The configuration file will include all configurations of lower proirity but overwrite any duplicated configurations.

Here are some commonly used configurations:

```toml
title = "My New Hugo Site" # The title of your site
baseURL = "https://example.org/" # The base URL of your site, you should change it to your own domain when you deploy your site
languageCode = "en-us" # The language code of your site
theme = "your-theme-name" # The theme you use
```

## Deploy your site to GitHub Pages

GitHub Pages is a free hosting service for static websites. You can deploy your site to GitHub Pages by following the steps below:

1. Create a new repository named `<your-username>.github.io` on GitHub. This will be the repository for your site. And the result will be shown at `https://<your-username>.github.io`.
You can also use another name for your repository, but the result will be shown at `https://<your-username>.github.io/<repository-name>`.
2. Add a remote to your local repository.
```bash
git remote add origin url-to-your-repository
# Push your local repository to GitHub.
git push -u origin main
# Pay attention to the branch name. 
# It should be main instead of master.
```
3. Enter the **Setting** of your repository, and scroll down to the GitHub Pages section. In **Build and deploy**, choose **Source** as **Guihub Actions**. For more infomation, visit [Host on GitHub Pages](https://gohugo.io/hosting-and-deployment/hosting-on-github/).

You can also learn to deploy your site to other platforms at [Hosting and Deployment](https://gohugo.io/hosting-and-deployment/).

## Some difficulties and solutions

### Edit corresponding files

Go into your theme folder, change file content and watch for changes in the browser. Remember to overwrite the file in root folder instead of the theme folder.

Generally, the following folders are used for:
- `content`: the content of your site
- `static`: static files, such as images, css, js, etc. For example, your avatar may be put in `static/images/avatar.jpg`.
- `layouts`: the layout of your site. For example, the layout of the home page is in `layouts/index.html`. The layout control how you markdown files are rendered into html files.

### Math rendering

#### Add Math support to your theme

KaTeX is a popular math rendering library. It can support most of the math syntax in LaTeX.

If your theme does not support Math rendering, you can use auto-render extension of KaTeX. You can find the usage at [KaTeX](https://katex.org/docs/autorender.html).

It usually involves the following steps:

- Add the reference to partials in html file used to render your post. For example, in `layouts/_default/single.html`, add the following line:
```html
{{ if .Ismath }}
{{ partial "katex.html" . }}
{{ end }}
```
Note that the real file name may differ from this example.
- Create a `math.html` or "katex.html" file in `layouts/partials` folder. It should refer to the KaTeX library and the auto-render extension. For example:
```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.16.8/dist/katex.min.css" integrity="sha384-GvrOXuhMATgEsSwCs4smul74iXGOixntILdUW9XmUC6+HX0sLNAK3q71HotJqlAn" crossorigin="anonymous">
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.16.8/dist/katex.min.js" integrity="sha384-cpW21h6RZv/phavutF+AuVYrr+dA8xD9zs6FwLpaCct6O9ctzYFfFr4dgmgccOTx" crossorigin="anonymous"></script>
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.16.8/dist/contrib/auto-render.min.js" integrity="sha384-+VBxd3r6XgURycqtZ117nYw44OOcIax56Z4dCRWbxyPt0Koah1uHoK0o4+/RRE05" crossorigin="anonymous"
    onload="renderMathInElement(document.body);"></script>
```
- Add the following line to the front matter of your post:
```yaml
math: true
```

#### Difference of Math expressions in Markdown and LaTeX

- KaTeX supports most of the LaTeX syntax, but not all. For example, `\begin{align*}...\end{align*}` is not supported. You can find the supported syntax at [KaTeX](https://katex.org/docs/supported.html).
- Pay attention to subscript and superscript. In LaTeX, you can use `x_{i}` & `x^{i}`. But when they appear twice in a math expression, markdown (with KaTex) may not render them correctly. Because in markdown, `_this-is-your-content_` can be rendered as italic. Here is an example:

  To render 

  $\mathbb{E}_S[V\_{\pi}(S)]$

  You should not write

  `
  $\mathbb{E}_S[V_{\pi}(S)]$
  `

  Because it will be rendered as

  $\mathbb{E}_S[V_{\pi}(S)]$

  Instead, use (add "\\" before "\_")

  `
  $\mathbb{E}_{S}[V\_{\pi}(S)]$
  `

  Then it will be rendered correctly.





