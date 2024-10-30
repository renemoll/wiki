---
title: Concurrency
description: 
published: true
date: 2024-10-30T21:08:20.736Z
tags: 
editor: markdown
dateCreated: 2024-10-30T21:08:20.736Z
---

# Concurrency

## Definitions

Oxford dictionairy:
Concurrency -> "a running togheter in place or time; meeting, combination"
Concurrent -> "running togheter in space, as parallel lines; going on side by side, as proceedings; occuring togheter, as events or circumstances...

Let us summize the above to: multiple activities running at the same time.

### Concurrency in computing

* Task switching -> multiple tasks run on the same processing unit, where a scheduler divides the available processing time between the different tasks, giving the illusion of concurrency.
* context switch -> switch from one task to another
* scheduler -> part of the operating system

* Hardware concurrency -> physically multiple cores (either multiple processors, multiple cores per processor or a combination).

* hardware threads -> a core may be able to run multiple threads.

Modern computers and operating systems combine both hardware concurrency and task switching.

Within an application
* mutliple processes
  * platform specific
  * takes up more system resources compared to addeing another thread
  * communicate between processes via the operating system
    * OS provides a form of security
    * has a learning curve
    * overhead
  * could use different programming languages
* multiple threads
  * multiple threads within the same proces
    * easy to exchange data (but may require synchronization)
    * easy to corrupt data
    
Why use concurrency?
 * performance
 * seperation of concerns
   * grouping specific functionality together and define a clear API

When not to use concurrency?
 * When not worth the effort ...
   * adds complexity
   * threads do eat up limited resources
   * too much threads may slow down the application (context switching)
   
 
    