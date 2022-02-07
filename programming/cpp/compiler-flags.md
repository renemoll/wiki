---
title: C++ compiler flags
description: 
published: true
date: 2022-02-07T19:32:11.489Z
tags: 
editor: markdown
dateCreated: 2022-02-07T19:28:50.042Z
---

# Compiler flags

Flag | Description | GCC/Clang | MSVC equivelant | Motivation
--- | --- | --- | --- | ---
`-Wall` | Enable warnings for common coding mistakes or potential errors. |
`-Wextra` | Extensions for -Wall |
`-Werror` | Treat warnings as errors to fail the build in case of warnings.
`-Wshadow`
`-Wnon-virtual-dtor`
`-pedantic`
`-Wpedantic` | # Warn for now standard C++.
`-Wconversion` | Warn about implicit type conversions which (may) change the value.
				-Wsign-conversion									# Warn about implicit sign conversions.
				-Wdouble-promotion									# Warn about floats being implictly converted to doubles.
				-Wfloat-equal										# Warn about floatint point values used in equality tests.
				$<$<CXX_COMPILER_ID:GNU>:-Warith-conversion>		# Warn about implicit type conversions during arithmitic operations.
				-Wpointer-arith										# Warn when sizeof(void) is used (directly or indirectly).
				$<$<COMPILE_LANGUAGE:CXX>:-Wold-style-cast>			# Warn about C-style casts.
				-Wcast-qual											# Warn when casting removes a type qualifier from a pointer.
				$<$<AND:$<CXX_COMPILER_ID:GNU>,$<COMPILE_LANGUAGE:CXX>>:-Wuseless-cast>		# Warn about casting to the same type.
				-Wcast-align										# Warn when casting a pointers changes the alignment of the pointee.
				$<$<COMPILE_LANGUAGE:C>:-Wbad-function-cast>		# Warn about casts to function pointers.
				$<$<COMPILE_LANGUAGE:CXX>:-Wnon-virtual-dtor>		# Warn about base classes without virtual destructors.
				$<$<COMPILE_LANGUAGE:CXX>:-Wctor-dtor-privacy>
				$<$<AND:$<CXX_COMPILER_ID:GNU>,$<COMPILE_LANGUAGE:CXX>>:-Wsuggest-override>	# Warn when a method overwriting a virtual method is not marked with override.
				-Wshadow											# Warn about duplicated variable names
				$<$<CXX_COMPILER_ID:Clang>:-Wshadow-all>
				$<$<COMPILE_LANGUAGE:CXX>:-Woverloaded-virtual>		# Warn when a derived function hides a virtual function of the base class.
				$<$<CXX_COMPILER_ID:GNU>:-Wduplicated-branches>		# Warn about identifcal branches in if-else expressions.
				$<$<CXX_COMPILER_ID:GNU>:-Wduplicated-cond>			# Warn about duplicated conditions in if-else expressions.
				$<$<CXX_COMPILER_ID:GNU>:-Wredundant-decls>			# Warn about multiple declarations within the same scope.
				-Wswitch-enum										# Warn about switch statements not using all possible enum values.
				-Wimplicit-fallthrough								# Warn about implicit, un-annotated, fallthroughs.
				-Wnull-dereference									# Warn about possible null pointer dereference code paths.
				-Wvla												# Warn about variable-length arrays being used.
				-Wwrite-strings										# Warn when attempting to write to a string constant.
				-Wformat=2											# Verify printf/scanf/.. arguments and format strings match.
				$<$<CXX_COMPILER_ID:GNU>:-Wformat-truncation=2>		# Warn when the output of sprintf/... might be truncated.
				-Wundef												# Warn when undefined macros are used (implicit conversion to 0.)
				$<$<CXX_COMPILER_ID:GNU>:-Wlogical-op>				# Warn about potential errors with logical operations.
				$<$<COMPILE_LANGUAGE:C>:-Wstrict-prototypes>		# Warn when a function declaration misses argument types.
				-Wunused											# Warn about any unused parameter/function/variable/etc...
				$<$<CXX_COMPILER_ID:GNU>:-Wmisleading-indentation>	# Warn about indentation giving the impression of scope.
				-Winline											# Warn when desired inlining is not possible.
				-Wtrampolines

# References

1. https://lefticus.gitbooks.io/cpp-best-practices/content/02-Use_the_Tools_Available.html
