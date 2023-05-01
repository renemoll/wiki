---
title: C (runtime) library
description: 
published: true
date: 2023-05-01T20:07:59.784Z
tags: 
editor: markdown
dateCreated: 2023-01-31T20:19:03.970Z
---

# C runtime & library

## What is this "runtime"

1. https://en.wikipedia.org/wiki/Runtime_library

## What is this "library"



## Available/common options

* newlib
C & math library combined with board support package (libgloss)
* newlib-nano
* redlib (NXP)
* avr-libc

Commercial 
* [emRun](https://www.segger.com/products/development-tools/runtime-library/)
C library

others
* [embedded artistry](https://github.com/embeddedartistry/libc)

Bionic libc -> Android
dietlibc -> (embedded) Linux
glibc -> Linux
klibc -> Linux
musl -> (embedded) Linux
uClibc, now uClibc-ng -> embedded Linux

## not using a library

can be an option, does mean no standard functions will be available.

# ref

1. https://en.wikipedia.org/wiki/Crt0
1. https://sourceware.org/newlib/libgloss.html
1. [ARM Cortex-M Run-Time Library Analysis](https://www.purposeful.co.uk/arm_rtabi/ARMv7M__aeabi_lmul.html)
1. [The C Runtime Initialization, crt0.o](https://www.embecosm.com/appnotes/ean9/html/ch05s02.html)
1. [My review of the C standard library in practice](https://nullprogram.com/blog/2023/02/11/)


# C libraries for embedded

The C and C++ standards define various functions you can use within your application. These are
implemented in a standard library. Gennerally refered to as libc/libc++, there are various
implementations. Such as: glibc (GNU C library) or UCRT (Universal C Run Time) [1]. 

The common implementations, such as glibc and UCRT, are designed with desktop use in mind. With
less focus on resource constrained environments, such as microcontrollers. Fortuantly, various
implementations are available specifically designed with microcontrollers in mind.

Some examples include:
* newlib
* newlib-nano
* picolibc
* Embedded Warrior Library (NXP)
* "SEGGER"
* "Redlib"

Some are proprietary libraries provided by microcontroller vendors, others are open-source. When 
you compile code for ARM Cortex-M devices, by default compiler will select newlib for you. 


newlib-nano:
 * removed support for printing/scanning floating point numbers (i.e. %f format support)
   note: gennerally this feature can be re-enabled explicitly.



References
1. https://en.wikipedia.org/wiki/C_standard_library#Implementations
https://mcuoneclipse.com/2023/01/28/which-embedded-gcc-standard-library-newlib-newlib-nano/

# Integrating a C library

* https://hackaday.com/2021/07/19/the-newlib-embedded-c-standard-library-and-how-to-use-it/
* https://sourceware.org/newlib/libc.html#Stubs
* Do it yourself
* libgloss?


# Freestanding

https://en.wikipedia.org/wiki/C_standard_library#Detection
