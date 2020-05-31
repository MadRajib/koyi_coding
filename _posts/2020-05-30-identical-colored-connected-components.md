---
layout: post
title: Finding identically colored connected components in a connected graph.
categories: [Graph,Connected Components,DFS]
tags: [Finding the identically colored connected components,Graph,DFS,Depth First Search]
---

Given a connected graph made of triangles with each vertex assigned a color, find identically
colored connected components. 

There are only three colors red, green, and blue are
considered and they are represented by 1,2,and 3 integers respectively. 

Triangles are
represented by three vertex indices i.e. [0 4 3] red triangle from the example below.

![connected graph]({{ site.BASE_PATH }}/assets/media/connected-graph.png)

The connected components in this graph are :  
Red: {0 ,2 ,3 ,4}  
Blue: {1}  
Green: {5,6} , {8,7}  

We are given two parameters saved in file:

1. List of traingles in the graph (in triangle.txt).
    ```bash
    # traingle.txt
    0 4 3
    0 1 3
    2 3 1
    5 6 3
    4 3 5
    1 8 7
    3 2 6
    ```

1. List of colors for all the vertices in order (in colors.txt).
    Here we are given three colors code  
        **1 => Red**  
        **2 => Green** and  
        **3 => Blue**
    ```bash
    # colors.txt
    1 # node 0
    3 # node 1
    1 # node 2
    1 # node 3
    1 # node 4
    2 # node 5
    2 # node 6
    2 # node 7
    2 # node 8
    ```  

The expected results for this graph should be sorted order by the component size:

```bash
# result.txt
0 2 3 4
5 6
7 8
1
```

## Solution

We will use the logic of *finding connected component from a graph* with a little modification. Go to the following links to understand how it is done.  
[Comoenent (graph theory)](https://en.wikipedia.org/wiki/Component_(graph_theory))  
[connected-components-in-an-undirected-graph](https://www.geeksforgeeks.org/connected-components-in-an-undirected-graph/)

### Approach:
___
#### First thing first !

***How can we find connected components from a graph?***

Well it's simple, now that we have adjacency list, we will visit each node and visit each node that can be reached from this node. We will use DFs for this purpose. And to keep track of nodes we visited for a particular node we will maintain an queue. 


> Note: we will also maintain an array of visited nodes so that we don't create duplicate components.Since only a node can be present only in one component.

After we have visited all the reachable nodes from a particular node.
we save the queue which has all the reachable nodes.
Then we start with another unvisited node and repeat the same process with a newly empty queue.

At the end after we have visited all the nodes we will have collection of set of connected components.

This is how we can use DFS to find all the connected components.

___

#### Coming to the Solution!

***But how can we find identical connected components***

But wait we all ready have a fully connected graph, so if we apply the above logic we will have only one set containing all the nodes, because there is only one connected components consisting of all the nodes.  

So we need to tweak ouf DFS a bit!
Our approach will just the same visit all the neighbors reachable from the current node. But instead of visited every neighbors  we will only visit those neighbor who has same color as the node .  
That way we will only visit same colored connected nodes.

Wow !! It's that simple. And its time code the logic!

___

### Code Time:

#### 1. Declaring a Skelton for logic.
We will create a class with required variables and functions:

<script src="https://gist.github.com/MadRajib/bb372e0a22ff4e8bb67c5f32fb0fd2dc.js"></script>

#### 2. Lets implement functions one by one.

We will implement the functions that deals with the input first!.

1.***ReadColorFile*** function:
  > ***input***: path to the color file.  
    ***output***: void  
    ***processing***: Reads data from the input file,  
    converts the string numbers to int and  
    stores them in ***vertex_colors*** vector.  


<script src="https://gist.github.com/MadRajib/b3139db908a2b1c170e81e656298c48d.js"></script>

2.***ReadTriangleFile*** function:
  > ***input***: path to the color file.  
    ***output***: void  
    ***processing***: Reads data from the input file,  
    converts the string numbers to int and  
    stores them in ***vertex_colors*** vector. 

<script src="https://gist.github.com/MadRajib/225a8d7bf50961280080c3af4187d9a6.js"></script>

3.Now we can initialize the constructor:
<script src="https://gist.github.com/MadRajib/6fdfc60cb6473f2b14caaa1a4dd47788.js"></script>

4.Finally we can work on the main algorithm:
<script src="https://gist.github.com/MadRajib/cb4a7bdb04589f0cbfec71571fe7f37c.js"></script>

5.Now the main function and to write result to the output file.
<script src="https://gist.github.com/MadRajib/02a964c020b2cbb24f06cfa4821b15a8.js"></script>

6. Full Code :  

<script src="https://gist.github.com/MadRajib/65b2a643fdebe16dc0db08b541c64584.js"></script>