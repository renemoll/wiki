---
title: Components
description: 
published: true
date: 2024-09-20T12:54:43.508Z
tags: 
editor: markdown
dateCreated: 2024-09-20T09:17:57.463Z
---

# Components


## Critical section

Use: ensure a single thread is executing specific piece of code.
Note: a thread here means context (main, interrupt, thread).
Related to: reentrancy.

### Options

* Disable all interrupts
  * Pros: simple and effective
  * Cons: increases latency of all interrupt handling
* Disable a range of interrupts
  * Pros: still simple, native support by most ARM Cortex-M (expect M0)
  * Cons: increases latency of disabled interrupt handling

> TODO: ARCH table

### Design

* Allow nesting
  * Ensure entering a critical section wihtin a critical section is possible and the exit behaviour is as expected.
  * Use the RAII pattern to capture the current state and restore that state when exiting the critical section.
* Use `PRIMASK`/`BASEPRI`

### Limitations

* Only works properly on single processor applications, which is acceptable for MCU deployment.

### References

* [Critical section](https://en.wikipedia.org/wiki/Critical_section)
* [EnterCritical() and ExitCritical(): Why Things are Failing Badly](https://mcuoneclipse.com/2014/01/26/entercritical-and-exitcritical-why-things-are-failing-badly/)

## Debouncing

### Options

* Digital logic ;)
* Hardwware filter
* Periodically (via a timer) read the input and once stable for X time, indicate input is present.

### References

* [A Guide to Debouncing, or, How to Debounce a Contact in Two Easy Pages, by Jack Ganssle](https://www.ganssle.com/debouncing.htm)
* [A Guide to Debouncing - Part 2, or, How to Debounce a Contact in Two Easy Pages, by Jack Ganssle](https://www.ganssle.com/debouncing-pt2.htm)

