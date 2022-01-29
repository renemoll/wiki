---
title: STM32 bootstrap
description: 
published: true
date: 2022-01-29T10:42:26.607Z
tags: 
editor: markdown
dateCreated: 2022-01-28T22:38:54.482Z
---

# STM32 bootstrap

* [STM32F7 Series peripheral interconnections](https://www.st.com/resource/en/application_note/an4676-stm32f7-series-peripheral-interconnections-stmicroelectronics.pdf)
* [Level 1 cache on STM32F7 Series and STM32H7 Series](https://www.st.com/resource/en/application_note/an4839-level-1-cache-on-stm32f7-series-and-stm32h7-series-stmicroelectronics.pdf)


Input:
* [From Zero to main()](https://interrupt.memfault.com/tag/zero-to-main/)
  * [the code](https://github.com/memfault/zero-to-main)
* [A General Overview of What Happens Before main()](https://embeddedartistry.com/blog/2019/04/08/a-general-overview-of-what-happens-before-main/)
* [Exploring Startup Implementations: Newlib (ARM)](https://embeddedartistry.com/blog/2019/04/17/exploring-startup-implementations-newlib-arm/)
* [Building Bare-Metal ARM Systems with GNU: Part 1 – Getting Started](https://www.embedded.com/building-bare-metal-arm-systems-with-gnu-part-1-getting-started/)

* [Use The Tools Available](https://lefticus.gitbooks.io/cpp-best-practices/content/02-Use_the_Tools_Available.html)

## CMSIS

* [startup_<device>.c](https://arm-software.github.io/CMSIS_5/Core/html/startup_c_pg.html)
* [SystemInit](https://arm-software.github.io/CMSIS_5/Core/html/group__system__init__gr.html#ga93f514700ccf00d08dbdcff7f1224eb2)
* [Device Header File <device.h>](https://arm-software.github.io/CMSIS_5/Core/html/device_h_pg.html)
  
> determine what to re-use from CMSIS
{.is-info}

  