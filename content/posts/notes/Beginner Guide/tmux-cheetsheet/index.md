---
title: Using tmux to manage your terminal
seo_title: tmux cheetsheet
summary: Create, kill, and manage tmux sessions
description:
slug: bg/tmux
author: FlammingFrost
math: false # set to true to enable KaTeX rendering

draft: false # set to false to publish
date: 2023-10-21
lastmod: 2023-10-28 # both date and lastmod will show in the post's footer

feature_image:
feature_image_alt:

categories:
  - Cheet sheet
tags:
  - Linux
series: 
  - Beginner's Guide
toc: true # set to true to enable a Table of Contents
related: true # set to true to enable Related Posts section
social_share: true # set to true to enable Social Sharing buttons
newsletter: false # set to true to enable Newsletter section, at the bottom of the page
disable_comments: false # set to true to disable comments for a specific post
---

> The main purpose for me to use tmux is to keep my program running even if I close the terminal.

## Basic Usage

| Command | Description |
| --- | --- |
| `tmux` | Start a new session |
| `tmux new -s <session-name>` | Start a new session with name |
| `tmux ls` | List all sessions |
| `tmux kill-session -t <session-name>` | Kill a session |
| `tmux attach -t <session-name>` | Attach to a session |
| `tmux detach` | Detach from a session |

## Other Commands

| Command | Description |
| --- | --- |
| `tmux rename-session -t <old-name> <new-name>` | Rename a session |
| `tmux switch -t <session-name>` | Switch to a session |
| `tmux a` | Attach to the last session |
| `tmux list-keys` | List all key bindings |
| `tmux list-commands` | List all commands and their arguments |
| `tmux info` | Show information about the current session |



## Installation

On Ubuntu, you can install tmux using the following command:

```bash
sudo apt install tmux
```



## Reference

- [Advanced Tmux Tutorial](https://www.51cto.com/article/664989.html)
