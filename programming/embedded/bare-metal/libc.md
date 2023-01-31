---
title: C (runtime) library
description: 
published: true
date: 2023-01-31T20:53:09.904Z
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
* embedded artistry

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
1. https://www.purposeful.co.uk/arm_rtabi/ARMv7M__aeabi_lmul.html
1. https://www.embecosm.com/appnotes/ean9/html/ch05s02.html