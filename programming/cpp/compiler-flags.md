---
title: C++ compiler flags
description: 
published: true
date: 2022-02-07T21:07:46.102Z
tags: 
editor: markdown
dateCreated: 2022-02-07T19:28:50.042Z
---

# Compiler flags

**General**

Flag | Description | GCC/Clang | MSVC equivelant |
--- | --- | --- | --- |
[`-Wall`](https://clang.llvm.org/docs/DiagnosticsReference.html#wall) | Enable warnings for common coding mistakes or potential errors. | Both (though set not equal) | ? |
[`-Wextra`](https://clang.llvm.org/docs/DiagnosticsReference.html#wextra) | Set of additional warnings to accompany `-Wall` | Both (though set not equal) | ? |
[`-Werror`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html) | Treat warnings as errors, to fail the build in case of warnings. | Both | ? |
[`-Wpedantic`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html) | Warn about non-ISO standard C/C++ constructions. | Both | ? |

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
[`-Wbad-function-cast`](https://clang.llvm.org/docs/DiagnosticsReference.html#wbad-function-cast) | Warn about function call is cast to a different type. | Both | ? |

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
[`-Wstrict-prototypes`](https://clang.llvm.org/docs/DiagnosticsReference.html#wstrict-prototypes) | Warn about function declarations misses argument types.
[`-Wunused`](https://clang.llvm.org/docs/DiagnosticsReference.html#wunused) | Warn about any unused parameter/function/variable/etc. | Both | ? |
[`-Wmisleading-indentation`](https://clang.llvm.org/docs/DiagnosticsReference.html#wmisleading-indentation) | Warn about indentation giving the impression of scope. | Both | ? |
[`-Winline`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html) | Warn about functions marked as `inline` which cannot/will not be inlined. | GCC | ? |

**String**

Flag | Description | GCC/Clang | MSVC equivelant |
--- | --- | --- | --- |
[`-Wvla`](https://clang.llvm.org/docs/DiagnosticsReference.html#wvla) | Warn about the use of variable length arrays. | Both | ? |
[`-Wwrite-strings`](https://clang.llvm.org/docs/DiagnosticsReference.html#wwrite-strings) | Warn about casting string literals. | Both | ? |
[`-Wformat=2`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html) | Verify the format string for functions such as `printf`, `scanf`, etc. | Both | ? |
[`-Wformat-truncation=2`](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html) | Warn calls to format functions (`printf` and such) where the output might be truncated. | GCC | ? |


`-Wtrampolines` | ?
`-fno-common` | ?
[`-Warray-bounds=2`](https://clang.llvm.org/docs/DiagnosticsReference.html#warray-bounds) | Warns about invalid array indices | Both (on by default/`-Wall`, level is GCC specific) | ? |


# Embedded

Compiler:
`-mthumb`
`-ffunction-sections`
`-fdata-sections`
`-fno-exceptions`
`-fno-unwind-tables`
`-fno-rtti`

linker
`-mthumb` ??
`--gc-sections`
`--cref`
`--print-memory-usage`

todo: `sysroot`?

# References

1. [Diagnostic flags in Clang](https://clang.llvm.org/docs/DiagnosticsReference.html)
1. GCC [Options to Request or Suppress Warnings](https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html)
1. GCC [Options Controlling C++ Dialect](https://gcc.gnu.org/onlinedocs/gcc/C_002b_002b-Dialect-Options.html)
1. [C++ Best Practices - Use The Tools Available](https://lefticus.gitbooks.io/cpp-best-practices/content/02-Use_the_Tools_Available.html)
