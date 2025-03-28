---
title: Wiki
description: 
published: true
date: 2025-03-28T16:53:10.270Z
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