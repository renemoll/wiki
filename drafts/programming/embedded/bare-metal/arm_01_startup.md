---
title: ARM booting
description: 
published: true
date: 2023-05-22T20:41:48.834Z
tags: 
editor: markdown
dateCreated: 2023-01-31T20:31:06.925Z
---

# ARM booting

1. starts with hardware

	Booting your MCU starts with some electronic design. The MCU needs to be provided with power,
the reset line held in a certain level, maybe some boot pin can be used to configure the initial MCU execution.

1. execution of reset handler

	The first handler

1. hardware initialization
1. memory initialization
1. initialization of the C environment

# 3 parts

1. MCU boot
1. C runtime
1. C++ runtime

Examples: STM32F7, NXP flashless? AVR ATmega8?

# MCU boot



# C runtime environment

Section 5.1.2
> Two execution environments are defined: *freestanding* and *hosted*. In both cases, program startup occurs when a designated C function is called by the execution environment. All objects with static storage duration shall be initialized (set to their initial values) before program startup. 

Section 4
> The two forms of conforming implementation are hosted and freestanding. A conforming hosted implementation shall accept any strictly conforming program. A conforming freestanding implementation shall accept any strictly conforming program in which the use of the features specified in the library clause (Clause 7) is confined to the contents of the standard headers <float.h>, <iso646.h>, <limits.h>, <stdalign.h>, <stdarg.h>, <stdbool.h>, <stddef.h>, <stdint.h>, and <stdnoreturn.h>. A conforming implementation may have extensions (including additional library functions), provided they do not alter the behavior of any strictly conforming program.4)

[C17](https://www.open-std.org/jtc1/sc22/wg14/www/docs/n2310.pdf)

* <float.h>: macros for limits/constraint/parameters for floats
* <iso646.h>: macros for operators
* <limits.h>: macros for limits/contrains/parameters for integers
* <stdalign.h>: macros for alignment?
* <stdarg.h>: macros for variable argument lists
* <stdbool.h>: macros to define booleans
* <stddef.h>: common types
* <stdint.h>: defines various integers types
* <stdnoreturn.h>: defines the no-return macro

Note: these headers only define language elements. No library functions are defined.
Yet, any freestanding library may implement library functions.
 -> depends on library/compiler?
 -> for example, GCC provides a large number of build in functions which it will provide. https://gcc.gnu.org/onlinedocs/gcc/Other-Builtins.html
 -> Clang provides a number of memory operation functions https://clang.llvm.org/docs/CommandGuide/clang.html

> In a freestanding environment (in which C program execution may take place without any benefit of an operating system), the name and type of the function called at program startup are implementation-defined. Any library facilities available to a freestanding program, other than the minimal set
required by Clause 4, are implementation-defined.

Hosted implementations are required to have a `main` function, freestanding might differ. 

Differences
* the library may depend on functionality provided by an operating system, such as opening a file or manipulating memory.



* storage durations of objects (6.2.4), 
* initialization (6.7.9).

Why would you use freestanding?

* https://en.cppreference.com/w/cpp/freestanding

Example
https://sourceware.org/newlib/libc.html#Stubs
Newlib library lists which system calls should be provided to make the library work. Options: no standard library (provide your own stubs), 

* linux
* nosys: stubbed system calls
* nano: 
* pid
* rdimon: semihost
* rdpmon
* redboot

# C++ runtime environment

# ref

* check older notes
* https://www.embedded.com/building-bare-metal-arm-systems-with-gnu-part-1-getting-started/
* https://www.amazon.com/dp/0750676094
* https://github.com/payne92/bare-metal-arm
* https://github.com/micro-os-plus/micro-os-plus-iii/blob/xpack/src/startup/exception-handlers.c
* https://github.com/zephyrproject-rtos/zephyr/tree/main/arch/arm/core/aarch32/cortex_m
* https://github.com/modm-io/modm/blob/develop/src/modm/platform/core/stm32/startup_platform.c.in