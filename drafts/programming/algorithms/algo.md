---
title: Algo
description: 
published: true
date: 2026-01-09T15:15:43.267Z
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
    -> large trees possble due to unbalanced composition.

* Weighted quick-union
	extend quick-union with tree size, and merge the root of the smaller tree into the root of the larger one. 
  this implies tracking the size of each tree
    
* Weighted QU + path compression: 
  extend Weighted quick-union and flatten the tree even further by assign each node to its grandparent when looking up a specific node.


Time complexity (worst-case, for indication)

| Algoritm       | Initialization | Merge | Find  |
| -------------- | -------------- | ----- | ----- |
| Quick-find     |              N |     N |     1 |
| Quick-union    |              N |     N |     N |
| Weighted QU    |              N | lg(N) | lg(N) |
| WQUPC          |              N |  α(n) |  α(n) |

> TODO: do above table properly