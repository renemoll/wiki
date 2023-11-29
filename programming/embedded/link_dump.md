---
title: links
description: 
published: true
date: 2023-11-29T20:15:42.458Z
tags: 
editor: markdown
dateCreated: 2023-07-16T14:00:49.706Z
---

# Links

# MCU


* [The ITM and the quest for faster logging](https://blog.japaric.io/itm/)
  > compares semihosting, serial and ITM on real CPU time
* [Profiling Firmware on Cortex-M](https://interrupt.memfault.com/blog/profiling-firmware-on-cortex-m)

* [My personal C coding style as of late 2023](https://nullprogram.com/blog/2023/10/08/)
 > idea: alt assert
* [My favorite C compiler flags during development](https://nullprogram.com/blog/2023/04/29/)

* [What is Type-Level Programming?](https://blog.sulami.xyz/posts/type-level-programming/)
  > concept of using types for specific (hardware) modes. I.e. a GPIO output is a different type then a GPIO input, as it has different capabilities.


* [Embedded Logging Case Study: From C to Shining C++ - Luke Valenty -CppNow 2022](https://www.youtube.com/watch?v=Dt0vx-7e_B0)

## Bootloader

* [mcuboot](https://github.com/mcu-tools/mcuboot)
* [How to update the OpenBLT bootloader itself](https://www.feaser.com/en/blog/2022/05/how-to-update-the-openblt-bootloader-itself/)
* [HN: From zero to main(): How to write a bootloader from scratch (memfault.com)](https://news.ycombinator.com/item?id=24635383)
* 

## start-up

* [From Zero to main(): Bare metal C (2019) (memfault.com)](https://news.ycombinator.com/item?id=34459053)
* [Itanium C++ ABI](https://itanium-cxx-abi.github.io/cxx-abi/abi.html#obj-ctor)
* [The most thoroughly commented linker script (probably)](https://blog.thea.codes/the-most-thoroughly-commented-linker-script/)
* [ARM Cortex-M Startup code (for C and C++)](https://allthingsembedded.com/post/2019-01-03-arm-cortex-m-startup-code-for-c-and-c/)
* [Creating a C Library](https://wiki.osdev.org/Creating_a_C_Library#Program_Initialization)
* [Calling Global Constructors](https://wiki.osdev.org/Calling_Global_Constructors#ARM_.28BPABI.29)
* [Porting NewLib: crt0](https://stackoverflow.com/questions/3381755/porting-newlib-crt0)

## profiling

* [Profiling memcpy performance on Cortex-M7 (stm32f7)](https://stackoverflow.com/questions/73690767/profiling-memcpy-performance-on-cortex-m7-stm32f7)
* [Cortex-M7 instruction cycle counts, timings, and dual-issue combinations](https://www.quinapalus.com/cm7cycles.html#conclusions)

# bob

* [stack protection](https://github.com/embeddedartistry/libc/blob/master/src/crt/stack_protection.c) / [blog](https://embeddedartistry.com/blog/2020/05/18/implementing-stack-smashing-protection-for-microcontrollers-and-embedded-artistrys-libc/) / ["Strong" stack protection for GCC](https://lwn.net/Articles/584225/)
* [cppbestpractices](https://github.com/cpp-best-practices/cppbestpractices/blob/master/02-Use_the_Tools_Available.md)
* [Effective Modern CMake](https://gist.github.com/mbinna/c61dbb39bca0e4fb7d1f73b0d66a4fd1)
* [cmake_template](https://github.com/cpp-best-practices/cmake_template/blob/main/ProjectOptions.cmake)
* [modern cmake](https://cliutils.gitlab.io/modern-cmake/chapters/features/cpp11.html)


* [readthedocs](https://about.readthedocs.com/)
* [Determine if Python is running inside virtualenv](https://stackoverflow.com/questions/1871549/determine-if-python-is-running-inside-virtualenv)


## auto-complete

* [How do I support tab completion in a python CLI program?](https://software.codidact.com/posts/284708)
* [Free shell auto-completion](https://github.com/docopt/docopt/issues/21)
* [How to make a python, command-line program autocomplete arbitrary things NOT interpreter](https://stackoverflow.com/questions/187621/how-to-make-a-python-command-line-program-autocomplete-arbitrary-things-not-int)
* [How to make python argcomplete run with PowerShell](https://stackoverflow.com/questions/64970692/how-to-make-python-argcomplete-run-with-powershell)
* [shtab](https://iterative.ai/blog/shtab-completion-release)
* 


# C++

* [Awesome Modern C++](https://awesomecpp.com/)
* [https://agraphicsguynotes.com/posts/fiber_in_cpp_understanding_the_basics](Fiber in C++: Understanding the Basics)

## Tools

* [Memory error checking in C and C++: Comparing Sanitizers and Valgrind](https://developers.redhat.com/blog/2021/05/05/memory-error-checking-in-c-and-c-comparing-sanitizers-and-valgrind)
 > Valgrind imposes a bigger slowdown on your application compared to Sanitizers
 > It seems sanitizers can catch more mistakes, however it does require all code to be compiled with the sanitizers enabled. Valgrind does not impose this requirement.
 > Not all sanitizers can at the same time (i.e. address and memory)
   * [ASAN: compiler flags](https://github.com/google/sanitizers/wiki/AddressSanitizerFlags)
   * ASAN: some options require runtime env flags: [AddressSanitizerUseAfterReturn](https://github.com/google/sanitizers/wiki/AddressSanitizerUseAfterReturn)
 * [sanitizers](https://github.com/embeddedartistry/cmake-buildsystem/blob/main/analysis/sanitizers.cmake)

## Libraries

[HN: Snmalloc: A Message Passing Allocator](https://news.ycombinator.com/item?id=37851210)

# Visual design

* [Visual design rules you can safely follow every time](https://anthonyhobday.com/sideprojects/saferules/)
