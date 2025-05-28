---
title: Compiler warnings
description: 
published: true
date: 2025-05-28T13:03:48.921Z
tags: 
editor: markdown
dateCreated: 2025-04-01T14:44:00.763Z
---

# Compiler settings

This document lists the compiler settings used by *Bob the developer*, with the goal to have the compiler check for as many potential mistakes as early on as possible.

This list is compiled by going through the compiler documentation and domain specific sources (listed in the references). 

The following assumptions are taken into account:
* Language: C17, C++17 or newer;
* Flags enabled via other flags are not explicitly mentioned unless to align different compilers.

## Compilers

| Compiler | Version |
| --- | --- |
| Clang | 20 |
| GCC | 14 |

> TODO: update for Visual Studio 2022

## Settings

| Category | Goal | GCC | Clang | MSVC | 
| --- | --- | --- | --- | --- |
| Aliasing | Warn about (strict) aliasing violations. | [`-Wstrict-aliasing`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Optimize-Options.html#index-Wstrict-aliasing) <br> [`-fstrict-aliasing`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Optimize-Options.html#index-fstrict-aliasing) <br> [`-Wold-style-cast`](https://gcc.gnu.org/onlinedocs/gcc/C_002b_002b-Dialect-Options.html#index-Wold-style-cast)  | [`-Wstrict-aliasing`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wstrict-aliasing) <br> [`-fstrict-aliasing`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-fstrict-aliasing) <br> [`-Wold-style-cast`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wold-style-cast) | n/a? |
| Aliasing | Warn whenever casting a pointer changes the alignment of the pointee. | [`-Wcast-align`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Optimize-Options.html#index-Wcast-align) <br> [`-Wcast-align=strict`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Optimize-Options.html#index-Wcast-align_003dstrict) | [`-Wcast-align`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wcast-align) | ? |
| Common defects | Enable warnings for common defects. | [`-Wall`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wall) <br> [`-Wextra`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-W) | [`-Wall`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wall) <br> [`-Wextra`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wextra) | `/W4` |
| Common defects | Warn about local variables shadowing (hiding) another variable. | [`-Wshadow`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wshadow) | [`-Wshadow`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wshadow) <br> [`-Wshadow-all`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wshadow-all) | `/analyze` |
| Common defects | Warn about duplicated conditions in `if-else` expressions. | [`-Wduplicated-cond`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wno-duplicated-cond) | n/a | ? |
| Common defects | Warn about identical branches in `if-else` expressions. | [`-Wduplicated-branches`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wno-duplicated-branches) | n/a | ? |
| Common defects | Warn about duplicated declarations within the same scope. | [`-Wredundant-decls`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wredundant-decls) | n/a | ? |
| Common defects | Warn about `switch` cases not covering all possible enum values. | [`-Wswitch-enum`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wswitch-enum) | [`-Wswitch-enum`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wswitch-enum) | ? |
| Common defects | Warn about possible null pointer dereferencing. | [`-Wnull-dereference`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wnull-dereference) | [`-Wnull-dereference`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wnull-dereference) | ? |
| Common defects | Warn about the use of undefined identifiers, which implicitly convert to 0. | [`-Wundef`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wundef) | [`-Wundef`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wundef) | ? |
| Common defects | Warn about potential mistakes with logical operators. | [`-Wlogical-op`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wlogical-op) | n/a | ? |
| Common defects | Warn about out of bound array subscripts. | [`-Warray-bounds=2`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wno-array-bounds) | [`-Warray-bounds`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#warray-bounds) <br> [`-Warray-bounds-pointer-arithmetic`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#warray-bounds-pointer-arithmetic) | ? |
| Common defects | Warn about (potential) use of uninitialized variables. | [`-Wtrivial-auto-var-init`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wtrivial-auto-var-init) <br> [`-ftrivial-auto-var-init=zero`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Optimize-Options.html#index-ftrivial-auto-var-init) | [`-Wconditional-uninitialized`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wconditional-uninitialized) | ? |
| Common defects | Warn about loop variables being manipulated inside the loop or unused. | n/a | [`-Wloop-analysis`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wloop-analysis) | ? |
| Common defects | Warn about floating-point values used in equality tests. | [`-Wfloat-equal`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wfloat-equal) | [`-Wfloat-equal`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wfloat-equal) | n/a |
| Common defects | Ensure global variables are not merged into a single element, causing a multiple declaration error | `-fno-common` | `-fno-common` | ? |
| Modernisation | Warn about implicit fall throughs. | [`-Wimplicit-fallthrough=5`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wimplicit-fallthrough) | [`-Wimplicit-fallthrough`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wimplicit-fallthrough) | ? |
| Portability | Enforce standard ISO C/C++ constructions. | [`-Wpedantic`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Optimize-Options.html#index-pedantic-1) | [`-Wpedantic`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#cmdoption-pedantic) <br> [`-Wgcc-compat`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wgcc-compat) <br> [`-Wgnu`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wgnu) <br> [`-Wmicrosoft`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wmicrosoft) <br> [`-Wreserved-identifier`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wreserved-identifier)| `/permissive-` |
| String format | Warn about arguments not matching with a format string. | [`-Wformat=2`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Optimize-Options.html#index-Wformat) | [`-Wformat=2`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wformat-2) | ? |
| String format | Warn about format functions (potentially) truncating the output. | [`-Wformat-truncation=2`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Optimize-Options.html#index-Wformat-truncation) | [`-Wformat-truncation=2`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wformat-truncation) | ? |
| Type conversion | Warn about (implicit) type conversions. | [`-Wconversion`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Optimize-Options.html#index-Wconversion) <br>  [`-Wsign-conversion`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Optimize-Options.html#index-Wsign-conversion) | [`-Wconversion`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wconversion) <br>  [`-Wsign-conversion`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wsign-conversion) | `/w14242` <br> `/w14254` <br> `/w14365` <br> `/w14826` |
| Type conversion | Warn about implicit type conversions with arithmetic operations. | [`-Warith-conversion`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Optimize-Options.html#index-Warith-conversion) | n/a | `/w14388` <br> `/w14287` |
| Type conversion | Warn about casts which remove type qualifiers. | [`-Wcast-qual`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Optimize-Options.html#index-Wcast-qual) | [`-Wcast-qual`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wcast-qual) | ? |
| Type conversion | Warn about casting to the same type. | [`-Wuseless-cast`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wuseless-cast) | n/a | ? |

### C specific
| Category | Goal | GCC | Clang | MSVC | 
| --- | --- | --- | --- |--- |
| Modernisation | Warn about missing and/or incomplete function declaration/definitions. | [`-Wmissing-prototypes`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wmissing-prototypes) <br> [`-Wmissing-declarations`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wmissing-declarations) <br> [`-Wstrict-prototypes`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Optimize-Options.html#index-Wstrict-prototypes) | [`-Wstrict-prototypes`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wstrict-prototypes)  | ? | 
| Type conversion | Warn about function calls cast to a different type. | [`-Wbad-function-cast`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Optimize-Options.html#index-Wbad-function-cast) | [`-Wbad-function-cast`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wbad-function-cast) <br> [`-Wcast-function-type-strict`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wcast-function-type-strict) | `/w14191` |




### C++ specific
| Category | Goal | GCC | Clang | MSVC | 
| --- | --- | --- | --- |--- |
| Modernisation | Warn about deprecated constructs. | [`-Wdeprecated`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Optimize-Options.html#index-Wno-deprecated) | [`-Wdeprecated`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wdeprecated) | ? |
| Modernisation | Warn about using 0 as a `null` pointer. | [`-Wzero-as-null-pointer-constant`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Optimize-Options.html#index-Wzero-as-null-pointer-constant) | [`-Wzero-as-null-pointer-constant`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wzero-as-null-pointer-constant) | ? |
| Modernisation | Warn about the use of `NULL` (instead of `nullptr`.) | [`-Wstrict-null-sentinel`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/C_002b_002b-Dialect-Options.html#index-Wstrict-null-sentinel) | n/a | ? |
| OOP | Warn about base classes without virtual destructors. | [`-Wnon-virtual-dtor`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/C_002b_002b-Dialect-Options.html#index-Wnon-virtual-dtor) | [`-Wnon-virtual-dtor`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wnon-virtual-dtor) | [`/w14265`](https://learn.microsoft.com/en-us/cpp/error-messages/compiler-warnings/compiler-warning-level-3-c4265?view=msvc-170) |
| OOP | Warn about classes which seemingly cannot be used (private constructor/destructors.) | [`-Wctor-dtor-privacy`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/C_002b_002b-Dialect-Options.html#index-Wctor-dtor-privacy) | [`-Wctor-dtor-privacy`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wctor-dtor-privacy) | ? |
| OOP | Warn about methods overwriting virtual methods not marked with `override`. | [`-Wsuggest-override`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/C_002b_002b-Dialect-Options.html#index-Wsuggest-override) | [`-Wsuggest-override`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wsuggest-override) <br> [`-Wsuggest-destructor-override`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wsuggest-destructor-override) | `/analyze` |
| OOP | Warn about methods in a derived class hiding virtual functions of the base class. | [`-Woverloaded-virtual`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/C_002b_002b-Dialect-Options.html#index-Woverloaded-virtual) | [`-Woverloaded-virtual`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#woverloaded-virtual) | `/w14263` |

`-Wsign-promo`

### Options

| Category | Goal | GCC | Clang | MSVC |
| --- | --- | --- | --- | --- |
| Documentation | Warn about code and documentation mismatches. | n/a | [`-Wdocumentation`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wdocumentation) <br> [`-Wdocumentation-pedantic`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wdocumentation-pedantic) | ? |
| Misc | Enable all warnings. | n/a | [`-Weverything`](https://releases.llvm.org/20.1.0/tools/clang/docs/UsersManual.html#cmdoption-Weverything) | `/Wall` |
| Misc | Treat warnings as errors. | [`-Werror`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Optimize-Options.html#index-Werror) | [`-Werror`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#cmdoption-Werror) | `/WX` |

### Microcontroller specific

| Category | Goal | GCC | Clang |  
| --- | --- | --- | --- |
| Type conversion | Warn about single-precision values being implictly converted to double-precision values. | [`-Wdouble-promotion`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wdouble-promotion) | [`-Wdouble-promotion`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wdouble-promotion) |

## Code generation




### Hardening

| Category | Goal | GCC | Clang | MSVC |
| --- | --- | --- | --- |--- |
| Common defects | Follow C99 standard definition for flexible array members in a structure. | [`-fstrict-flex-arrays=3`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/C-Dialect-Options.html#index-fstrict-flex-arrays) | [`-fstrict-flex-arrays=3`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-fstrict-flex-arrays) | ? |
| Common defects | Stack Smashing Protector | [`-fstack-protector-strong`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Instrumentation-Options.html#index-fstack-protector-strong) | [`-fstack-protector-strong`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-fstack-protector-strong) | ? |
| ? | | [`-fstack-clash-protection`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Instrumentation-Options.html#index-fstack-clash-protection) | [`-fstack-clash-protection`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-fstack-clash-protection) | ? |
| ? | | [`-fcf-protection=full`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Instrumentation-Options.html#index-fcf-protection) | [`-fcf-protection=full`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-fcf-protection) | ? |
| ? | Don't allow executing code from the stack. | [`-Wtrampolines`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wtrampolines) <br> `-Wl,-z,noexecstack` <br> `-Wl,-z,noexecheap` | ? | ? |


> Note: `__stack_chk_fail` & `__stack_chk_guard` with `-fstack-protector-strong`
> -fstack-protector-all?

### Microcontroller specific

| Category | Goal | GCC | Clang |
| --- | --- | --- | --- |
| ARM Cortex-M | Generate Thumb instructions | [`-mthumb`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/ARM-Options.html#index-marm) | [`-mthumb`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-mthumb) |
| ARM Cortex-M | Use 'ARM Architecture Procedure Calling Standard' ABI. | [`-mabi=aapcs`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/ARM-Options.html#index-mabi-1) | [`-mabi=aapcs`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-mabi)
| ARM Cortex-M | Specify the target processor. | [`-mcpu=<name>`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/ARM-Options.html#index-mcpu-2) | [`-mcpu=<name>`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang1-mcpu)
| Optimization | Place each function/data element into its own section | [`-fdata-sections`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Optimize-Options.html#index-ffunction-sections) <br> [`-ffunction-sections`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Optimize-Options.html#index-ffunction-sections) | [`-fdata-sections`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-fdata-sections) <br> [`-ffunction-sections`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-ffunction-sections) |
| Optimization | Do not remove `NULL` pointer checks as the assumptions likely do not hold. | [`-fno-delete-null-pointer-check`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Optimize-Options.html#index-fdelete-null-pointer-checks) | [`-fno-delete-null-pointer-check`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-fdelete-null-pointer-checks)


### Library specific

| Library | Option | Goal |
| --- | --- | --- | 
| glibc, newlib | `_FORTIFY_SOURCE=3` | Enable input and buffer overflow checks for C library calls. |
| libstdc++ | `_GLIBCXX_ASSERTIONS` | Check preconditions for C++ library calls. |

> TODO: links

## Omitted

* `-fno-trampolines`: desired on i.e. embedded systems to avoid code execution from stack however disabling has no effect.


## References

1. [Diagnostic flags in Clang](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html)
1. [Clang command line argument reference](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html)
1. GCC - [Options to Request or Suppress Warnings](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html)
1. GCC - [Options Controlling C++ Dialect](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/C_002b_002b-Dialect-Options.html)


---


# Warnings (TODO)

* https://interrupt.memfault.com/blog/using-psp-msp-limit-registers-for-stack-overflow
* https://developer.arm.com/documentation/dui0774/l/Compiler-Command-line-Options/-fstack-protector---fstack-protector-all---fstack-protector-strong---fno-stack-protector


## Debugging

| Category | Goal | GCC | Clang |  
| --- | --- | --- | --- |
| Debugging | Produce debug information | [`-g3`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Debugging-Options.html#index-g) <br> [`-ggdb3`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Debugging-Options.html#index-ggdb) <br> [`-gdwarf-5`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Debugging-Options.html#index-gdwarf) | [`-g3`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-g) <br> [`-ggdb3`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-ggdb3) <br> [`-gdwarf-5`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-gdwarf-5) | ? |
| Debugging | Format C++ template diagnostics in a tree structure. | [`-fdiagnostics-show-template-tree`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Diagnostic-Message-Formatting-Options.html#index-fdiagnostics-show-template-tree) | [`-fdiagnostics-show-template-tree`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-fdiagnostics-show-template-tree) |  ? |

* fdiagnostics-color

Debug
 - set flags: -O0 -g3 -ggdb -fno-omit-frame-pointer
              /Od
 - define (-D): DEBUG
 - do not define (-U): NDEBUG

Release
 - set flags: -On -g2
              /Ox, /O2
 - define: NDEBUG
 - do not define DEBUG


Note:
 -g3 adds debug information, does not hit performance. That comes from not optimizing

https://cheatsheetseries.owasp.org/cheatsheets/C-Based_Toolchain_Hardening_Cheat_Sheet.htm

# Hardening

- general
- PC
- MCU?
 
https://best.openssf.org/Compiler-Hardening-Guides/Compiler-Options-Hardening-Guide-for-C-and-C++.html

* stripping symbols?
https://github.com/zephyrproject-rtos/zephyr/blob/main/scripts/kconfig/hardened.csv

Todo:
* newlib / picolibc?
* PAC?
* arm cortex-m specifics?
* `-mbranch-protection=standard`
* `-Wl,-z,relro`, `-Wl,-z,now`
 * `-fPIE -pie` (executable), `-fPIC -shared` (library)
* `-fno-strict-overflow` (`-fwrapv` + `-fwrapv-pointer`)
* `-Whardened`
* `-Wl,--as-needed`, `-Wl,--no-copy-dt-needed-entries`
* linker: `nodump`, `nodlopen`


## Sanitizers

* address (+ `-O1 -g -fno-omit-frame-pointer -fno-optimize-sibling-calls -fno-common`)
* thread (+ `-O2 -g`)
* leak
* undefined (+ `-O1 -g`)
* more useful options?
  -fsanitize=integer and -fsanitize=shift
  
## General

| Category | Goal | GCC | Clang | MSVC | 
| --- | --- | --- | --- |--- |
| Treat warnings as errors. | [`-Werror`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html#index-Werror) | [`-Werror`](https://clang.llvm.org/docs/UsersManual.html#cmdoption-Werror) | `/WX` |


Add common:
- [`-Wheader-hygiene`](https://clang.llvm.org/docs/DiagnosticsReference.html#wheader-hygiene)
- [`-Wtautological-constant-in-range-compare`](https://clang.llvm.org/docs/DiagnosticsReference.html#wtautological-constant-in-range-compare)

## Misc

| Goal | GCC | Clang | MSVC | 
| --- | --- | --- |--- |
| Warn about invalid pointer usage. | [`-Wpointer-arith`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html#index-Wpointer-arith) | [`-Wpointer-arith`](https://clang.llvm.org/docs/DiagnosticsReference.html#wpointer-arith) | ? |
|  Warn about optimizations where signed overflow is assumed not to occour. | [`-Wstrict-overflow=4`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html#index-Wstrict-overflow) | [`-Wstrict-overflow=4`](https://clang.llvm.org/docs/DiagnosticsReference.html#wstrict-overflow) (compat) | ? |
| Warn about shifting into the sign bit of a signed number | [`-Wshift-overflow=2`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html#index-Wshift-overflow) | [`-Wshift-overflow=2`](https://clang.llvm.org/docs/DiagnosticsReference.html#wshift-overflow) [d] | ? |\
||| [`-Wshift-sign-overflow`](https://clang.llvm.org/docs/DiagnosticsReference.html#wshift-sign-overflow) | |
| Warn about any unused parameter, function, variable, ... | [`-Wunused`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html#index-Wunused) | [`-Wunused`](https://clang.llvm.org/docs/DiagnosticsReference.html#wunused) | ? |\
|| `-Wunused-const-variable` ||
| Warn about functions marked as `inline` which cannot or will not be inlined. | [`-Winline`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html) | [`-Winline`](https://clang.llvm.org/docs/DiagnosticsReference.html#winline) (compat) | ? |

Add:
- [`Walloca`](https://clang.llvm.org/docs/DiagnosticsReference.html#walloca)

## Strings

Add:
- [`-Wformat-non-iso`](https://clang.llvm.org/docs/DiagnosticsReference.html#wformat-non-iso)
- [`-Wformat-type-confusion`](https://clang.llvm.org/docs/DiagnosticsReference.html#wformat-type-confusion)
- `-Wformat-overflow=2`
- `Wformat-signedness `


## Hardening

## Todo

* -fstack-check
* `-fsanitize=address`
* `ffreestanding`?
* update links to specific versions


* [What is the Strict Aliasing Rule and Why do we care?](https://gist.github.com/shafik/848ae25ee209f698763cffee272a58f8)


# TODO

# Compiler flags

## Generic

Based on [1], [3], [4] and [6] [9]

 
**String**

Flag | Description | GCC/Clang | MSVC equivelant |
--- | --- | --- | --- |
[`-Wvla`](https://clang.llvm.org/docs/DiagnosticsReference.html#wvla) | Warn about the use of variable length arrays. | Both | ? |
[`-Wwrite-strings`](https://clang.llvm.org/docs/DiagnosticsReference.html#wwrite-strings) | Warn about casting string literals. | Both | ? |
[-Wformat-type-confusion]() | Warn when an argument does match the format specified type.  | Clang | ? |

**Code generation**

Based on [2], [5] and [8]

Flag | Description | GCC/Clang | MSVC equivelant |
--- | --- | --- | --- |
`-fstack-usage` | Generate stack usage files for detailed stack analysis. | Both | ? |
[`-fvisibility`](https://gcc.gnu.org/onlinedocs/gcc/Code-Gen-Options.html#index-fvisibility) |  Set default symbol visibility to hidden | Both | ? |
[`-fvisibility-inlines-hidden`](https://clang.llvm.org/docs/ClangCommandLineReference.html#cmdoption-clang-fvisibility-inlines-hidden) | Sets the default symbol visibility to hidden for inline functions | Both | ? |
[`-x assembler-with-cpp`](https://clang.llvm.org/docs/ClangCommandLineReference.html#cmdoption-clang-x-language) | Tell the compiler the source language. | Both | ?
[`fwrapv`](https://clang.llvm.org/docs/ClangCommandLineReference.html#cmdoption-clang-fwrapv) | Treat signed integer overflow as two’s complement integers. | Both | ?

**Debugging**

> fstack-usage link and how to use the output.
> fomit-frame-pointer (?)
> 

## Embedded

### Compiler

Flag | Description | GCC/Clang |
--- | --- | --- |
[`-fno-exceptions`](https://clang.llvm.org/docs/ClangCommandLineReference.html#cmdoption-clang-fexceptions) | Disable support for exceptions | Both |
[`-fno-unwind-tables`](https://clang.llvm.org/docs/ClangCommandLineReference.html#cmdoption-clang-funwind-tables) | Disable generation of unwind tables (for backtraces) | Both |
[`-fno-rtti`](https://clang.llvm.org/docs/ClangCommandLineReference.html#cmdoption-clang-frtti) | Disable run-time type information | Both |

> **Beware**: dropping excpetion handling, unwind tables and RTTI only applies to the libraries/applications you build with these flags. The runtime you use will (very likely) be build with support for these features.
{.is-warning}
> `-mcpu`/`-mfpu`/`-mfloat-abi`/`-mabi`

### Linker

Flag | Description |
--- | --- | --- |
[`--gc-sections`](https://linux.die.net/man/1/ld) | Remove any unused sections |
[`--cref`](https://linux.die.net/man/1/ld) | Generate a cross reference table to determine declaration and use of symbols |
`--print-memory-usage` | Print out the memory usage summary after linking |

> `-nostartfiles`, `-nostdlib`, `--specs`
> `--build-id=uuid`, `--no-warn-rwx-segment`

> These options only apply to `ld`, hence no GCC/Clang/MSVC column.
{.is-info}

> todo: `sysroot`?
> https://interrupt.memfault.com/blog/code-size-optimization-gcc-flags#c-library
> No stdlib?
> -spec=nano.spec
> https://arobenko.github.io/bare_metal_cpp/#_know_your_compiler_output

## Debugging

[9]

> -g3
> -Os / -O1

Note that CMake already provides optimization flags (`-On` and `-g`) depending on the build configuration.

## Omitted

Flag | Description | Reason |
--- | --- | --- |
`-fdevirtualize` | Attempt to convert virtual calls to direct calls | Part of O2,O3,Os (GCC)


# References

1. [Diagnostic flags in Clang](https://clang.llvm.org/docs/DiagnosticsReference.html)
2. [Clang command line argument reference](https://clang.llvm.org/docs/ClangCommandLineReference.html)
3. GCC [Options to Request or Suppress Warnings](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html)
4. GCC [Options Controlling C++ Dialect](https://gcc.gnu.org/onlinedocs/gcc/C_002b_002b-Dialect-Options.html)
5. GCC [Options for Code Generation Conventions](https://gcc.gnu.org/onlinedocs/gcc/Code-Gen-Options.html)
6. [C++ Best Practices - Use The Tools Available](https://lefticus.gitbooks.io/cpp-best-practices/content/02-Use_the_Tools_Available.html)
7. [ld](https://linux.die.net/man/1/ld)
8. [Three GCC Flags for Analyzing Memory Usage](https://embeddedartistry.com/blog/2020/08/17/three-gcc-flags-for-analyzing-memory-usage/)
9. [The Best and Worst GCC Compiler Flags For Embedded](https://interrupt.memfault.com/blog/best-and-worst-gcc-clang-compiler-flags)

https://wiki.debian.org/Hardening
https://wiki.debian.org/HardeningWalkthrough
https://wiki.gentoo.org/wiki/Hardened/Toolchain

x86

`-mfunction-return=thunk` and `-mindirect-branch=thunk`
 
