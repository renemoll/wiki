---
title: start-up
description: 
published: true
date: 2023-09-25T20:35:11.005Z
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

# Theory / background

Going through linkerscripts, and maybe even low-level initialization code provided by a libc implementations, you may run into the following

init: https://github.com/eblot/newlib/blob/master/newlib/libc/misc/init.c
fini: https://github.com/eblot/newlib/blob/master/newlib/libc/misc/fini.c

You may find resources discussion .ctors/dtors, crtbegin/crtend, crti/crtn...

And begin to wonder, what is all this, what is it for and is it even relevant?


All have to do with initialization before `main` is called and finalization after main returns.


There seem to be N groups:

- .ctors/.dtors -> list of constructors/destructors
- init/fini
- .init_array/.fini_array

> where does crtbegin/crtend, crti/crtn fit in?

[GCC intenals](https://gcc.gnu.org/onlinedocs/gccint/Initialization.html)
* The linker must build two lists of these functions—a list of initialization functions, called `__CTOR_LIST__`, and a list of termination functions, called `__DTOR_LIST__`.
Four variants:
#. arbitrary sections: on systems that support a .init section (`crtstuff.c `) (`INIT_SECTION_ASM_OP`)
#. arbitrary sections:  the `__main` function is defined in `libgcc2.c` and runs the global constructors.
#. no arbitrary sections: fucntion pointer list in a special section (`TARGET_ASM_CONSTRUCTOR`)
#. no arbitrary sections: no special section: These functions are called via __main as described above. In order to use this method, use_collect2 must be defined in the target in config.gcc. 

target-def.h
#. `TARGET_ASM_NAMED_SECTION` / `CTORS_SECTION_ASM_OP` / `DTORS_SECTION_ASM_OP`
#. `INIT_SECTION_ASM_OP`
#. `INIT_SECTION_ASM_OP` = false, `TARGET_ASM_CONSTRUCTOR` list
#. `TARGET_HAVE_CTORS_DTORS` = false

* `TARGET_ASM_NAMED_SECTION`: no real effect
* `CTORS_SECTION_ASM_OP` / `DTORS_SECTION_ASM_OP`
* `INIT_SECTION_ASM_OP`
* `TARGET_ASM_CONSTRUCTOR`
* `TARGET_HAVE_CTORS_DTORS`

* `USE_INITFINI_ARRAY`, when enabled:
  * disables:
    * `INIT_SECTION_ASM_OP` / `FINI_SECTION_ASM_OP`
  * enables:
    * `INIT_ARRAY_SECTION_ASM_OP` / `FINI_ARRAY_SECTION_ASM_OP`
    * `TARGET_ASM_CONSTRUCTOR` / `TARGET_ASM_DESTRUCTOR`

* crti
  * `.init` section with `_init` function prelouge 



* crtn
  * `.fini` section with `_fini` function epilouge 



Before an application is executed, it may require initialization. Same when it terminates. 

## background

https://maskray.me/blog/2021-11-07-init-ctors-init-array

[System V Application Binary Interface](https://www.sco.com/developers/gabi/latest/contents.html)
* brief intro on the sections: https://www.sco.com/developers/gabi/latest/ch4.sheader.html#special_sections
								https://www.sco.com/developers/gabi/latest/ch5.dynamic.html#dynamic_section



.init initialization instructions
.fini termination instructions

.pre_initarray, list of pre-initialization functions
.init_array, list of initialization functions
.fini_array, list of termination functions

.ctors
.dtors
> removed -> https://gcc.gnu.org/bugzilla/show_bug.cgi?id=46770


## How to trigger it

1. natural occourance
1. compiler arguments & extensions/attributes


* https://docs.oracle.com/cd/E19683-01/816-1386/6m7qcobkh/index.html#chapter2-48195
The registration of initialization and termination functions can be carried out directly by the link-editor using the -z initarray and -z finiarray options


## How to initialize it

Linker tags these sections with: DT_PREINIT_ARRAY and DT_PREINIT_ARRAYSZ, DT_INIT_ARRAY and DT_INIT_ARRAYSZ, and DT_FINI_ARRAY and DT_FINI_ARRAYSZ, DT_INIT and DT_FINI  (usefull?)

On a computer with an OS, the OS takes care of calling all the init/fini related code.

On a MCU we don't have that luxery. either we avoid needing this. or we perform the initialization.

* https://docs.oracle.com/cd/E19683-01/816-1386/6m7qcobkh/index.html#chapter2-48195
* https://docs.oracle.com/cd/E19683-01/816-1386/6m7qcobks/index.html
* https://refspecs.linuxbase.org/elf/gabi4+/ch5.dynamic.html



## Thread local storage


.tbss
This section holds uninitialized thread-local data that contribute to the program's memory image. By definition, the system initializes the data with zeros when the data is instantiated for each new execution flow. The section occupies no file space, as indicated by the section type, SHT_NOBITS. Implementations need not support thread-local storage.
.tdata
This section holds initialized thread-local data that contributes to the program's memory image. A copy of its contents is instantiated by the system for each new execution flow. Implementations need not support thread-local storage.