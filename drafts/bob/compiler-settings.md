---
title: Compiler settings
description: 
published: true
date: 2025-06-02T11:15:05.792Z
tags: 
editor: markdown
dateCreated: 2025-06-02T11:15:05.792Z
---

# TODO

* Visual Studio 2022
* latest GCC
* latest clang

# Compiler settings

This document lists the compiler settings used by *Bob the developer*, with the goal to have the compiler check for as many potential mistakes as early on as possible.

This list is compiled by going through the compiler documentation and domain specific sources (listed in the references). 

The following assumptions are taken into account:
* Language: C17, C++17 or newer;
* Flags enabled via other flags are not explicitly mentioned unless to align different compilers.

## Compiler support

| Compiler | Version |
| --- | --- |
| Clang | 20 |
| GCC | 14 |

## Settings

| Goal | GCC | Clang | MSVC | 
| --- | --- | --- | --- |
| Enable warnings for common defects. | [`-Wall`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wall) <br> [`-Wextra`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-W) | [`-Wall`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wall) <br> [`-Wextra`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wextra) | `/W4` |
| Enforce standard ISO C/C++ constructions. | [`-Wpedantic`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-pedantic-1) | [`-Wpedantic`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wpedantic) <br> [`-Wgcc-compat`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wgcc-compat) <br> [`-Wgnu`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wgnu) <br> [`-Wmicrosoft`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wmicrosoft) <br> [`-Wreserved-identifier`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wreserved-identifier)| `/permissive-` |
| Warn about (implicit) type conversions. | [`-Wconversion`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wconversion) <br>  [`-Wsign-conversion`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wsign-conversion) | [`-Wconversion`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wconversion) <br>  [`-Wsign-conversion`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wsign-conversion) | `/w14242` <br> `/w14254` <br> `/w14365` <br> `/w14826` |

