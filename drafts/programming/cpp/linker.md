---
title: Linker
description: 
published: true
date: 2024-09-29T18:00:36.764Z
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
`.shstrtab` | A section containing the section names.
`.note.gnu.build-id` | TBD
`.strtab` | A table containing the names of the symbols in the symbol table.
`.symtab` | A table containing all symbols and meta data (name, sizes, location).


### Section types

Type | Description
--- | ---
`SHT_NULL` | An empty section with no size.
`SHT_PROGBITS` | Initialized data and/or instructions.
`SHT_STRTAB` | The string table.
`SHT_SYMTAB` | The symbol table.
`SHT_NOTE` | Textual  meta-data.
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
`.note.gnu.build-id` | `SHT_NOTE` | (depends) | TBD

> Note: mapping is defined in the linker file, the above is an example.

Type | Example
--- | ---
SHT_NOTE | GCC build id

Obsolete:
* `.init`: see `.init_array`
* `.fini`: see `.fini_array`
* `.ctors`: see `.init_array`
* `.dtors`: see `.fini_array`


```bash
.note.gnu.build-id   bytes: 32                   kb: 0.0        type: SHT_NOTE
  section: .isr_vector          bytes: 504                  kb: 0.5        type: SHT_PROGBITS
  section: .ARM                 bytes: 8                    kb: 0.0        type: SHT_ARM_EXIDX
  section: .init_array          bytes: 12                   kb: 0.0        type: SHT_INIT_ARRAY
  section: .fini_array          bytes: 4                    kb: 0.0        type: SHT_FINI_ARRAY
  section: ._user_heap_stack    bytes: 512                  kb: 0.5        type: SHT_NOBITS
  section: .ARM.attributes      bytes: 46                   kb: 0.0        type: SHT_ARM_ATTRIBUTES
  section: .debug_info          bytes: 11960                kb: 11.7       type: SHT_PROGBITS
  section: .debug_abbrev        bytes: 2373                 kb: 2.3        type: SHT_PROGBITS
  section: .debug_aranges       bytes: 112                  kb: 0.1        type: SHT_PROGBITS
  section: .debug_rnglists      bytes: 245                  kb: 0.2        type: SHT_PROGBITS
  section: .debug_line          bytes: 2639                 kb: 2.6        type: SHT_PROGBITS
  section: .debug_str           bytes: 6355                 kb: 6.2        type: SHT_PROGBITS
  section: .comment             bytes: 68                   kb: 0.1        type: SHT_PROGBITS
  section: .debug_frame         bytes: 720                  kb: 0.7        type: SHT_PROGBITS
  section: .debug_loclists      bytes: 380                  kb: 0.4        type: SHT_PROGBITS
  section: .debug_line_str      bytes: 206                  kb: 0.2        type: SHT_PROGBITS
  section: .shstrtab 
```

## References

* [System V Application Binary Interface - Edition 4.1](https://www.sco.com/developers/devspecs/gabi41.pdf)
