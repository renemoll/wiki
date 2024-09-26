---
title: Linker
description: 
published: true
date: 2024-09-26T19:58:02.030Z
tags: 
editor: markdown
dateCreated: 2024-09-26T19:58:02.030Z
---

# Linker

> From an embedded software developer point of view

## Sections

Note: this is note a complete list as not all setions are relevant to embedded development.

Section | Use
--- | ---
`.bss` | Uninitialized data.
`.data` | Initialized data.
`.rodata` | Read-only data.
`.text` | Executable instruction.

### Section types

Type | Description
--- | ---
`SHT_NULL` | An empty section with no size.
`SHT_PROGBITS` | Initialized data and/or instructions.
`SHT_SYMTAB` | The symbol table.
`SHT_STRTAB` | The string table.
`SHT_NOTE` | File specific meta-data.
`SHT_NOBITS` | Simular to `SHT_PROGBITS` but without any content, acts as a placeholder.



`SHT_INIT_ARRAY` | An array of pointers, pointing to initialization functions.
`SHT_INIT_ARRAY` | An array of pointers, pointing to initialization functions.
`SHT_PREINIT_ARRAY` | An array of pointers, pointing to pre-initialization functions.
`SHT_ARM_EXIDX`
`SHT_ARM_ATTRIBUTES`

> What ends up where?
> What is the use of `SHT_NULL`?


Section | Type | Mapping | Note
--- | ---| ---
`.bss` | `SHT_NOBITS` | RAM | `SHT_NOBITS` means this unitialized data is taken into consideration for memory mapping. However, since the content is all zero; it is not stored in the file.
`.data` | `SHT_PROGBITS` | FLASH + RAM | Initialized, non-constant, data, stored in FLASH and copied into RAM during startup.
`.rodata` | `SHT_PROGBITS` | FLASH | Initialized, constant, data, stored in FLASH.
`.text` | `SHT_PROGBITS` | FLASH | Functional code.



Type | Example
--- | ---
SHT_NOTE | GCC build id

Obsolete:
* `.init`: see `.init_array`
* `.fini`: see `.fini_array`