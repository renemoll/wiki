---
title: Error handling
description: 
published: true
date: 2026-02-27T10:58:02.909Z
tags: 
editor: markdown
dateCreated: 2026-02-27T10:58:02.909Z
---

# On error handling




Kinds of errors:
* user errors
    
    Think of a user providing invalid input (text, flags, ..)
    
* system errors

    A system service or resources becoming unavailable. Think of loosing a wireless connection, or running out of memory.

* programming errors

    Passing an invalid parameter to a function.

These different kind of errors require different stategies to handle.


User errors are to be expected, a user can input anything and your application has to "deal" with it. This means parsing user input. (article on parsing vs validation)

System errors can ocour, some may be normal operation, other may be exceptional. Wether or not the application needs to be robust against these errors depends on the application. Same applies to libraties. When you cannot gaurantee a working state, termination is the solution.

Programming errors are bugs and therefore should be fixed. 
 * should be caught as soon as possible.
 * for a library/module, it should be clear on the interface what goes wrong (not 10 levels deep in the call stack) to make it clear as a programmer error and nog a library error.

How to reach as soon as possible:
 * detect issues at compile time
   * using strong types can avoid many checks (if this pointer not null, is this integer positive or negative)
 * detect issues trough compiler warnings
   * configuration -> use bob :)
 * detect issues trough static analysis
    * integrate tools into the build
 * detect issues trough unit testing (with dynamic analysis)
    * integrate tools into the build
    * test edge cases (on exposes API)
 * detect issues trough runtime checks
    * contracts/asserts/checks





