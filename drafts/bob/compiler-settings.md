---
title: Compiler settings
description: 
published: true
date: 2025-06-02T13:55:01.872Z
tags: 
editor: markdown
dateCreated: 2025-06-02T11:15:05.792Z
---

# TODO

* Visual Studio 2022
* latest GCC
* latest clang
* Note: `__stack_chk_fail` & `__stack_chk_guard` with `-fstack-protector-strong`


# Compiler settings

This document lists the compiler settings used by *Bob the developer*, with the goal to have the compiler check for as many potential mistakes as early on as possible.

This list is compiled by going through the compiler documentation and domain specific sources (listed in the references). 

The following assumptions are taken into account:
* Language: C17, C++17 or newer;
* Flags enabled via other flags are not explicitly mentioned unless to align different compilers;
* Flags which have no effect are still listed to avoid exceptions.

## Compiler support

| Compiler | Version |
| --- | --- |
| Clang | 20 |
| GCC | 14 |

## Settings

| Goal | GCC | Clang | MSVC |
| --- | --- | --- | --- |
| Enable warnings for common defects. | [`-Wall`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wall) <br> [`-Wextra`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-W) | [`-Wall`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wall) <br> [`-Wextra`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wextra) | `/W4` |
| Enforce standard ISO C/C++ constructions. | [`-Wpedantic`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-pedantic-1) | [`-Wpedantic`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wpedantic) <br> [`-Wgcc-compat`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wgcc-compat) <br> [`-Wgnu`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wgnu) <br> [`-Wmicrosoft`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wmicrosoft) <br> [`-Wreserved-identifier`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wreserved-identifier) <br> [`-Wformat-non-iso`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wformat-non-iso) | `/permissive-` |
| Warn about (implicit) type conversions. | [`-Wconversion`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wconversion) <br>  [`-Wsign-conversion`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wsign-conversion) <br> [`-Warith-conversion`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Warith-conversion) | [`-Wconversion`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wconversion) <br>  [`-Wsign-conversion`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wsign-conversion) | `/w14242` <br> `/w14254` <br> `/w14365` <br> `/w14826` <br> `/w14388` <br> `/w14287` |
| Warn about (strict) aliasing violations. | [`-Wstrict-aliasing`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wstrict-aliasing) <br> [`-fstrict-aliasing`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Optimize-Options.html#index-fstrict-aliasing) <br> [`-Wold-style-cast`](https://gcc.gnu.org/onlinedocs/gcc/C_002b_002b-Dialect-Options.html#index-Wold-style-cast)  | [`-Wstrict-aliasing`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wstrict-aliasing) <br> [`-fstrict-aliasing`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-fstrict-aliasing) <br> [`-Wold-style-cast`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wold-style-cast) | n/a? |
| Warn whenever casting a pointer changes the alignment of the pointee. | [`-Wcast-align`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wcast-align) <br> [`-Wcast-align=strict`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wcast-align_003dstrict) | [`-Wcast-align`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wcast-align) | ? |
| Warn about casts removing type qualifiers. | [`-Wcast-qual`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wcast-qual) | [`-Wcast-qual`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wcast-qual) | ? |
| Warn about casting to the same type. | [`-Wuseless-cast`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wuseless-cast) | n/a | ? |
| Warn about (potential) use of uninitialized variables. | [`-Wtrivial-auto-var-init`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wtrivial-auto-var-init) <br> [`-ftrivial-auto-var-init=zero`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Optimize-Options.html#index-ftrivial-auto-var-init) | [`-Wconditional-uninitialized`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wconditional-uninitialized) <br> [`-ftrivial-auto-var-init=zero`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-ftrivial-auto-var-init) | ? |
| Warn about potential null pointer dereferencing. | [`-Wnull-dereference`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wnull-dereference) | [`-Wnull-dereference`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wnull-dereference) | ? |
| Keep `NULL` pointer checks as the elemination assumptions likely do not hold. | [`-fno-delete-null-pointer-check`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Optimize-Options.html#index-fdelete-null-pointer-checks) | [`-fno-delete-null-pointer-check`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-fdelete-null-pointer-checks)
| Warn about out of bound array subscripts. | [`-Warray-bounds=2`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wno-array-bounds) | [`-Warray-bounds`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#warray-bounds) <br> [`-Warray-bounds-pointer-arithmetic`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#warray-bounds-pointer-arithmetic) | ? |
| Warn about shadowing (hiding) variables. | [`-Wshadow`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wshadow) | [`-Wshadow`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wshadow) <br> [`-Wshadow-all`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wshadow-all) | `/analyze` |
| Warn about `switch` cases not covering all possible enum values. | [`-Wswitch-enum`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wswitch-enum) | [`-Wswitch-enum`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wswitch-enum) | ? |
| Warn about implicit fall throughs. | [`-Wimplicit-fallthrough=5`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wimplicit-fallthrough) | [`-Wimplicit-fallthrough`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wimplicit-fallthrough) | ? |
| Warn about potential mistakes with logical operators. | [`-Wlogical-op`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wlogical-op) | n/a | ? |
| Warn about arguments not matching with a format string. | [`-Wformat=2`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wformat) <br> [`-Wformat-signedness`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wformat-signedness) | [`-Wformat=2`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wformat-2) <br> [`-Wformat-signedness`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wformat-signedness) <br> [`-Wformat-type-confusion`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wformat-type-confusion) | ? |
| Warn about format functions (potentially) truncating or overflowing the output string. | [`-Wformat-truncation=2`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wformat-truncation) <br> [`-Wformat-overflow=2`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wformat-overflow) | [`-Wformat-truncation=2`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wformat-truncation) | ? |
| Warn about duplicated code. | [`-Wduplicated-cond`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wno-duplicated-cond) <br> [`-Wduplicated-branches`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wno-duplicated-branches) <br> [`-Wredundant-decls`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wredundant-decls) | [`-Wredundant-decls`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wredundant-decls) | ? |
| Warn about loop variables being manipulated inside the loop or unused. | n/a | [`-Wloop-analysis`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wloop-analysis) | ? |
| Warn about floating-point values used in equality tests. | [`-Wfloat-equal`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wfloat-equal) | [`-Wfloat-equal`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wfloat-equal) | n/a |
| Warn about the use of undefined identifiers, which implicitly convert to `0`. | [`-Wundef`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wundef) | [`-Wundef`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wundef) | ? |

### C specific settings

| Goal | GCC | Clang | MSVC |
| --- | --- | --- | --- |
| Warn about missing and/or incomplete function declaration/definitions. | [`-Wmissing-prototypes`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wmissing-prototypes) <br> [`-Wmissing-declarations`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wmissing-declarations) <br> [`-Wstrict-prototypes`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wstrict-prototypes) | [`-Wmissing-prototypes`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wmissing-prototypes) <br> [`-Wmissing-declarations`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wmissing-declarations) <br> [`-Wstrict-prototypes`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wstrict-prototypes)  | ? | 
| Warn about function calls cast to a different type. | [`-Wbad-function-cast`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wbad-function-cast) | [`-Wbad-function-cast`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wbad-function-cast) <br> [`-Wcast-function-type-strict`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wcast-function-type-strict) | `/w14191` |

### C++ specific settings

| Goal | GCC | Clang | MSVC |
| --- | --- | --- | --- |
| Warn about implicit sign conversions during overload resolution. | [`-Wsign-promo`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/C_002b_002b-Dialect-Options.html#index-Wsign-promo) | [`-Wsign-promo`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wsign-promo) | ? |
| Warn about using `0` or `NULL` instead of `nullptr`. | [`-Wzero-as-null-pointer-constant`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/C_002b_002b-Dialect-Options.html#index-Wzero-as-null-pointer-constant) <br> [`-Wstrict-null-sentinel`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/C_002b_002b-Dialect-Options.html#index-Wstrict-null-sentinel) | [`-Wzero-as-null-pointer-constant`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wzero-as-null-pointer-constant) | ? |
| Warn about deprecated constructs. | n/a | [`-Wdeprecated`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wdeprecated) | ? |
| Warn about methods overwriting virtual methods not marked with `override`. | [`-Wsuggest-override`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/C_002b_002b-Dialect-Options.html#index-Wsuggest-override) | [`-Wsuggest-override`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wsuggest-override) <br> [`-Wsuggest-destructor-override`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wsuggest-destructor-override) | `/analyze` |
| Warn about methods in a derived class hiding virtual functions of the base class. | [`-Woverloaded-virtual`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/C_002b_002b-Dialect-Options.html#index-Woverloaded-virtual) | [`-Woverloaded-virtual`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#woverloaded-virtual) | `/w14263` |
| Warn about base classes without virtual destructors. | [`-Wnon-virtual-dtor`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/C_002b_002b-Dialect-Options.html#index-Wnon-virtual-dtor) | [`-Wnon-virtual-dtor`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wnon-virtual-dtor) | [`/w14265`](https://learn.microsoft.com/en-us/cpp/error-messages/compiler-warnings/compiler-warning-level-3-c4265?view=msvc-170) |
| Warn about classes which seemingly cannot be used (private constructor/destructors.) | [`-Wctor-dtor-privacy`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/C_002b_002b-Dialect-Options.html#index-Wctor-dtor-privacy) | [`-Wctor-dtor-privacy`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wctor-dtor-privacy) | ? |

### Microcontroller specific

| Goal | GCC | Clang |  
| --- | --- | --- | --- |
| Specify the target processor. | [`-mcpu=<name>`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/ARM-Options.html#index-mcpu-2) | [`-mcpu=<name>`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang1-mcpu)
| Place each function/data element into its own section to allow analysis and dead code removal. | [`-fdata-sections`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Optimize-Options.html#index-ffunction-sections) <br> [`-ffunction-sections`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Optimize-Options.html#index-ffunction-sections) | [`-fdata-sections`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-fdata-sections) <br> [`-ffunction-sections`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-ffunction-sections) |
| Remove any unused sections. | [`-Wl,--gc-sections`](https://linux.die.net/man/1/ld)  | [`-Wl,--gc-sections`](https://linux.die.net/man/1/ld) |
| Warn about single-precision values being implictly converted to double-precision values. | [`-Wdouble-promotion`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wdouble-promotion) | [`-Wdouble-promotion`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wdouble-promotion) |

### ARM Cortex-M specific

| Goal | GCC | Clang |
| --- | --- | --- |
| Generate Thumb instructions | [`-mthumb`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/ARM-Options.html#index-marm) | [`-mthumb`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-mthumb) |
| Use 'ARM Architecture Procedure Calling Standard' ABI. | [`-mabi=aapcs`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/ARM-Options.html#index-mabi-1) | [`-mabi=aapcs`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-mabi)

### Hardening

| Goal | GCC | Clang | MSVC |
| --- | --- | --- | --- |
| Follow C99 standard definition for flexible array members in a structure. | [`-fstrict-flex-arrays=3`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/C-Dialect-Options.html#index-fstrict-flex-arrays) | [`-fstrict-flex-arrays=3`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-fstrict-flex-arrays) | ? |
| Enable Stack Smashing Protector | [`-fstack-protector-strong`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Instrumentation-Options.html#index-fstack-protector-strong) | [`-fstack-protector-strong`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-fstack-protector-strong) | ? |
| Prevent stack clash attacks by limited stack allocation size. | [`-fstack-clash-protection`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Instrumentation-Options.html#index-fstack-clash-protection) | [`-fstack-clash-protection`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-fstack-clash-protection) | ? |
| Prevent code execution on the stack. | [`-fno-trampolines`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Code-Gen-Options.html#index-ftrampolines) <br> [`-Wtrampolines`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wtrampolines) <br> [`-Wl,-z,noexecstack`](https://linux.die.net/man/1/ld) <br> `-Wl,-z,noexecheap` | [`-Wl,-z,noexecstack`](https://linux.die.net/man/1/ld) <br> `-Wl,-z,noexecheap` | ? |
| Link only libraries which are specified and used. | [`-Wl,--as-needed`](https://linux.die.net/man/1/ld) <br> [`-Wl,--no-copy-dt-needed-entries`](https://linux.die.net/man/1/ld) | [`-Wl,--as-needed`](https://linux.die.net/man/1/ld) <br> [`-Wl,--no-copy-dt-needed-entries`](https://linux.die.net/man/1/ld) | ? |
| Disable lazy binding, resolve all symbols at start-up. | [`-Wl,-z,relro`](https://linux.die.net/man/1/ld) <br> [`-Wl,-z,now`](https://linux.die.net/man/1/ld)| [`-Wl,-z,relro`](https://linux.die.net/man/1/ld) <br> [`-Wl,-z,now`](https://linux.die.net/man/1/ld) | ? |

### x86

| Category | Goal | GCC | Clang |
| --- | --- | --- | --- |
| Verify target addresses of control-flow transfer instructions are valid. | [`-fcf-protection=full`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Instrumentation-Options.html#index-fcf-protection) | [`-fcf-protection=full`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-fcf-protection) | ? |

### Options

| Goal | GCC | Clang | MSVC |
| --- | --- | --- | --- |
| Enable all warnings. | n/a | [`-Weverything`](https://releases.llvm.org/20.1.0/tools/clang/docs/UsersManual.html#cmdoption-Weverything) | `/Wall` |
| Treat warnings as errors. | [`-Werror`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Werror) | [`-Werror`](https://releases.llvm.org/20.1.0/tools/clang/docs/UsersManual.html#cmdoption-Werror) | `/WX` |
| Warn about code and documentation mismatches. | n/a | [`-Wdocumentation`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wdocumentation) <br> [`-Wdocumentation-pedantic`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wdocumentation-pedantic) | ? |

## Omitted

* Omitting `-fstack-check` in favor of `-fstack-clash-protection` ([Stack clash mitigation in GCC, Part 3](https://developers.redhat.com/blog/2020/05/22/stack-clash-mitigation-in-gcc-part-3))

## References

1. [Diagnostic flags in Clang](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html)
1. [Clang command line argument reference](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html)
1. GCC - [Options to Request or Suppress Warnings](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html)
1. GCC - [Options Controlling C++ Dialect](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/C_002b_002b-Dialect-Options.html)
1. [What is the Strict Aliasing Rule and Why do we care?](https://gist.github.com/shafik/848ae25ee209f698763cffee272a58f8)
1. [Compiler Options Hardening Guide for C and C++](https://best.openssf.org/Compiler-Hardening-Guides/Compiler-Options-Hardening-Guide-for-C-and-C++.html)
1. [-fstack-protector, -fstack-protector-all, -fstack-protector-strong, -fno-stack-protector](https://developer.arm.com/documentation/dui0774/l/Compiler-Command-line-Options/-fstack-protector---fstack-protector-all---fstack-protector-strong---fno-stack-protector)
