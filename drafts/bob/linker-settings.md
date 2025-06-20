---
title: Linker settings
description: 
published: true
date: 2025-06-20T14:33:03.170Z
tags: 
editor: markdown
dateCreated: 2025-06-20T14:29:31.559Z
---

# TODO

* MSVC

# Linker settings

## Settings

| Goal | GCC/Clang | MSVC |
| --- | --- | --- |
| Print out a memory usage summary after linking | `--print-memory-usage` | ? |
| Generate a cross reference table to determine declaration and use of symbols | [`--cref`](https://linux.die.net/man/1/ld) | ? |

### Microcontroller specific

| Goal | GCC/Clang |
| --- | --- |
| Remove any unused sections (code/data). | [`-Wl,--gc-sections`](https://linux.die.net/man/1/ld) |

### Hardening

| Goal | GCC/Clang | MSVC |
| --- | --- | --- |
| Prevent code execution on the stack. | [`-Wl,-z,noexecstack`](https://linux.die.net/man/1/ld) <br> `-Wl,-z,noexecheap` | ? |
| Link only libraries which are specified and used. | [`-Wl,--as-needed`](https://linux.die.net/man/1/ld) <br> [`-Wl,--no-copy-dt-needed-entries`](https://linux.die.net/man/1/ld) | ? |
| Disable lazy binding, resolve all symbols at start-up. | [`-Wl,-z,relro`](https://linux.die.net/man/1/ld) <br> [`-Wl,-z,now`](https://linux.die.net/man/1/ld) | ? |