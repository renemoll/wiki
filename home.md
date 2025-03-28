---
title: Wiki
description: 
published: true
date: 2025-03-28T19:42:32.456Z
tags: 
editor: markdown
dateCreated: 2024-03-26T11:44:10.044Z
---

# Notes on

[Improving C++ Compilation Times: Tools & Techniques - Vittorio Romeo - ACCU 2023](https://www.youtube.com/watch?v=PfHD3BsVsAM)

1. Use Ninja [check]
1. Use lld [todo]
   * `-fuse-ld=lld`
   * `mold` even faster.. but only for unix systems
1. compiler cache
   - `ccache`, `sccache`

```cmake
find_program(CCACHE_PROGRAM ccache)
if (CCACHE_PROGRAM)
	set_property(GLOBAL PROPERTY RULE_LAUNCH_COMPILE "${CCACHE_PROGRAM}")
endif()
```


1. precompiled headers
 * useful for :
   * commonly use headers from within your project
   * "expensive" 3rd party headers
   * common STL headers
 * useful when:
   * the project has a lot of source files
 * which headers to include?
   * use `include-what-you-use` (frequently used) and ClangBuildAnalyzer (expensive)
 * one pre-compiled header per target

1. unity builds
 * CMake combines multiple sources files into one
  * Shared headers/templates/libraries will be compiled once per unity build
  * less work for the linker
  * less object files, less disk IO
 * 

```cmake
-DCMAKE_UNITY_BUILD=ON
```

```cmake
set_target_properties(<target> PROPERTIES UNITY_BUILD ON)
```

 * not useful when:
  * internal linkage (anonymus namespace symbol clashes)
  * `using namespace` in one file may influence another file
  * one define influences another source
  * masks missing header(s)
 * recommended to have a non unity build next to this...
 * useful to:
  * find ODR violations and missing header guards
> This one seems risky but could be interesting



