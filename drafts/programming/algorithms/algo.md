---
title: Algo
description: 
published: true
date: 2026-01-06T13:49:12.644Z
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





union-find - implementations

* Quick-find: assigns a set identifier to each element. 
* Quick-union: assigns a parent identifier to each element.
  -> large trees possble due to unbalanced composition.
* Weighted quick-union: extend quick-union with tree size, and merge smaller tree into the larger one. 
* Weighted QU + path compression: flatten the tree even further by assign each node to its grandparent when looking up a specific node.

Time complexity (worst-case, for indication)

| Implementation | Initialization | Merge | Find  |
| -------------- | -------------- | ----- | ----- |
| Quick-find     |              N |     N |     1 |
| Quick-union    |              N |     N |     N |
| Weighted QU    |              N | lg(N) | lg(N) |
| WQUPC          |              N |     ? |  α(n) |

> TODO: do above table properly