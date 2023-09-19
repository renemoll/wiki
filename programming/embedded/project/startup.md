---
title: start-up
description: 
published: true
date: 2023-09-19T20:35:36.595Z
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
* CMSIS
* STM
* ...

| lib | code |
| --- | --- |
| CMSIS | [startup_ARMCM7.S](https://github.com/ARM-software/CMSIS_5/blob/develop/Device/ARM/ARMCM7/Source/GCC/startup_ARMCM7.S), [system_ARMCM7.c](https://github.com/ARM-software/CMSIS_5/blob/develop/Device/ARM/ARMCM7/Source/system_ARMCM7.c) |
| newlib / newlib-nano | [crt0.S](https://github.com/bminor/newlib/blob/master/libgloss/arm/crt0.S) |
| picolibc | [crt0.c](https://github.com/picolibc/picolibc/blob/main/picocrt/machine/arm/crt0.c), [crt0.h](https://github.com/picolibc/picolibc/blob/main/picocrt/crt0.h) |
| STM | cmsis_device_f7 |
| modm | (?) |

#### CMSIS

* copy data
* zero bss
* set VTOR
* enable FPU
* UNALIGNED_SUPPORT_DISABLE (SCB->CCR)

#### newlib / newlib-nano / libgloss

* zero BSS
* call init/fini

#### modm

* set main stack pointer
* enable FPU
* enable TCMs
* copy data
* zero bss
* enable I cache
* set VTOR
* SCB_CCR_DIV_0_TRP_Msk
* call __init_array_start



#### picolibc

* configure FPU
* copy data
* clear bss
* TLS
* __libc_init_array

#### STM

* copy data
* zero bss
* enable FPU
* set VTOR 
* __libc_init_array

### RTOS

https://en.wikipedia.org/wiki/ARM_architecture_family#Embedded_operating_systems
https://en.wikipedia.org/wiki/Comparison_of_real-time_operating_systems
* open-source
* cortex-m



| OS | Code |
| --- | --- |
| ChibiOS/RT | crt0_v7m.s |
| Contiki-NG | Uses CMSIS start-up code. |
| FreeRTOS | Uses STM/CMSIS start-up code. |
| mbed-OS | Uses STM/CMSIS start-up code. | 
| NuttX | [vector table](https://github.com/apache/nuttx/blob/master/arch/arm/src/armv7-m/arm_vectors.c), [start-up](https://github.com/apache/nuttx/blob/master/arch/arm/src/stm32f7/stm32_start.c) |
| RIOT | [reset handler](https://github.com/RIOT-OS/RIOT/blob/master/cpu/cortexm_common/vectors_cortexm.c)
| rtthread | Uses STM/CMSIS start-up code. | 
| ThreadX | [start-up](https://github.com/azure-rtos/threadx/blob/master/ports/cortex_m7/gnu/example_build/cortexm7_crt0.S)


#### ChibiOS

* disable interrupts
* optional: set main&process stack pointer
* optional: set VTOR
* optional: enable & configure FPU
* optional: enable caches
* init gpio & clock
* optional: fill stack spaces
* optional: copy irq vector table
* optional: clear BSS
* optional: copy data
* optional: init RAM (copy / clear)
* optional: call init/fini

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
