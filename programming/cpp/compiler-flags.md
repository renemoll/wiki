---
title: C++ compiler flags
description: 
published: true
date: 2022-02-07T20:25:31.533Z
tags: 
editor: markdown
dateCreated: 2022-02-07T19:28:50.042Z
---

# Compiler flags

Flag | Description | GCC/Clang | MSVC equivelant |
--- | --- | --- | --- |
[`-Wall`](https://clang.llvm.org/docs/DiagnosticsReference.html#wall) | Enable warnings for common coding mistakes or potential errors. | Both (though not equal) | ? |
`-Wextra` | Extensions for -Wall |
`-Werror` | Treat warnings as errors to fail the build in case of warnings.
`-pedantic` | (below)
`-Wpedantic` | Warn for now standard C++.
`-Wconversion` | Warn about implicit type conversions which (may) change the value.
`-Wsign-conversion` | Warn about implicit sign conversions.
`-Wdouble-promotion` | Warn about floats being implictly converted to doubles.
`-Wfloat-equal` | Warn about floatint point values used in equality tests.
`-Warith-conversion` | Warn about implicit type conversions during arithmitic operations. | GCC |
`-Wpointer-arith` | Warn when sizeof(void) is used (directly or indirectly).
`-Wold-style-cast` | Warn about C-style casts.
`-Wcast-qual` | Warn when casting removes a type qualifier from a pointer.
`-Wuseless-cast` | Warn about casting to the same type. | GCC
`-Wcast-align` | Warn when casting a pointers changes the alignment of the pointee.
`-Wbad-function-cast>` | Warn about casts to function pointers.
`-Wnon-virtual-dtor` | Warn about base classes without virtual destructors.
`-Wctor-dtor-privacy` | ?
`-Wsuggest-override>` | Warn when a method overwriting a virtual method is not marked with override. | GCC
`-Wshadow`  | Warn about duplicated variable names
`-Wshadow-all` | (?) | Clang
`-Woverloaded-virtual` | Warn when a derived function hides a virtual function of the base class.
`-Wduplicated-branches>` | Warn about identifcal branches in if-else expressions. | GCC
`-Wduplicated-cond` | Warn about duplicated conditions in if-else expressions. | GCC
`-Wredundant-decls` | Warn about multiple declarations within the same scope. | GCC
`-Wswitch-enum` | Warn about switch statements not using all possible enum values (default not being considered). | Both | ? |
`-Wimplicit-fallthrough` | Warn about implicit, un-annotated, fallthroughs.
`-Wnull-dereference` | Warn about possible null pointer dereference code paths.
`-Wvla` | Warn about variable-length arrays being used.
`-Wwrite-strings` | Warn when attempting to write to a string constant.
`-Wformat=2` | Verify printf/scanf/.. arguments and format strings match.
`-Wformat-truncation=2` | Warn when the output of sprintf/... might be truncated. | GCC
`-Wundef` | Warn when undefined macros are used (implicit conversion to 0.)
`-Wlogical-op` | Warn about potential errors with logical operations. | GCC
`-Wstrict-prototypes` | Warn when a function declaration misses argument types.
`-Wunused` | Warn about any unused parameter/function/variable/etc...
`-Wmisleading-indentation` | Warn about indentation giving the impression of scope. | GCC
`-Winline` | Warn when desired inlining is not possible.
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

1. https://clang.llvm.org/docs/DiagnosticsReference.html
1. https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html
1. https://lefticus.gitbooks.io/cpp-best-practices/content/02-Use_the_Tools_Available.html
