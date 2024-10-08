---
title: Alignment and padding
description: 
published: true
date: 2024-01-30T13:53:17.931Z
tags: 
editor: markdown
dateCreated: 2024-01-30T13:53:17.931Z
---

# Alignment and padding

[C++ Weekly - Ep 410 - What Are Padding and Alignment? (And Why You Might Care)](https://www.youtube.com/watch?v=E0QhZ6tNoRg)

Basic information

Data types have memory alignment requirememts (C/C++ standard)
 - certain types can only started at certain memory offsets
 - depends on the size of the data type
 - impacts code generation
 - some architectures cannot work with unaligned memory access
 - alignment depends on the architecture

Combining data types with different alignment requirements (i.e. in a struct) can
have a negative impact on the size of the overall struct. This can be checked by:
- sizeof(T)
- using compiler warning -Wpadded
  note: likely will always give you warnings, may not be usefull all the time.
- rearranging struct members will break the ABI (you are changing the memory layout, after all)

Why would you want to know this?
 - memory usage
 - cache friendlyness

Rule of thumb:
 - place the largest sized elements first
 - try to group certain types together (to fill a gap for example)
 - play tetris

What about packed structs?
 - not standardized -> compiler extension    
 - hard to do correct (example...)
 - trade memory saving for inefficient generated code (likely the compiler will create a copy into an aligned memory location)
 - issue on architectures which cannot work with unaligned memory
  
