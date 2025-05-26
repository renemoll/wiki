---
title: Type punning
description: 
published: true
date: 2025-05-26T14:38:35.846Z
tags: 
editor: markdown
dateCreated: 2025-05-16T14:04:22.085Z
---

# Type punning


# Introduction

## What is it

Type punning is a programming technique to use an object of a certain type as if is another type. Also see [Wikipedia](https://en.wikipedia.org/wiki/Type_punning).

## Why use it

Type punning is commonly used for:
* Manual optimizations, i.e. fast(er) computations;
* Serialization/deserialization of data structures;
* Low-level communication handling.

By taking the original object and representing it as something else, i.e. floats as integers or bytes and vice versa.

## What is the problem?

There are several methods to perform type punning, more then the standard specifies. This means there is good chance you get to deal with undefined behaviour, or non-portable code.

Is that a problem? Maybe, it depends on what you want to achieve.

# The problem

> See [What is the Strict Aliasing Rule and Why do we care?](https://gist.github.com/shafik/848ae25ee209f698763cffee272a58f8)


# The correct way

## How can the compiler help?

Enable:
* `-fstrict-aliasing`
* `-Wstrict-aliasing`
* `-Wold-style-cast`

Sanitizer:
* Address sanitizer: `-fsanitize=address`
* Type sanitizer: `-fsanitize=type` (experimental)

# References

* [Type aliasing](https://en.cppreference.com/w/cpp/language/reinterpret_cast#Type_aliasing)


# Scratchpad 




## How to use it
https://stackoverflow.com/questions/67636231/what-is-the-modern-correct-way-to-do-type-punning-in-c

OK methods:
* `memcpy` -> OK
  Starts a new object, copies the underlaying data byte array
* `bit_cast` -> OK
  Samilar to `memcpy`, can be `constexpr`
* `std::start_lifetime_as` -> ok
  Does not copy the data, kind of like placement new without calling the constructor.
* placement new + aligned storage...
* std::start_lifetime_as
  trival constructors


NOK Methods in C and C++:
* Pointer type conversion -> UB
  The standard specifies an object of a certain type may only be pointed to by a pointer of the same type. Having a pointer of a different type pointing to the object is seen as invalid and can be optimized away by the compiler.
* unions -> conditionally ok in C, UB in C++
  Invalid in C++
  Valic in C as long as the type used to read is not larger then the type used to write to
* `reinterpret_cast`, conditionally ok in C++
  Ok if converting a type from/to a byte reprentation (`char`, `unsigned char` or `std::byte`) (type accessability)

```C++
// #include <format>
#include <iostream>
#include <string>
#include <string_view>
#include <array>

#include <bit>
#include <cinttypes>

void example1() {
    float pi = 3.14f;
    std::cout << "pi: " << pi << std::endl;

    uint32_t direct_cast = static_cast<uint32_t>(pi);
    std::cout << "direct_cast: " << direct_cast << std::endl;

    uint32_t pointer_cast = *(uint32_t *)&pi;
    std::cout << "pointer_cast: " << std::hex << pointer_cast << std::endl;

    uint32_t reinterpretted = *reinterpret_cast<uint32_t*>(&pi); // UB, why not detected?
    std::cout << "reinterpret_cast: " << std::hex << reinterpretted << std::endl;

    union conv {
        float value;
        uint32_t bits;
    };

    conv t;
    t.value = pi;
    std::cout << "union: " << std::hex << t.bits << std::endl;

    // Note: bit-cast basically performs a memcpy, which is already a preffered method...
    uint32_t bit_casted = std::bit_cast<uint32_t>(pi);
    std::cout << "bit_cast: " << bit_casted << ", return: " << std::bit_cast<float>(bit_casted) << std::endl;
}

void example2() {
    std::array<uint8_t, 6> bytes = {0xAF, 0xC3, 0xF5, 0x48, 0x40, 0xFA};

    float pointer_cast = *(float *)&bytes[1];
    std::cout << "pointer_cast: " << pointer_cast << std::endl;

    float reinterpretted = *reinterpret_cast<float*>(&bytes[1]);
    std::cout << "reinterpret_cast: " << reinterpretted << std::endl;

    // union conv {
    //     float value;
    //     uint32_t bits;
    // };

    // conv t;
    // t.bits = bytes[1] | (bytes[2] << 8) | (bytes[3] << 16) | (bytes[4] << 24);
    // std::cout << "union: " << t.value << std::endl;

}

int main()
{
    example1();
    example2();
    return 0;
}

```

```C++
pi: 3.14
direct_cast: 3
pointer_cast: 4048f5c3
reinterpret_cast: 4048f5c3
union: 4048f5c3
bit_cast: 4048f5c3, return: 3.14
pointer_cast: 3.14
reinterpret_cast: 3.14
```
## Background

C++ operates on objects, objects can be created, destroyed, manipulated and accessed. Note that an object in this sense is not an instance of a class. More something that is stored in memory (variables, class instances, ...).

An object has:
* a type
* a size and thereby alignment
* a storage / lifetime
* a value
* and optionally a name

Important for this topic are the type, size and alignment. 
* the standard does not allow to interpret a certain object as something of another type (aliassing)
* alignment needs to be taken into account with casting

https://www.youtube.com/watch?v=pbkQG09grFw
* storage and lifetime are decoupled.


## What is allowed?

An object may be accessed:
* Through a reference to its type (adding cv qualifiers is ok)
* Through a singed/unsigned reference
* Through a byte representation (char, unsinged char, std::byte)

Anthing else -> UB


# Resources

1. https://andreasfertig.com/blog/2025/03/the-correct-way-to-do-type-punning-in-cpp/
1. https://andreasfertig.com/blog/2025/04/the-correct-way-to-do-type-punning-in-cpp-the-second-act/
1. https://en.cppreference.com/w/cpp/language/reinterpret_cast#Type_aliasing
1. https://en.cppreference.com/w/cpp/language/object#Strict_aliasing

# TODO

1. https://stackoverflow.com/questions/72511754/safely-type-punning-pod-like-structures-in-place-in-c20
1. https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Ru-pun
1. https://accu.org/journals/overload/28/160/anonymous/
   https://gist.github.com/shafik/848ae25ee209f698763cffee272a58f8
 
 
