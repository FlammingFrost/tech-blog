---
title: Basic Concepts in Network Science
seo_title: Basic Concepts in Network Science
summary: Start from graph theory, we use some quantitative measures to describe the structure of a network.
description: 
slug: NetSci/basic-concepts
author: FlammingFrost
math: true # set to true to enable KaTeX rendering

draft: true # set to false to publish
date: 2024-03-10
lastmod: 2024-03-10 # both date and lastmod will show in the post's footer

feature_image:
feature_image_alt:

categories:
  - Network Science
  - Tutorial

tags:
  - Network
  - Basic
series: 
  - Network Science Course Notes

toc: true # set to true to enable a Table of Contents
related: true # set to true to enable Related Posts section
social_share: true # set to true to enable Social Sharing buttons
newsletter: false # set to true to enable Newsletter section, at the bottom of the page
disable_comments: false # set to true to disable comments for a specific post
---

## Degree & neighbors
Degree of a node is the number of edges connected to it. For a directed network, we have in-degree and out-degree.

The neighbors of a node are the nodes that are connected to it by an edge.

The sum of all degrees in a network is twice the number of edges, because each edge is counted twice.
$$
L = \frac{1}{2}\sum_{i=1}^{N}k_i (\text{undirected network}) = \frac{1}{2}(\sum_{i=1}^{N}k_i^{in} + \sum_{i=1}^{N}k_i^{out}) (\text{directed network})
$$

In network science, we use $\langle \cdot \rangle$ to denote the average (mean) of a quantity. For example, the average degree of a network is $\langle k \rangle = \frac{1}{N}\sum_{i=1}^{N}k_i$.

## Degree Distribution
The degree distribution of a network is the probability distribution of the **degrees** over the entire network. For example, a long-tailed distribution means that there are more nodes with large degrees, compared to a normal distribution.

As a distribution, it basically have:
- Normalized: $\sum_{k=1}^{N}p_k = 1$ or $\int_{k_{min}}^{k_{max}}p(k)dk = 1$
- Probability: $p_k = \frac{n_k}{N}$, where $n_k$ is the number of nodes with degree $k$, and $N$ is the total.

In language of expectation, the average degree of a network is $\langle k \rangle = \sum_{k=1}^{N}kp_k$.

## Adjacency Matrix
The adjacency matrix $A$ of a network is a square matrix used to represent a finite graph. 

$A_{ij} = 1$ if there is an edge from node $j$ to node $i$. You can image that the edge/link flows from $j$ to $i$, from the top of $A$ to the left.

It's clear that the adjacency matrix is symmetric for an undirected network.

I think such definition means to facilitate the matrix operation, such as matrix multiplication on the right. For example, $A^2_{ij}$ is the number of paths of length 2 from node $j$ to node $i$.

## Bipartite Network
A bipartite network is a network whose nodes can be divided into two disjoint sets $U$ and $V$, such that every link connects a node in $U$ to a node in $V$. This means that a node in $U$ can only connect to a node in $V$, and vice versa.

## Weighted Network
In a weighted network, each edge/link has a weight. The weight can be any real number, and it can represent the strength of the connection. In problems like traffic flow, transportation, or social network, the weight can represent the capacity of the road, the number of passengers, or the strength of the relationship.

## Path & Distance
The distance between two nodes is the length of the **shortest** path between them. For a weighted network, the distance is the sum of the weights of the edges in the shortest path. (or you can perceive the unweighted network as a weighted network with all weights equal to 1)

The average distance of a network is the average of the shortest path between all pairs of nodes.
$$
\langle d \rangle = \frac{1}{N(N-1)}\sum_{i\neq j}d_{ij}
$$
Here the denominator $N(N-1)$ is the number of possible pairs of nodes. It's also the number of links in a complete network.

## Connectedness
If there is a path between node $i$ and node $j$, we say that node $i$ and node $j$ are connected. 

A network is connected if there is a path between every pair of nodes. Otherwise, it's disconnected.

If a network is disconnected, it consists of several connected components. A connected component is a subgraph in which every pair of nodes is connected by a path.

## Clustering Coefficient
Clustering coefficient measures the how the neighbors of a node are connected to each other. 

It is defined as the fraction of the number of links between the neighbors of a node and the maximum possible number of links between them.
$$
C_i = \frac{2L_i}{k_i(k_i-1)} = \frac{L_i}{k_i(k_i-1)/2}
$$
where $L_i$ is the number of links between the neighbors of node $i$, and $k_i$ is the degree of node $i$. Note that $C\in[0,1]$. The larger the clustering coefficient, the more the neighbors of a node are connected to each other.

