---
title: Compiler warnings
description: 
published: true
date: 2025-06-02T11:49:36.861Z
tags: 
editor: markdown
dateCreated: 2025-04-01T14:44:00.763Z
---



## Settings

| Category | Goal | GCC | Clang | MSVC | 
| --- | --- | --- | --- | --- |
| Common defects | Warn about the use of undefined identifiers, which implicitly convert to 0. | [`-Wundef`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wundef) | [`-Wundef`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wundef) | ? |
| Common defects | Warn about potential mistakes with logical operators. | [`-Wlogical-op`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wlogical-op) | n/a | ? |
| Common defects | Warn about `switch` cases not covering all possible enum values. | [`-Wswitch-enum`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wswitch-enum) | [`-Wswitch-enum`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wswitch-enum) | ? |
| Modernisation | Warn about implicit fall throughs. | [`-Wimplicit-fallthrough=5`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wimplicit-fallthrough) | [`-Wimplicit-fallthrough`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wimplicit-fallthrough) | ? |

### C++ specific
| Category | Goal | GCC | Clang | MSVC | 
| --- | --- | --- | --- |--- |
| OOP | Warn about base classes without virtual destructors. | [`-Wnon-virtual-dtor`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/C_002b_002b-Dialect-Options.html#index-Wnon-virtual-dtor) | [`-Wnon-virtual-dtor`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wnon-virtual-dtor) | [`/w14265`](https://learn.microsoft.com/en-us/cpp/error-messages/compiler-warnings/compiler-warning-level-3-c4265?view=msvc-170) |
| OOP | Warn about classes which seemingly cannot be used (private constructor/destructors.) | [`-Wctor-dtor-privacy`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/C_002b_002b-Dialect-Options.html#index-Wctor-dtor-privacy) | [`-Wctor-dtor-privacy`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wctor-dtor-privacy) | ? |
| OOP | Warn about methods overwriting virtual methods not marked with `override`. | [`-Wsuggest-override`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/C_002b_002b-Dialect-Options.html#index-Wsuggest-override) | [`-Wsuggest-override`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wsuggest-override) <br> [`-Wsuggest-destructor-override`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#wsuggest-destructor-override) | `/analyze` |
| OOP | Warn about methods in a derived class hiding virtual functions of the base class. | [`-Woverloaded-virtual`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/C_002b_002b-Dialect-Options.html#index-Woverloaded-virtual) | [`-Woverloaded-virtual`](https://releases.llvm.org/20.1.0/tools/clang/docs/DiagnosticsReference.html#woverloaded-virtual) | `/w14263` |
| | Warn about (implicit) sign conversions. | [`-Wsign-promo`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/C_002b_002b-Dialect-Options.html#index-Wsign-promo) | ? | ? |


### Hardening

| Category | Goal | GCC | Clang | MSVC |
| --- | --- | --- | --- |--- |
| Common defects | Follow C99 standard definition for flexible array members in a structure. | [`-fstrict-flex-arrays=3`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/C-Dialect-Options.html#index-fstrict-flex-arrays) | [`-fstrict-flex-arrays=3`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-fstrict-flex-arrays) | ? |
| Common defects | Stack Smashing Protector | [`-fstack-protector-strong`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Instrumentation-Options.html#index-fstack-protector-strong) | [`-fstack-protector-strong`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-fstack-protector-strong) | ? |
|  | Prevent stack clash attacks by limited stack allocation size. | [`-fstack-clash-protection`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Instrumentation-Options.html#index-fstack-clash-protection) | [`-fstack-clash-protection`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-fstack-clash-protection) | ? |
| ? | Don't allow executing code from the stack. | `-fno-trampolines` <br> [`-Wtrampolines`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Warning-Options.html#index-Wtrampolines) <br> `-Wl,-z,noexecstack` <br> `-Wl,-z,noexecheap` | ? | ? |


> Note: `__stack_chk_fail` & `__stack_chk_guard` with `-fstack-protector-strong`
> -fstack-protector-all?

### x86

| Category | Goal | GCC | Clang |
| --- | --- | --- | --- |
| x86  |  Verify target addresses of control-flow transfer instructions are valid. | [`-fcf-protection=full`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Instrumentation-Options.html#index-fcf-protection) | [`-fcf-protection=full`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-fcf-protection) | ? |


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

* `-fstack-check` in favor of `-fstack-clash-protection` ([Stack clash mitigation in GCC, Part 3](https://developers.redhat.com/blog/2020/05/22/stack-clash-mitigation-in-gcc-part-3))


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
| | Output coloured text in the terminal. [`-fdiagnostics-color`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Diagnostic-Message-Formatting-Options.html#index-fdiagnostics-color) | ? |

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
|  Warn about optimizations where signed overflow is assumed not to occour. | [`-Wstrict-overflow=4`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html#index-Wstrict-overflow) | [`-Wstrict-overflow=4`](https://clang.llvm.org/docs/DiagnosticsReference.html#wstrict-overflow) (compat) | ? |
| Warn about shifting into the sign bit of a signed number | [`-Wshift-overflow=2`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html#index-Wshift-overflow) | [`-Wshift-overflow=2`](https://clang.llvm.org/docs/DiagnosticsReference.html#wshift-overflow) [d] | ? |\
||| [`-Wshift-sign-overflow`](https://clang.llvm.org/docs/DiagnosticsReference.html#wshift-sign-overflow) | |



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
 
