---
title: Compiler warnings
description: 
published: true
date: 2025-06-05T15:03:04.644Z
tags: 
editor: markdown
dateCreated: 2025-04-01T14:44:00.763Z
---


## Leveraging Your Toolchain to Improve Security
[Leveraging Your Toolchain to Improve Security](https://embeddedartistry.com/blog/2023/09/20/leveraging-your-toolchain-to-improve-security/)

To include 3rd party code:
* mark include folders as "system" (`-isystem`, `target_include_directories` with `SYSTEM`)
* split build structure into libraries with different sets of warnings

* `Wstrict-overflow` -> omitted due to signed integer? Note
* `Wshift-overflow` -> omitted as I target newer C++ versions
* `Wshift-sign-overflow`
* `-Wstringop-overflow=4`
* `-Wuse-after-free=3`
* `Wuninitialized`
* `-Wswitch-default ` -> omitted as I want all cases explicitly covered
* `-Wjump-misses-init`
* `Wcomma`
* `Wassign-enum`
* `Wunreachable-code-aggressive`

* clang-tidy
* scan-build
* https://github.com/Ericsson/codechecker/blob/master/docs/usage.md

* Implementing stack smashing protection: https://embeddedartistry.com/blog/2020/05/18/implementing-stack-smashing-protection-for-microcontrollers-and-embedded-artistrys-libc/
* `-fsanitize=safe-stack`?
* `-fsanitize=signed-integer-overflow`
* `-fsanitize=bounds`


## Sanitizers

* address (+ `-O1 -g -fno-omit-frame-pointer -fno-optimize-sibling-calls -fno-common`)
```
ASAN_OPTIONS=strict_string_checks=1:detect_stack_use_after_return=1:check_initialization_order=1:strict_init_order=1 ./instrumented-executable
ASAN_SYMBOLIZER_PATH=/usr/local/bin/llvm-symbolizer ./a.out
```
https://github.com/google/sanitizers/wiki/AddressSanitizerFlags
Cannot be combined with -fsanitize=thread 
`-fsanitize-address-use-after-scope`?

* thread (+ `-O2 -g`)
Cannot be combined with -fsanitize=address, -fsanitize=leak

* leak
```
ASAN_OPTIONS=detect_leaks=1
```
Part of ASAN

* undefined (+ `-O1 -g`)
```
-fsanitize=float-divide-by-zero,undefined,vptr -g  -fno-omit-frame-pointer -fno-sanitize-merge and
UBSAN_OPTIONS=print_stacktrace=1 
```

* memory
`-fsanitize=memory -fno-omit-frame-pointer -g -O1 -fno-optimize-sibling-calls`
`-fsanitize-memory-track-origins=2`?
```
MSAN_SYMBOLIZER_PATH=/usr/local/bin/llvm-symbolizer ./a.out
```

* more useful options?
  -fsanitize=integer and -fsanitize=shift
  -fsanitize=signed-integer-overflow

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

-fverbose-asm

# TODO

* https://interrupt.memfault.com/blog/using-psp-msp-limit-registers-for-stack-overflow


## Hardening
 
* stripping symbols?
  * https://github.com/zephyrproject-rtos/zephyr/blob/main/scripts/kconfig/hardened.csv
  * https://best.openssf.org/Compiler-Hardening-Guides/Compiler-Options-Hardening-Guide-for-C-and-C++.html#maintaining-debug-information-in-separate-files


Todo:
* newlib / picolibc?
* PAC?
* arm cortex-m specifics?
* `-mbranch-protection=standard`
* `-fhardened` and `-Whardened`
* linker: `nodump`, `nodlopen`

## General

Add common:
- [`-Wheader-hygiene`](https://clang.llvm.org/docs/DiagnosticsReference.html#wheader-hygiene)
- [`-Wtautological-constant-in-range-compare`](https://clang.llvm.org/docs/DiagnosticsReference.html#wtautological-constant-in-range-compare)

## Misc

| Goal | GCC | Clang | MSVC | 
| --- | --- | --- |--- |
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

fvisibility -> https://gcc.gnu.org/wiki/Visibility

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
8. [Three GCC Flags for Analyzing Memory Usage](https://embeddedartistry.com/blog/2020/08/17/three-gcc-flags-for-analyzing-memory-usage/)
9. [The Best and Worst GCC Compiler Flags For Embedded](https://interrupt.memfault.com/blog/best-and-worst-gcc-clang-compiler-flags)

https://wiki.debian.org/Hardening
https://wiki.debian.org/HardeningWalkthrough
https://wiki.gentoo.org/wiki/Hardened/Toolchain

x86

`-mfunction-return=thunk` and `-mindirect-branch=thunk`
 
