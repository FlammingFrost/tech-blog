---
title: Some Notes for Betaflight
seo_title: Some Notes for Betaflight
summary: Recording some difficulties I encountered and the solutions I found when using Betaflight. PID tuning, receiver setup, VTX setup, etc.
description:
slug: fpv/bf
author: FlammingFrost
math: false # set to true to enable KaTeX rendering

draft: false # set to false to publish
date: 2024-03-06
lastmod: 2023-10-28 # both date and lastmod will show in the post's footer

feature_image:
feature_image_alt:

categories:
  - FPV
tags:
  - Betaflight
series: 
  - FPV software
toc: true # set to true to enable a Table of Contents
related: true # set to true to enable Related Posts section
social_share: true # set to true to enable Social Sharing buttons
newsletter: false # set to true to enable Newsletter section, at the bottom of the page
disable_comments: false # set to true to disable comments for a specific post
---

## Dji O3 Air Unit setup
### 1. HD format
From Betaflight 4.4, the DJI HD format is supported. The DJI HD format is 16:9, while the default FPV format is 4:3. It allows more broad canvas for OSD display.

**Settings on Goggles:**
- Go to `Settings` -> `Display` -> `Canvas` -> `Wide` to set the canvas to 16:9.

**Settings on Betaflight:**
- Go to -> `OSD Display` -> `Display format` -> `HD` to set the display format to HD.
- Go to -> `Cmd` -> `set osd_display_port = MSP` to set the OSD display port to MSP. And `save` to save the settings.

