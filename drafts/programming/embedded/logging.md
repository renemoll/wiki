---
title: Logging
description: 
published: true
date: 2025-07-04T20:58:30.350Z
tags: 
editor: markdown
dateCreated: 2025-07-04T20:15:00.067Z
---

# TODO

* [STM32 C++ and Retargeting std::cout to UART](https://stackoverflow.com/questions/71442249/stm32-c-and-retargeting-stdcout-to-uart)
* Find a place for: [Howto: Porting newlib - A Simple Guide](https://www.embecosm.com/appnotes/ean9/ean9-howto-newlib-1.0.html#id2719973)


# Logging

Ways to output:
* printf
* iostream
  * std::cout
  * write to file

## embedded

[printf on embedded](https://interrupt.memfault.com/blog/printf-on-embedded)

* `printf` will call `_write` which can be re-implemented to call UART
* you will need nano specs (impact?)
* use `setvbuf` to configure the output buffer for `printf`
* only from one context
  * even desired to log from interrupt context? should not be...
  

Redirects

* UART
  * Pro: only requires a UART peripheral and serial to USB conveter
  * Pro: can always be used, even in the field
  * Con: either requires its own UART of snoops bandwidth from an existing link
* Semihosting
  * Pro: easy to setup (supported by newlib and common debug probes)
  * Pro: uses existing SWD/SWO lines
  * Con: only available with a debugger probe connected
  * Con: pauses processor to transfer data
* SWO/ITM
  * Pro: requires only a single pin/wire (SWO)
  * Con: it is an optional ARM feature, so not all chips support it
  * Con: requires a debug probe to capture and decode (though the protocol is straightforward to implement)
* RTT
  * Pro: no additional hardware required
  * Pro: very fast as it does not interrupt the processor
  * Con: only available with a debugger probe connected
  * Con: requires a bit of RAM

speeds
* RTT is very fast as it writes to RAM and reads memory without the processor
* SWO/ITM is quite fast, blocking call but data transfers at high speed
* Semihosting is slow
* UART depends on configuration and if it is shared or dedicated

## IO libs

* https://github.com/Viatorus/emio