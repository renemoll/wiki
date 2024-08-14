---
title: Floating point numbers
description: 
published: true
date: 2024-08-14T08:18:27.958Z
tags: 
editor: markdown
dateCreated: 2024-08-13T06:49:32.863Z
---

# Floating point numbers


## The problem

```C
bool isEqual = fabs(f1 – f2) <= epsilon;
```

* `FLT_EPSILON` is a standard define -> defines the difference between `1.0` and the next representable value.
* epsilon depends on the (difference of the) values you are comparing

Alternative: relative epsilon -> error as a max percentage of the differerence between 2 floats.
May require tweaking depending on the input.


## How to compare

* Comparing against zero? Absolute epsilon
* Comparing non-zero numbers? Relative epsilon or ULPs
* Comparing two numbers which could be zero and non-zero? ...


## Tooling

* compiler options?
* analysis tools?

## References

* [Comparing Floating Point Numbers, 2012 Edition](https://randomascii.wordpress.com/2012/02/25/comparing-floating-point-numbers-2012-edition/)