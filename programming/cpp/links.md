---
title: C++ Links
description: 
published: true
date: 2023-07-16T12:03:52.862Z
tags: 
editor: markdown
dateCreated: 2022-12-14T19:49:06.828Z
---

# C++ links

A collection of pages I encountered which might be useful

## Blogs

* [Meeting C++ blogroll](https://www.meetingcpp.com/blog/blogroll/)

* [Andrzej's C++ blog](https://akrzemi1.wordpress.com/)
* [Better Embedded System SW](https://betterembsw.blogspot.com/)
* [Embedded Artistry](https://embeddedartistry.com/blog)
* [foonathan::blog()](https://www.foonathan.net/)
* [Interrupt](https://interrupt.memfault.com/blog/)
* [Modernes C++](https://www.modernescpp.com/)
* [The Pasture](https://thephd.dev/)
* [Sticky Bits](https://blog.feabhas.com/)

* [Sutter’s Mill](https://herbsutter.com/)

### Not updated anymore

* [IT Hare](http://ithare.com/)
* [Simplify C++](https://arne-mertz.de/)

## C++20

* [C++20: The Big Four](https://www.modernescpp.com/index.php/thebigfour)
* [Concepts](https://www.modernescpp.com/index.php/define-concepts)
* [Modules](https://www.modernescpp.com/index.php/cpp20-modules)
* [Ranges intro](https://www.modernescpp.com/index.php/c-20-the-ranges-library)
* [Ranges](https://www.modernescpp.com/index.php/the-ranges-library-in-c-20-a-deep-dive)
* [Coroutines](https://www.modernescpp.com/index.php/c-20-coroutines-the-first-overview)
  * [C++20 Coroutines on Microcontrollers—What We Learned](file:///C:/Users/RMQ/Downloads/Belsonetal.-2020-C20CoroutinesonMicrocontrollers-WhatWeLearned.pdf)
    Interesting code, not yet suitable for embedded.

## Usefull code
* [SI units](https://github.com/bernedom/SI)
* foonathan [memory](https://github.com/foonathan/memory)

On `volatile`:
* [Modern Embedded C++ – Deprecation of volatile](https://blog.feabhas.com/2021/05/modern-embedded-c-deprecation-of-volatile/#more-3495)
* [Improve volatile Usage with volatile_load() and volatile_store()](https://embeddedartistry.com/blog/2019/03/11/improve-volatile-usage-with-volatile_load-and-volatile_store/)

## On algorithm implementation:
* [Numerical Recipes](http://numerical.recipes/)

## On software design
* [A Procedure for Designing Abstract Interfaces for Device Interface Modules](https://embeddedartistry.com/fieldatlas/a-procedure-for-designing-abstract-interfaces-for-device-interface-modules/)
* [Prototyping and Design for Change: Lightweight Architectural Strategies](https://embeddedartistry.com/blog/2020/01/20/prototyping-for-portability-lightweight-architectural-strategies/)
* [Feature Flag-Driven Development](https://dzone.com/articles/feature-flag-driven-development)


## Embedded debugging

* [Ending the Embedded Software Dark Ages: Let’s Start With Processor Fault Debugging!](https://embeddedartistry.com/blog/2021/01/11/hard-fault-debugging/)
* [How to debug a HardFault on an ARM Cortex-M MCU](https://interrupt.memfault.com/blog/cortex-m-fault-debug?query=hardfault)

## On embedded software design

* [Embedded Virtual Machine](https://github.com/embvm)
* [Virtual Devices in Embedded Systems Software](https://embeddedartistry.com/blog/2020/08/03/virtual-devices-in-embedded-systems-software/)
* [Real-World Portable Driver Examples](https://embeddedartistry.com/blog/2020/11/23/real-world-portable-driver-examples/)

## On documentation

* [Embedded Artistry README Template](https://embeddedartistry.com/blog/2017/11/30/embedded-artistry-readme-template/)

## Toolchain background

* [ELF file structure](https://wiki.osdev.org/ELF) and [object file](https://en.wikipedia.org/wiki/Object_file)
* [GCC sections](https://gcc.gnu.org/onlinedocs/gccint/Sections.html)
* [Boot sequence](https://wiki.osdev.org/Boot_sequence)
* [How kernel, compiler, and C library work together](https://wiki.osdev.org/How_kernel,_compiler,_and_C_library_work_together)
* [Bare bones](https://wiki.osdev.org/Bare_bones)
* [A tale of two toolchains and glibc](https://www.collabora.com/news-and-blog/blog/2021/09/30/a-tale-of-two-toolchains-and-glibc/)
* [Generating relocatable code for ARM processors](https://blog.llvm.org/posts/2021-10-01-generating-relocatable-code-for-arm-processors/)

* [Tracking Firmware Code Size](https://interrupt.memfault.com/blog/code-size-deltas?query=compile%20flags)
* [Code Size Optimization: GCC Compiler Flags](https://interrupt.memfault.com/blog/code-size-optimization-gcc-flags?query=improving%20compilation%20time)
* [Improving Compilation Time of C/C++ Projects](https://interrupt.memfault.com/blog/improving-compilation-times-c-cpp-projects?query=improving%20compilation%20time)
* [Better Firmware with LLVM/Clang](https://interrupt.memfault.com/blog/arm-cortexm-with-llvm-clang?query=better%20firmware%20with%20llvm)
* [GNU Binutils: the ELF Swiss Army Knife](https://interrupt.memfault.com/blog/gnu-binutils?query=gnu%20binutil)

* [Modern CMake – Tips and Tricks](https://www.incredibuild.com/blog/modern-cmake-tips-and-tricks)

* [text, data and bss: Code and Data Size Explained](https://mcuoneclipse.com/2013/04/14/text-data-and-bss-code-and-data-size-explained/)

* http://www.catb.org/esr/structure-packing/

> https://interrupt.memfault.com/blog/arm-cortexm-with-llvm-clang?query=clang
> https://clang.llvm.org/docs/CrossCompilation.html

### On linters, formatters, sanityzers and such

* [Automatically format and lint code with pre-commit](https://interrupt.memfault.com/blog/pre-commit?query=automatically%20format%20and%20lint)
* [LINT does not do peer reviews](https://betterembsw.blogspot.com/2020/08/lint-does-not-do-peer-reviews.html)
* [Static checks with CMake/CDash (iwyu, clang-tidy, lwyu, cpplint and cppcheck)](https://www.kitware.com/static-checks-with-cmake-cdash-iwyu-clang-tidy-lwyu-cpplint-and-cppcheck/)
* [cmake scripts](https://github.com/StableCoder/cmake-scripts#sanitizer-builds-sanitizerscmake)
* [CodeChecker](https://github.com/Ericsson/CodeChecker)
* [oclint](https://oclint.org/)
* [ikos](https://github.com/NASA-SW-VnV/ikos)

## Tooling

* [sourcegraph](https://about.sourcegraph.com/)

## On Qt/QML

* [Developing a QML Keypad with TDD](https://embeddeduse.com/2021/11/18/developing-a-qml-keypad-with-tdd/)
* [QCustomPlot ](https://www.qcustomplot.com/)
* [PyQt6 events and signals](https://zetcode.com/pyqt6/eventssignals/)

## CMake

* [Tutorial: Preparing libraries for CMake FetchContent](https://www.foonathan.net/2022/06/cmake-fetchcontent/)

## Cppcon

* [Real-time Programming with the C++ Standard Library - Timur Doumler - CppCon 2021](https://www.youtube.com/watch?v=Tof5pRedskI)
