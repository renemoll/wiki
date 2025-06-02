---
title: Compiler warnings
description: 
published: true
date: 2025-06-02T13:55:02.441Z
tags: 
editor: markdown
dateCreated: 2025-04-01T14:44:00.763Z
---



## Sanitizers

* address (+ `-O1 -g -fno-omit-frame-pointer -fno-optimize-sibling-calls -fno-common`)
* thread (+ `-O2 -g`)
* leak
* undefined (+ `-O1 -g`)
* more useful options?
  -fsanitize=integer and -fsanitize=shift

## Library specific

| Library | Option | Goal |
| --- | --- | --- | 
| glibc, newlib | `_FORTIFY_SOURCE=3` | Enable input and buffer overflow checks for C library calls. |
| libstdc++ | `_GLIBCXX_ASSERTIONS` | Check preconditions for C++ library calls. |

> TODO: links

## Build targets


> -g3
> -Os / -O1

Note that CMake already provides optimization flags (`-On` and `-g`) depending on the build configuration.

Debugging

| Goal | GCC | Clang |  
| --- | --- | --- |
| Produce debug information | [`-g3`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Debugging-Options.html#index-g) <br> [`-ggdb3`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Debugging-Options.html#index-ggdb) <br> [`-gdwarf-5`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Debugging-Options.html#index-gdwarf) | [`-g3`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-g) <br> [`-ggdb3`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-ggdb3) <br> [`-gdwarf-5`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-gdwarf-5) | ? |
| Format C++ template diagnostics in a tree structure. | [`-fdiagnostics-show-template-tree`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Diagnostic-Message-Formatting-Options.html#index-fdiagnostics-show-template-tree) | [`-fdiagnostics-show-template-tree`](https://releases.llvm.org/20.1.0/tools/clang/docs/ClangCommandLineReference.html#cmdoption-clang-fdiagnostics-show-template-tree) |  ? |
| Output coloured text in the terminal. [`-fdiagnostics-color`](https://gcc.gnu.org/onlinedocs/gcc-14.2.0/gcc/Diagnostic-Message-Formatting-Options.html#index-fdiagnostics-color) | ? |

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


# TODO

* https://interrupt.memfault.com/blog/using-psp-msp-limit-registers-for-stack-overflow


## Hardening

- general
- PC
- MCU?
 
* stripping symbols?
https://github.com/zephyrproject-rtos/zephyr/blob/main/scripts/kconfig/hardened.csv

Todo:
* newlib / picolibc?
* PAC?
* arm cortex-m specifics?
* `-mbranch-protection=standard`
 * `-fPIE -pie` (executable), `-fPIC -shared` (library)
* `-fno-strict-overflow` (`-fwrapv` + `-fwrapv-pointer`)
* `-Whardened`
* linker: `nodump`, `nodlopen`

## General

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

## Todo

* `ffreestanding`?

Based on [1], [3], [4] and [6] [9]
 
**String**

Flag | Description | GCC/Clang | MSVC equivelant |
--- | --- | --- | --- |
[`-Wvla`](https://clang.llvm.org/docs/DiagnosticsReference.html#wvla) | Warn about the use of variable length arrays. | Both | ? |
[`-Wwrite-strings`](https://clang.llvm.org/docs/DiagnosticsReference.html#wwrite-strings) | Warn about casting string literals. | Both | ? |

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

## Embedded

### Compiler

Flag | Description | GCC/Clang |
--- | --- | --- |
[`-fno-exceptions`](https://clang.llvm.org/docs/ClangCommandLineReference.html#cmdoption-clang-fexceptions) | Disable support for exceptions | Both |
[`-fno-unwind-tables`](https://clang.llvm.org/docs/ClangCommandLineReference.html#cmdoption-clang-funwind-tables) | Disable generation of unwind tables (for backtraces) | Both |
[`-fno-rtti`](https://clang.llvm.org/docs/ClangCommandLineReference.html#cmdoption-clang-frtti) | Disable run-time type information | Both |

> **Beware**: dropping excpetion handling, unwind tables and RTTI only applies to the libraries/applications you build with these flags. The runtime you use will (very likely) be build with support for these features.
{.is-warning}
> `-mfpu`/`-mfloat-abi`/`-mabi`

### Linker

Flag | Description |
--- | --- | --- |
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

## Omitted

Flag | Description | Reason |
--- | --- | --- |
`-fdevirtualize` | Attempt to convert virtual calls to direct calls | Part of O2,O3,Os (GCC)


# References

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
 
