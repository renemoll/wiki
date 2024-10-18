---
title: Coroutines
description: 
published: true
date: 2024-10-18T09:03:05.689Z
tags: 
editor: markdown
dateCreated: 2024-10-18T09:03:05.689Z
---

# Coroutines



## What are these coroutines?

> Functions whose execution can paused and resumed.


Characteristics:
- Local data within a coroutines persist between succesive calls;
- Execution of a coroutine is suspended the function yields control, and resumes where it left off when the coroutines continues. 

An implementation has at least the following features:
- Control transfer: yield control and pause execution of the current coroutine
  - In asymmetric coroutines, control yields to the caller.
  - In symmetric coroutines, the programmer specifies where to yield to
- is a coroutine able to suspend ifself when called from another function?
  - In such a case the coroutine is a stackful coroutine;
  - On the other hand, stackless coroutines must be explicitly marked as a coroutine.


## Related technologies

* Threads
* Fibers

## References

* [Coroutine](https://en.wikipedia.org/wiki/Coroutine)