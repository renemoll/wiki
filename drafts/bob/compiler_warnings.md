---
title: Compiler warnings
description: 
published: true
date: 2025-04-01T14:54:35.518Z
tags: 
editor: markdown
dateCreated: 2025-04-01T14:44:00.763Z
---

# Compiler warnings




### General

| Goal | GCC | Clang | MSVC | MSVC |
| --- | --- | --- |--- |
| Enable warnings for common coding mistakes and/or potential errors. | [`-Wall`](https://clang.llvm.org/docs/DiagnosticsReference.html#wall) \ | [`-Wall`](https://clang.llvm.org/docs/DiagnosticsReference.html#wall) \ | `/Wall` | `/W4` \
|  | [`-Wextra`](https://clang.llvm.org/docs/DiagnosticsReference.html#wextra) |  [`-Wextra`](https://clang.llvm.org/docs/DiagnosticsReference.html#wextra)
| Have the compiler treat warnings as errors. | [`-Werror`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html) | [`-Werror`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html) | `/WX` | `/WX`
| Enforce standard ISO C/C++ constructions. | [`-Wpedantic`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html) | [`-Wpedantic`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html) | `/permissive-` | `/permissive-`

### Type conversion

