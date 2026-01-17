---
title: Algo
description: 
published: true
date: 2026-01-17T08:32:59.590Z
tags: 
editor: markdown
dateCreated: 2026-01-06T13:49:12.644Z
---

# Algo

Algorithms and data structures go hand in hand, as algorithms are applied onto data.


Data structures

* union-find: stores a collection of non-overlapping (disjoint) sets.
  Typical operations: add new items/sets, connect items (merge sets), determine if two items belong to the same set.





Algorithms





### Example: implementations of union-find

There are various ways to implement a datatype such as union-find, this shows that different algorithms lead to different time and space characteristics.

* Quick-find
	using an identifier array, assigns a set identifier to each element. 
  
  Cons:
  Merge operation is too expensive
  
* Quick-union
  using an identifier array, assigns a parent identifier to each element.
  
  Cons:
  While is can be faster, worst case for find could still be N due to tall trees
    -> large trees possible due to unbalanced composition.

* Weighted quick-union
	extend quick-union with tree size, and merge the root of the smaller tree into the root of the larger one. 
  this implies tracking the size of each tree
    
* Weighted QU + path compression: 
  extend Weighted quick-union and flatten the tree even further by assign each node to its grandparent when looking up a specific node.


Time complexity (worst-case, for indication of array access)

| Algorithm      | Initialization | Merge | Find  |
| -------------- | -------------- | ----- | ----- |
| Quick-find     |              N |     N |     1 |
| Quick-union    |              N |     N |     N |
| Weighted QU    |              N | lg(N) | lg(N) |
| WQUPC          |              N | lg(N) | lg(N) |

> TODO: do above table properly


### Algorithm analysis

Basic steps:

1. Observe: observe some quantity (i.e run time, memory usage, ...), over different input sizes (doubling the input with each experiment will reveal a power law.)

1. Hypothesize: using the results of the observation (i.e. in the form of a log/log plot), determine the trend (i.e. approximation function). This will form the basis of a **cost model**.

1. Predict: using the model, predict the change of the observed quantity (**cost**) for new inputs.

1. Verify: verify the new predictions, made using the hypothesized model, agree with new observations. 

1. Validate: continue the above until the hypothesis (cost model) and observations agree.  

Now, when we make observations we may also measure undesired effects which are unrelated to the algorithm under analysis. Such as impact of the OS scheduler, IO latency (system), CPU processing power (hardware), used programming language (software). The goal is not to be a 100% accurate, but to determine the trend.

#### The cost model

Run-time is generally the cost to look at. In that case, two factors are important: 
1. the cost of executing a set of statement and;
1. the number of times each statement is executed.

**Tilde approximation**
While it is possible to analyze the run-time for each statement in detail, it is a tedious excersive with limited value. Instead, focus on the most expensive and/or most executed statements (assuming that will dominate the costs (hypothesis)).

Next, approximate by ignoring lower order terms:
$$aN^3 + bN^2 + cN + d \sim aN^3$$

**Order of growth classifications**

Order of Growth (OoG)

Name         | Order of Growth | Description
-------------|-----------------|------------
Constant     |        1        | Statement, look-up
Logarithmic  |        log(n)   | Divide in half
Linear       |        n        | Loop
linearithmic |        n log(n) | Divide and conquer
Quadratic    |        n^2^     | Double loop 
Cubic        |        n^3^     | Tripple loop
Exponential  |        2^n^     | 
Factorial    |        n!

Notations:
- $\Omega$ used for lower bound
- O: used for upper bound
- $\Theta$: used both(?) (clasification?)

### Theory of algorithms

- best case: easiest input -> goal
- worst case: most dificult input -> guarantee for all inputs
- average case: "random" input -> prediction

Goal
 - determine dificulty of a problem
 - find "optimal" algorithms
 
Approach
 - Suppress details during analysis
 - focus on worst case input to avoid variation
 