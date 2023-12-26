---
title: Applying LLMs in Specific Domains
seo_title: NLPProj
summary: Some thoughts about the challenge and the impact of LLMs in.
description: A brief guide to post template. # not sure about the usage
slug: NLPProj
author: FlammingFrost
math: true # set to true to enable KaTeX rendering

draft: false # set to false to publish
date: 2023-12-26
lastmod: 2023-12-26 # both date and lastmod will show in the post's footer


categories:
tags:
series: 

toc: true # set to true to enable a Table of Contents
related: true # set to true to enable Related Posts section
social_share: true # set to true to enable Social Sharing buttons
newsletter: false # set to true to enable Newsletter section, at the bottom of the page
disable_comments: false # set to true to disable comments for a specific post
---

> This is a part of Project 2 of the course *Advanced Natural Language Processing* in Fall 2023 at Southern University of Science and Technology. Taught by Prof. [Guahua Chen](https://faculty.sustech.edu.cn/?tagid=chengh3&iscss=1&snapid=1&orderby=date&go=1).

# Applying LLMs in Specific Domains

In this blog, I would like to share some of my thoughts on applying LLMs in specific domains. I will focus on the following aspects:
- What are the challenges of applying LLMs in specific domains?
- What will be the future of these domains?

I will focus on **clinical domain**, a domain that:
- has a large amount of private, unlabeled data; while the labeled data is sparse and expensive to obtain.
- high economic value
- social importance

## Challenges
**For model designer**, the model performance might be the most important thing. Only after with a stable and reliable performance, the model can be permitted to be used in the real world. 
- Accuracy
- Reliability
- efficiency
- interpretability

But we should notice a gap between the performance on metrics (like benchmarks) and the performance in the real world. The model should not overfit the benchmarks, but should be able to generalize to the real world. However, like what's described by Gresham's Law, due to a lack of real-evaluation, model designers tend to overfit the benchmarks and ignore the real-world performance.

**For engineers**, more challenges are waiting for them.
- Data privacy
- Data security
- Data bias

For example, in the clinical domain, the data is highly private and sensitive. Hospital are usually reluctant to share their data with others. Some solutions like federated learning can be used to solve this problem. But it is still a challenge to apply LLMs in the clinical domain. Another challenge is the correctness of the model output. For example the *illusion* of the model. The model might be overconfident in its prediction, but the prediction is actually wrong. This is a challenge for the model designer to improve the reliability of the model.

**There are other challenges** need to be considered before LLMs enter the clinical domain and potentially solve the problems in the clinical domain independently.

- Legal issues
- Ethical issues

FDor example, no doubt that if insurance companies use the model to predict the risk of a patient, it will be a great help for the insurance company. But it will also be a disaster for the patient. The patient might be rejected by the insurance company, and the patient might not be able to get the treatment he needs. This is particular problematic if the LLM is still not reliable enough, as its output might contain bias and errors.

## Future

I want to share some of my thoughts on the impact of LLMs in labor market.

I firmly believe that no matter how good the model can be in the near future, it's inevitable that LLM will replace human experts in corresponding domains, in a large scale. Offering cheap though low-quality service, it can easily take over the market.

The story is not about a LLM learning slowly and secretly, then released and beat all the human experts in one day. It's about a LLM first providing a cheap service and inaccurate service. With a convenient AI assistance, people is less likely to turn to human experts for consulting unless it's necessary, causing a dramatic drop in need. This will eventually force the majority of human experts to leave the market.

Only the most experienced and skilled human experts will remain in the market. They will provide high-quality service, and the price will be high.
~~Then the LLM will gradually improve its performance, and finally beat all the human experts.~~