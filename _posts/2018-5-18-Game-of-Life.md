---
layout: post
title:  "Game of Life"
date:   2018-05-18 21:24:14 +1000
categories: javascript trick
---

Conway's Game of Life is a well-known simulation game. At first glance, it's easy to implement, but to a degree, for example, on a grid of extremely large dimensions, it's very complex to achieve optimal results.

![markup]({{site.url}}/assets/images/game-of-life-colored.gif)

The game consists of a grid of n × m, each cell can has one of two state **alive** or **dead**.

At one point in time, the whole grid is called a **generation**, and the computer automatically changes from one generation to the next by changing the cells on the grid, according to the rules. :

*   Live cells that have **2 or 3** adjacent living cells will continue to live to the next generation. On the contrary, it will be dead.
*   The dead cells that have **three** adjacent living cells will become the living cells in the next generation.

![markup]({{site.url}}/assets/images/game-of-life-visual.png)

> Source: http://natureofcode.com/book/chapter-7-cellular-automata/

One of the easiest ways to implement this game is to use an n × m 2 dimensional array, with each element representing a cell.

For each generation, we run two nested `for` loops, count the total number of adjacent "neighbors", and perform the transformation according to the set. In the following figure, the number on each cell represents the number of adjacent cells of that cell, transforming it into two successive generations:

![markup]({{site.url}}/assets/images/game-of-life-blinker.png)

> Source: http://www.paleotechnologist.net/?p=451

    Input: A two-dimensional array of size n × m

    1: For i from 0 → n:
    2: For j from 0 → m:
    3: Count the adjacent living cells of cell A [i, j]
    4: Transform the state of cell A [i, j] based on the number of live cells counted above
    5: Returns array A


```
Output: A new two-dimensional array of size n × m
```

The algorithm has the complexity of O(nm) and absolutely not the optimal solution. The bigger the n × m, the slower generation will be.

One point to keep in mind for the algorithm is that the count of adjacent cells needs to be done on the array representing the older generation, not the new generation array being created.

___

There are many solutions to optimize Game of Life's generations, most of which serve the purpose of handling the largest possible size of the game.

One of the most discussed solutions is the [Hashlife](http://www.drdobbs.com/jvm/an-algorithm-for-compressing-space-and-t/184406478?pgno=1) algorithm, which represents the grid of the game using Quadtree and uses the memoize method to speed up computing.

![markup]({{site.url}}/assets/images/game-of-life-quadtree.gif)
> Source: Dr. Dobb's - An Algorithm for Compressing Space and Time

Next, GPU solutions such as [texture-based solutions](http://nullprogram.com/blog/2014/06/10/) for computation with WebGL, or using [CUDA](http://www.marekfiser.com/Projects/Conways-Game-of-Life-on-GPU-using-CUDA).

As you can see, implementing Game of Life is a pretty interesting topic, if you want it to be easy (limited size), it's extremely easy, but if you want it more difficult (no size limitation), it's also extremely complicated.