---
title: Type punning
description: 
published: true
date: 2025-05-27T08:31:48.459Z
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


# How to type pun

In C11 and C++17 and forwards:

Method | Valid C | Valid C++
| --- | --- | --- |
| `std::memcpy` | Y | Y |
| `std::bit_cast` | n/a | Y (from C++20) |
| placement `new` | n/a | Y |
| C style casts | Conditionally | N |
| `reinterpret_cast` | n/a | Conditionally |
| `unions` | Conditionally | N |
| `std::start_lifetime_as` |

* Using `std::memcpy` is fine, in theory it starts a new object and copies the underlaying bytes. Note that the compiler tends remove the actual copy during optimization. Be aware that you need to manually take into account if the sizes/alignment/... match.
* Using `std::bit_cast` is better as it offloads several checks to the compiler and can be `constexpr`.
* Use placement `new` when converting a byte storage to an object. Beware you have to ensure the storage is properly aligned for the object type.
* C style casts are only valid if the cast is compatible with the effective type of the object pointed to, a qualified pointer, a signed/unsigned type related to the effective type or a `char` type.
* `reinterpret_cast`
* unions
* `std::start_lifetime_as`

## How can the compiler help?

Enable:
* `-fstrict-aliasing`
* `-Wstrict-aliasing`
* `-Wold-style-cast`

Sanitizer:
* Address sanitizer: `-fsanitize=address`
* Type sanitizer: `-fsanitize=type` (experimental)

## Examples

`std::bit_cast`:
```C++
[[nodiscard]] constexpr float int_to_float_bit_cast(int x) noexcept
{
    return std::bit_cast<float>(x);
}
```

`std::memcpy`:
```C++
[[nodiscard]] float int_to_float_memcpy(int x) noexcept
{
    float destination;
    std::memcpy(&destination, &x, sizeof(x));
    return destination;
}
```

placement `new`:
```C++
[[nodiscard]] float int_to_float_placement(int x) noexcept
{
    new(&x) float;
    return *std::launder(reinterpret_cast<float*>(&x));
}
```

> Aligned storage (needs fixing)
```
std::aligned_storage_t<sizeof(X), alignof(X)> storage;
X* p - new (&storage) X;
```


# References

* [Type aliasing](https://en.cppreference.com/w/cpp/language/reinterpret_cast#Type_aliasing)
* [Type punning in modern C++ - Timur Doumler - CppCon 2019](https://www.youtube.com/watch?v=_qzMpk-22cc)


# Scratchpad




## How to use it
https://stackoverflow.com/questions/67636231/what-is-the-modern-correct-way-to-do-type-punning-in-c

OK methods:

* `std::start_lifetime_as` -> ok
  Does not copy the data, kind of like placement new without calling the constructor.
* placement new + aligned storage...
* std::start_lifetime_as
  trival constructors

NOK Methods in C and C++:
* unions -> conditionally ok in C, UB in C++
  Invalid in C++
  Valic in C as long as the type used to read is not larger then the type used to write to
* `reinterpret_cast`, conditionally ok in C++
  Ok if converting a type from/to a byte reprentation (`char`, `unsigned char` or `std::byte`) (type accessability)

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
 
 
