---
title: Components
description: 
published: true
date: 2024-09-20T09:17:57.463Z
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
  * Cons: increases latency (possibly changing timing)
* Disable a range of interrupts
  * Pros: still simple, native support by most ARM Cortex-M (expect M0)

> TODO: ARCH table

### Design

* Ensure entering a critical section wihtin a critical section is possible and the exit behaviour is as expected.
  * Use the RAII pattern to capture the current state and restore that state when exiting the critical section.
* Use `PRIMASK`


### References

* [EnterCritical() and ExitCritical(): Why Things are Failing Badly](https://mcuoneclipse.com/2014/01/26/entercritical-and-exitcritical-why-things-are-failing-badly/)
