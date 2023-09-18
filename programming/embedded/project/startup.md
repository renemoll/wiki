---
title: start-up
description: 
published: true
date: 2023-09-18T20:20:47.985Z
tags: 
editor: markdown
dateCreated: 2023-09-18T18:47:56.505Z
---

# startup


Goal: start-up code

Must be:
* small footprint
* fast*
* readable/maintainable
* customizable

* fast is tricky on certain MCUs, especially the STM32F7 I am working with.

## Existing solutions

Cortex-M0/M0+/M1 -> ARMv6-M
Cortex-M3/M4/M7 -> ARMv7-M / ARMv7E-M
Cortex-M23/33/55/85 -> ARMv8-M


### libraries

* newlib
* newlib-nano
* picolibc
* modm
* ...

### RTOS

https://en.wikipedia.org/wiki/ARM_architecture_family#Embedded_operating_systems
https://en.wikipedia.org/wiki/Comparison_of_real-time_operating_systems
* open-source
* cortex-m



| OS | Code |
| --- | --- |
| ChibiOS/RT | |
| FreeRTOS | Uses STM/CMSIS start-up code. |
| mbed-OS | Uses STM/CMSIS start-up code. | 
| NuttX | [vector table](https://github.com/apache/nuttx/blob/master/arch/arm/src/armv7-m/arm_vectors.c), [start-up](https://github.com/apache/nuttx/blob/master/arch/arm/src/stm32f7/stm32_start.c) |
| RIOT | [reset handler](https://github.com/RIOT-OS/RIOT/blob/master/cpu/cortexm_common/vectors_cortexm.c)
| rtthread | Uses STM/CMSIS start-up code. | 
| ThreadX | [start-up](https://github.com/azure-rtos/threadx/blob/master/ports/cortex_m7/gnu/example_build/cortexm7_crt0.S)




#### NuttX
* Reset MPU
* Clear BSS (inline C)
 > unclear if optimized by compiler
* Copy data (inline C)
 > unclear if optimized by compiler
* Optinal: copy function to RAM
* Clock config
* FPU config
* Optional: enable UART
* Enable TC memory
* Enable caches
* Optional: enable system log (ITM)
* Optional: initialize user-space

#### RIOT
* enable FPU
* clear bss
* copy data
* set VTOR
* setup NVIC priorties
* enable wake-up from WFE
* initialize clock / peripherals
* __libc_init_array

#### ThreadX

(all assembly)
* Clear BSS
* Copy data
* call static constructors

## Theory / background

info on
* crtbegin/crtend etc...
* TLS
