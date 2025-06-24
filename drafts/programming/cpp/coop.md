---
title: Execution model
description: 
published: true
date: 2025-06-24T18:39:06.323Z
tags: 
editor: markdown
dateCreated: 2025-06-24T18:39:06.323Z
---

# TODO

* look at philips amp
* look at rust embassy
* look up basics and add examples

# Execution model


Application: actor model like
* modules accepting messages from various sources

Why?
* Decoupling
* Clear interface
* Flexilibity

Cons:
* Data races?
* Do not want to spin up threads on a microcontroller


Application interacts with hardware, both inside microcontroller (peripherals) and outside (external devices). Execution a task (communication, calculation, ..) can take time.

API options:
* Blocking API calls
  Call from application module blocks until the driver is ready.
  * Sequential code and accept the wait
* Asynchronous calls
  Call from application module triggers a driver to perform a certain action.
  Either:
  * the application periodically polls the driver for an update; or
  * the driver invokes a callback.
  
  Can emulate blocking calls when desired.
  Likely use a state machine: wait with the next step until ready.
  
* theading (non-preemptive)
  Thread yield after triggering blocking operations.
  Will still need to poll/be notified when the operation is complete. Scheduler may schedule the thread even when there is no result available yet.
  
* cooperative multitasking (fibers/coroutines)
  Either a fiber (application module) blocks (and does not get scheduled) until the driver completes its action.
  


