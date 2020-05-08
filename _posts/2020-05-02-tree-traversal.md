---
layout: post
title: Tree Traversal Algorithms
categories: [Tree,Traversal]
tags: [Tree Traversals,pre-order,in-order,post-order,level-order,Depth First Search,DFS,Breadth First Search,BFS]
---

In this article we will go through various tree traversal techniques
(Both recursive and iterative).

Trees may be traversed in two broad ways.

 1. Depth-first order.
    1. Pre-order (first left then center and then right)
    1. In-order (first center then left and then right)
    1. Post-order (first left then right and then center)
 1. Breadth-first order.(One level at a time)

#### Depth-first order (search/traversal)

In abstract sense it works by going to the depth of a node first before exploring all its neighboring nodes. And then coming back again to visit all the left neighboring nodes and repeating the process.

