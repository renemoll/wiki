---
title: Type punning
description: 
published: true
date: 2025-05-27T09:58:37.051Z
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

## Use-case: convert between two types

Method | Valid C | Valid C++
| --- | --- | --- |
| `std::bit_cast` | n/a | Y (from C++20) |
| `std::memcpy` | Y | Y |
| C style casts | Conditionally | N |
| `unions` | Conditionally | N |

* Using `std::bit_cast` is an improved variant of using `std::memcpy` as it will perform the convervsion, performs several checks at compile time and can be `constexpr`.
* Using `std::memcpy` is fine as it starts a new object and copies the underlaying bytes. Note that the compiler tends remove the actual copy during optimization. Be aware that you need to manually ensure the size and alignment match and the type is trivially copyable.
* C style casts are only valid if the cast is compatible with the effective type of the object pointed to, a qualified pointer, a signed/unsigned type related to the effective type or a `char` type.
* In C, unions can be used to convert between two types, given they are compatible.

## Use-case: convert an object to an array of bytes

Method | Valid C | Valid C++
| --- | --- | --- |
| `std::bit_cast` | n/a | Y (from C++20) |
| `std::memcpy` | Y | Y |
| `reinterpret_cast` | n/a | N* |

* `reinterpret_cast` is valid when casting to a byte representation, however using that byte representation is undefined (for now).

## Use-case: convert an array of bytes to an object

Method | Valid C | Valid C++
| --- | --- | --- |
| `std::bit_cast` (?) | n/a | Y (from C++20) |
| `std::memcpy` | Y | Y |
| `std::start_lifetime_as` | N | Y (from C++23)
| placement `new` | n/a | Y |

* `std::start_lifetime_as` can be used to start a new object given an array of bytes. Of course the storage must be aligned for the desired type and the type must be trivial copyable. Note that `std::start_lifetime_as` this does not call any constructor.
* Use placement `new` to construct an object on a given storage and call the constructor. Beware you have to ensure the storage is properly aligned for the object type.

## How can the compiler help?

Enable:
* `-fstrict-aliasing`
* `-Wstrict-aliasing`
* `-Wold-style-cast`

Sanitizer:
* Address sanitizer: `-fsanitize=address`
* Undefined Behavior sanitizer: `-fsanitize=undefined`
* Type sanitizer: `-fsanitize=type` (experimental)

## Examples

Converting between two types with `std::bit_cast`:
```C++
[[nodiscard]] constexpr float int_to_float_bit_cast(int x) noexcept
{
    return std::bit_cast<float>(x);
}
```

Converting between two types with `std::memcpy`:
```C++
[[nodiscard]] float int_to_float_memcpy(int x) noexcept
{
    float destination;
    std::memcpy(&destination, &x, sizeof(x));
    return destination;
}
```

Converting bytes to an object with placement `new`:
```C++ 
```

Converting bytes to an object with `std::start_lifetime_as`:
```C++

```

# References

* C++ reference - [Type aliasing](https://en.cppreference.com/w/cpp/language/reinterpret_cast#Type_aliasing)
* [Type punning in modern C++ - Timur Doumler - CppCon 2019](https://www.youtube.com/watch?v=_qzMpk-22cc)
* [The correct way to do type punning in C++](https://andreasfertig.com/blog/2025/03/the-correct-way-to-do-type-punning-in-cpp/)
* [The correct way to do type punning in C++ - The second act](https://andreasfertig.com/blog/2025/04/the-correct-way-to-do-type-punning-in-cpp-the-second-act/)
* [Practical Type Punning in C++11 and higher](https://blog.hiebl.cc/posts/practical-type-punning-in-cpp/)
* [What is the modern, correct way to do type punning in C++?](https://stackoverflow.com/questions/67636231/what-is-the-modern-correct-way-to-do-type-punning-in-c)
* C++ Core Guidelines - [C.183: Don’t use a union for type punning](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Ru-pun)

# Scratchpad


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


## How to use it


https://www.youtube.com/watch?v=pbkQG09grFw
* storage and lifetime are decoupled.

# TODO

1. https://stackoverflow.com/questions/72511754/safely-type-punning-pod-like-structures-in-place-in-c20

1. https://accu.org/journals/overload/28/160/anonymous/
   https://gist.github.com/shafik/848ae25ee209f698763cffee272a58f8
 
 
