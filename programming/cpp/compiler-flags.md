---
title: C++ compiler flags
description: 
published: true
date: 2023-11-16T21:34:54.551Z
tags: 
editor: markdown
dateCreated: 2022-12-14T19:49:02.673Z
---

# Compiler flags

## Generic

Based on [1], [3], [4] and [6] [9]

**General**

Flag | Description | GCC/Clang | MSVC equivelant |
--- | --- | --- | --- |
[`-Wall`](https://clang.llvm.org/docs/DiagnosticsReference.html#wall) | Enable warnings for common coding mistakes or potential errors. | Both (though set not equal) | ? |
[`-Wextra`](https://clang.llvm.org/docs/DiagnosticsReference.html#wextra) | Set of additional warnings to accompany `-Wall` | Both (though set not equal) | ? |
[`-Werror`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html) | Treat warnings as errors, to fail the build in case of warnings. | Both | ? |
[`-Wpedantic`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html) | Warn about non-ISO standard C/C++ constructions. | Both | ? |

> -Wdocumentation
> -Weverything

**Type conversion**

Flag | Description | GCC/Clang | MSVC equivelant |
--- | --- | --- | --- |
[`-Wconversion`](https://clang.llvm.org/docs/DiagnosticsReference.html#wconversion) | Warn about implicit type conversions which (may) change or not fit the value. | Both | ? |
[`-Wsign-conversion`](https://clang.llvm.org/docs/DiagnosticsReference.html#wsign-conversion) | Warn about implicit sign conversions. | Both | ? |
[`-Wdouble-promotion`](https://clang.llvm.org/docs/DiagnosticsReference.html#wdouble-promotion) | Warn about floats being implictly converted to doubles. | Both | ? |
[`-Wfloat-equal`](https://clang.llvm.org/docs/DiagnosticsReference.html#wfloat-equal) | Warn about floating point values used in equality tests. | Both | ? |
[`-Warith-conversion`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html) | Warn about implicit type conversions with arithmitic operations. | GCC | ? |
[`-Wpointer-arith`](https://clang.llvm.org/docs/DiagnosticsReference.html#wpointer-arith) | Warn when sizeof(void) is used (directly or indirectly). | Both | ? |
[`-Wold-style-cast`](https://clang.llvm.org/docs/DiagnosticsReference.html#wold-style-cast) | Warn about C-style casts. | Both | ? |
[`-Wcast-qual`](https://clang.llvm.org/docs/DiagnosticsReference.html#wcast-qual) | Warn about casts removing a type qualifier. | Both | ? |
[`-Wuseless-cast`](https://gcc.gnu.org/onlinedocs/gcc/C_002b_002b-Dialect-Options.html) | Warn about casting to the same type. | GCC | ? |
[`-Wcast-align`](https://clang.llvm.org/docs/DiagnosticsReference.html#wcast-align) | Warn when casting a pointer changes the alignment of the pointee. | Both | ? |
[`-Wcast-align=strict`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html#index-Wcast-align_003dstrict) | Stricter version | GCC | ? |
[`-Wbad-function-cast`](https://clang.llvm.org/docs/DiagnosticsReference.html#wbad-function-cast) | Warn about function call is cast to a different type. | Both | ? |
[-Wstrict-overflow=2](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html#index-Wstrict-overflow) |  Warn about optimizations where signed overflow is assumed not to occour. | Both | ? |
[-Wshift-overflow=2](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html#index-Wshift-overflow) | GCC | ? |
[-Wshift-sign-overflow](https://clang.llvm.org/docs/DiagnosticsReference.html#wshift-sign-overflow) | See above | Clang | ? |
[-Wzero-as-null-pointer-constant](https://clang.llvm.org/docs/DiagnosticsReference.html#wzero-as-null-pointer-constant) | Warn about using 0 as a null pointer. | Clang | ? |

**Classes**

Flag | Description | GCC/Clang | MSVC equivelant |
--- | --- | --- | --- |
[`-Wnon-virtual-dtor`](https://clang.llvm.org/docs/DiagnosticsReference.html#wnon-virtual-dtor) | Warn about base classes without virtual destructors. | Both | ? |
[`-Wctor-dtor-privacy`](https://gcc.gnu.org/onlinedocs/gcc/C_002b_002b-Dialect-Options.html) | Warn about classes which seemingly cannot be used. | Both | ? |
[`-Wsuggest-override`](https://clang.llvm.org/docs/DiagnosticsReference.html#wsuggest-override) | Warn about methods overwriting a virtual method while not marked with `override`. | Both | ? |
[`-Woverloaded-virtual`](https://clang.llvm.org/docs/DiagnosticsReference.html#woverloaded-virtual) | Warn about derived methods hiding a virtual function of the base class. | Both | ? |

**Misc**

Flag | Description | GCC/Clang | MSVC equivelant |
--- | --- | --- | --- |
[`-Wshadow`](https://clang.llvm.org/docs/DiagnosticsReference.html#wshadow) | Warn about variables with the same name, shadowing the one(s) in a broader scope. | Both | ? |
[`-Wshadow-all`](https://clang.llvm.org/docs/DiagnosticsReference.html#wshadow-all) | Additional shadowing checks | Clang | ? |
[`-Wduplicated-branches`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html) | Warn about identifcal branches in if-else expressions. | GCC | ? |
[`-Wduplicated-cond`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html) | Warn about duplicated conditions in if-else expressions. | GCC | ? |
[`-Wredundant-decls`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html) | Warn about multiple declarations within the same scope. | GCC | ? |
[`-Wswitch-enum`](https://clang.llvm.org/docs/DiagnosticsReference.html#wswitch-enum) | Warn about switch statements not using all possible enum values (default not being considered). | Both | ? |
[`-Wimplicit-fallthrough`](https://clang.llvm.org/docs/DiagnosticsReference.html#wimplicit-fallthrough) | Warn about implicit, un-annotated, fallthroughs. | Both | ? |
[`-Wnull-dereference`](https://clang.llvm.org/docs/DiagnosticsReference.html#wnull-dereference) | Warn about possible null pointer dereference. | Both | ? |
[`-Wundef`](https://clang.llvm.org/docs/DiagnosticsReference.html#wundef) | Warn about the use of undefined macros (which implicitly convert to 0.) | Both | ? |
[`-Wlogical-op`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html) | Warn about potential errors with logical operations. | GCC | ? |
[`-Wstrict-prototypes`](https://clang.llvm.org/docs/DiagnosticsReference.html#wstrict-prototypes) | Warn about function declarations misses argument types. | Both | ? |
[`-Wunused`](https://clang.llvm.org/docs/DiagnosticsReference.html#wunused) | Warn about any unused parameter/function/variable/etc. | Both | ? |
[`-Wmisleading-indentation`](https://clang.llvm.org/docs/DiagnosticsReference.html#wmisleading-indentation) | Warn about indentation giving the impression of scope. | Both | ? |
[`-Winline`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html) | Warn about functions marked as `inline` which cannot/will not be inlined. | Both | ? |
[`-Wtrampolines`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html) | Warn about code to jump to a function, requiring an executable stack | GCC | ? |
[`-Warray-bounds=2`](https://clang.llvm.org/docs/DiagnosticsReference.html#warray-bounds) | Warns about invalid array indices | Both (on by default/`-Wall`, level is GCC specific) | ? |
[`-Wzero-as-null-pointer-constant`](https://clang.llvm.org/docs/DiagnosticsReference.html#wzero-as-null-pointer-constant) | Warn about the use of 0 as nullptr | Both | ? |
`Wstrict-null-sentinel` | Warn about the use of an uncasted NULL as sentinel | GCC | ? |
[-Wconditional-uninitialized](https://clang.llvm.org/docs/DiagnosticsReference.html#wconditional-uninitialized) | Warn about variables which might be uinitialized | Clang | ? |
[-Wtrivial-auto-var-init](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html#index-Wtrivial-auto-var-init) | Warn about automatic variables which might be unintialized. | GCC | ? |
[-Wloop-analysis](https://clang.llvm.org/docs/DiagnosticsReference.html#wloop-analysis) | Warn about loop varialbes being manipulated/ignored/.. inside the loop | Clang | ? |

**String**

Flag | Description | GCC/Clang | MSVC equivelant |
--- | --- | --- | --- |
[`-Wvla`](https://clang.llvm.org/docs/DiagnosticsReference.html#wvla) | Warn about the use of variable length arrays. | Both | ? |
[`-Wwrite-strings`](https://clang.llvm.org/docs/DiagnosticsReference.html#wwrite-strings) | Warn about casting string literals. | Both | ? |
[`-Wformat=2`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html) | Verify the format string for functions such as `printf`, `scanf`, etc. | Both | ? |
[`-Wformat-truncation=2`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html) | Warn calls to format functions (`printf` and such) where the output might be truncated. | GCC | ? |
[-Wformat-type-confusion]() | Warn when an argument does match the format specified type.  | Clang | ? |

**Code generation**

Based on [2], [5] and [8]

Flag | Description | GCC/Clang | MSVC equivelant |
--- | --- | --- | --- |
[`-fno-common`](https://clang.llvm.org/docs/ClangCommandLineReference.html#cmdoption-clang-fcommon) | Ensures uninitialized variables are not merged into a single unit, causing a multiple declaration error. | Both | ? |
`-fstack-usage` | Generate stack usage files for detailed stack analysis. | Both | ? |
[`-fvisibility`](https://gcc.gnu.org/onlinedocs/gcc/Code-Gen-Options.html#index-fvisibility) |  Set default symbol visibility to hidden | Both | ? |
[`-fvisibility-inlines-hidden`](https://clang.llvm.org/docs/ClangCommandLineReference.html#cmdoption-clang-fvisibility-inlines-hidden) | Sets the default symbol visibility to hidden for inline functions | Both | ? |
[`-x assembler-with-cpp`](https://clang.llvm.org/docs/ClangCommandLineReference.html#cmdoption-clang-x-language) | Tell the compiler the source language. | Both | ?
[`fwrapv`](https://clang.llvm.org/docs/ClangCommandLineReference.html#cmdoption-clang-fwrapv) | Treat signed integer overflow as two’s complement integers. | Both | ?
[-ftrivial-auto-var-init=zero] | Ensure automatic variables are always initialized. | Both | ? | 

**Debugging**

Flag | Description | GCC/Clang | MSVC equivelant |
--- | --- | --- | --- |
[`-gdwarf-4`](https://gcc.gnu.org/onlinedocs/gcc-10.1.0/gcc/Debugging-Options.html) | Generate debugging information. | Both | ?
[`-fvar-tracking-assignments`](https://gcc.gnu.org/onlinedocs/gcc-10.1.0/gcc/Debugging-Options.html) | Annotates variables to improve debugging. | GCC | ?
[`-fdiagnostics-show-template-tree`](https://clang.llvm.org/docs/ClangCommandLineReference.html#cmdoption-clang-fdiagnostics-show-template-tree) | Highlight the differences when diagnosing template type errors. | Both | ?

> why not dwarf-5?
> fstack-usage link and how to use the output.
> fomit-frame-pointer (?)
> 

## Embedded

### Compiler

Flag | Description | GCC/Clang |
--- | --- | --- |
[`-ffunction-sections`](https://clang.llvm.org/docs/ClangCommandLineReference.html#cmdoption-clang-ffunction-sections) | Place each function into its own section | Both |
[`-fdata-sections`](https://clang.llvm.org/docs/ClangCommandLineReference.html#cmdoption-clang-fdata-sections) | Place each data element into its own section | Both |
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

## Debugging

[9]

> -g3
> -Os / -O1

Note that CMake already provides optimization flags (`-On` and `-g`) depending on the build configuration.

## Omitted

Flag | Description | Reason |
--- | --- | --- |
`-fdevirtualize` | Attempt to convert virtual calls to direct calls | Part of O2,O3,Os (GCC)
`-fstrict-aliasing` | ... | Part of O2, O3, Os (GCC/Clang).
`-Wstrict-aliasing` | | Part of `-Wall`, active when `-fstrict-aliasing` is active.

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