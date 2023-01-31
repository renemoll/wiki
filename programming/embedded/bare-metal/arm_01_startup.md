---
title: ARM booting
description: 
published: true
date: 2023-01-31T20:54:23.228Z
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


# ref

* check older notes
* https://www.embedded.com/building-bare-metal-arm-systems-with-gnu-part-1-getting-started/
* https://www.amazon.com/dp/0750676094
* https://github.com/payne92/bare-metal-arm
* https://github.com/micro-os-plus/micro-os-plus-iii/blob/xpack/src/startup/exception-handlers.c
* https://github.com/zephyrproject-rtos/zephyr/tree/main/arch/arm/core/aarch32/cortex_m
* https://github.com/modm-io/modm/blob/develop/src/modm/platform/core/stm32/startup_platform.c.in