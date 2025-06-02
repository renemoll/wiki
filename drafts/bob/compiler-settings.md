---
title: Compiler settings
description: 
published: true
date: 2025-06-02T11:35:33.133Z
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
| Warn about (implicit) type conversions. | [`-Wconversion`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wconversion) <br>  [`-Wsign-conversion`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wsign-conversion) <br> [`-Warith-conversion`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Warith-conversion) | [`-Wconversion`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wconversion) <br>  [`-Wsign-conversion`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wsign-conversion) | `/w14242` <br> `/w14254` <br> `/w14365` <br> `/w14826` <br> `/w14388` <br> `/w14287` |
| Warn about (strict) aliasing violations. | [`-Wstrict-aliasing`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wstrict-aliasing) <br> [`-fstrict-aliasing`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Optimize-Options.html#index-fstrict-aliasing) <br> [`-Wold-style-cast`](https://gcc.gnu.org/onlinedocs/gcc/C_002b_002b-Dialect-Options.html#index-Wold-style-cast)  | [`-Wstrict-aliasing`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wstrict-aliasing) <br> [`-fstrict-aliasing`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-fstrict-aliasing) <br> [`-Wold-style-cast`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wold-style-cast) | n/a? |
| Warn whenever casting a pointer changes the alignment of the pointee. | [`-Wcast-align`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wcast-align) <br> [`-Wcast-align=strict`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wcast-align_003dstrict) | [`-Wcast-align`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wcast-align) | ? |
| Warn about casts removing type qualifiers. | [`-Wcast-qual`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wcast-qual) | [`-Wcast-qual`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wcast-qual) | ? |
| Warn about casting to the same type. | [`-Wuseless-cast`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wuseless-cast) | n/a | ? |
| Warn about (potential) use of uninitialized variables. | [`-Wtrivial-auto-var-init`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wtrivial-auto-var-init) <br> [`-ftrivial-auto-var-init=zero`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Optimize-Options.html#index-ftrivial-auto-var-init) | [`-Wconditional-uninitialized`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wconditional-uninitialized) <br> [`-ftrivial-auto-var-init=zero`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-ftrivial-auto-var-init) | ? |
| Warn about shadowing (hiding) variables. | [`-Wshadow`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wshadow) | [`-Wshadow`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wshadow) <br> [`-Wshadow-all`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wshadow-all) | `/analyze` |
| Warn about arguments not matching with a format string. | [`-Wformat=2`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wformat) | [`-Wformat=2`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wformat-2) | ? |
| Warn about format functions (potentially) truncating the output. | [`-Wformat-truncation=2`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wformat-truncation) | [`-Wformat-truncation=2`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wformat-truncation) | ? |
| Warn about duplicated branches/conditions in `if-else` expressions. | [`-Wduplicated-cond`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wno-duplicated-cond) <br> [`-Wduplicated-branches`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wno-duplicated-branches) | n/a | ? |

### C specific settings

| Goal | GCC | Clang | MSVC |
| --- | --- | --- | --- |
| Warn about missing and/or incomplete function declaration/definitions. | [`-Wmissing-prototypes`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wmissing-prototypes) <br> [`-Wmissing-declarations`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wmissing-declarations) <br> [`-Wstrict-prototypes`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wstrict-prototypes) | [`-Wmissing-prototypes`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wmissing-prototypes) <br> [`-Wmissing-declarations`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wmissing-declarations) <br> [`-Wstrict-prototypes`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wstrict-prototypes)  | ? | 
| Warn about function calls cast to a different type. | [`-Wbad-function-cast`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wbad-function-cast) | [`-Wbad-function-cast`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wbad-function-cast) <br> [`-Wcast-function-type-strict`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wcast-function-type-strict) | `/w14191` |

### C++ specific settings

| Goal | GCC | Clang | MSVC |
| --- | --- | --- | --- |

### Options

| Goal | GCC | Clang | MSVC |
| --- | --- | --- | --- |
| Enable all warnings. | n/a | [`-Weverything`](https://releases.llvm.org/20.1.0/tools/clang/docs/UsersManual.html#cmdoption-Weverything) | `/Wall` |
| Treat warnings as errors. | [`-Werror`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Werror) | [`-Werror`](https://releases.llvm.org/20.1.0/tools/clang/docs/UsersManual.html#cmdoption-Werror) | `/WX` |
| Warn about code and documentation mismatches. | n/a | [`-Wdocumentation`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wdocumentation) <br> [`-Wdocumentation-pedantic`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wdocumentation-pedantic) | ? |
