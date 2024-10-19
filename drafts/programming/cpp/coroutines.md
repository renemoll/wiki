---
title: Coroutines
description: 
published: true
date: 2024-10-19T12:01:37.760Z
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
* Protothreads?

## Coroutines in C++

* Supported from C++20
* stackless (data not stored on the stack (i.e. on the heap)
* a function becomes a coroutine if it contains any of the following: `co_await`, `co_yield`, `co_return`.

## Coroutines on MCU




## References

* [Coroutine](https://en.wikipedia.org/wiki/Coroutine)
* [Coroutines (C++20)](https://en.cppreference.com/w/cpp/language/coroutines)
