---
title: Compiler warnings
description: 
published: true
date: 2025-04-01T14:44:00.763Z
tags: 
editor: markdown
dateCreated: 2025-04-01T14:44:00.763Z
---

# Compiler warnings




### General

| Goal | GCC/Clang | MSVC | MSVC |
| --- | --- | --- |
| Enable warnings for common coding mistakes or potential errors. | [`-Wall`](https://clang.llvm.org/docs/DiagnosticsReference.html#wall)  | `/Wall` | `/W4`
|  | [`-Wextra`](https://clang.llvm.org/docs/DiagnosticsReference.html#wextra)
| Have the compiler treat warnings as errors. | [`-Werror`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html) | `/WX` | `/WX`

### Type conversion

