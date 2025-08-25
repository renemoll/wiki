---
title: Type punning
description: 
published: true
date: 2025-08-25T18:50:06.617Z
tags: 
editor: markdown
dateCreated: 2025-05-16T14:04:22.085Z
---

# Type punning

## Introduction

### What is it

Type punning is a programming technique using an object of a specific type as if it is another type Also see [Wikipedia](https://en.wikipedia.org/wiki/Type_punning). Another way to look at it is to change the view of the underlying data of an object.

### Why use it

Type punning can be used for:
* Manual optimizations, i.e. fast(er) computations;
* Serialization/deserialization of data structures;
* Low-level communication handling.

By taking the original object and representing it as something else, i.e. floats as integers or bytes and vice versa.

### What is the problem?

In general it is not a good idea to do type punning, as you are bypassing the type system. However, sometimes you may need it for low-level data manipulation. If you do need to use type punning, better use a proper method.

There are several methods to perform type punning, more than the standard specifies. This means there is a good chance you have to deal with undefined behaviour or non-portable code.

Is that a problem? That depends on what you want to achieve.

## The problem

The problems are explained very well by others, so I will refer to this article: [What is the Strict Aliasing Rule and Why do we care?](https://gist.github.com/shafik/848ae25ee209f698763cffee272a58f8)

## How to type pun

### Use-case: convert between two types

Method | Valid C | Valid C++
| --- | --- | --- |
| `std::bit_cast` (from C++20) | n/a | Y |
| `std::memcpy` | Y | Y |
| C style casts | Conditionally | N |
| `unions` | Conditionally | N |

* Using `std::bit_cast` is an improved variant of using `std::memcpy` as it will perform the conversion, performs several checks at compile time and can be `constexpr`.
* Using `std::memcpy` is fine as it starts a new object and copies the underlying bytes. Note that the compiler tends to remove the actual copy during optimization. Be aware that you need to manually verify that the size and alignment match and the type is trivially copyable.
* C style casts are only valid if the cast is compatible with the effective type of the object pointed to, a qualified pointer, a signed/unsigned type related to the effective type or a `char` type.
* In C, unions can be used to convert between two types, given they are compatible.

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
    float result;
    std::memcpy(&result, &x, sizeof(x));
    return result;
}
```

### Use-case: convert an object to an array of bytes

Method | Valid C | Valid C++
| --- | --- | --- |
| `std::bit_cast` (from C++20) | n/a | Y |
| `std::memcpy` | Y | Y |
| `reinterpret_cast` | n/a | N* |

* `reinterpret_cast` is valid when casting to a byte representation. Using that byte representation is undefined behaviour for now.

Converting an object in bytes using `std::bit_cast`:
```C++
[[nodiscard]] std::array<std::byte, 4> int_to_bytes_bit_cast(int x) noexcept
{
    return std::bit_cast<std::array<std::byte, 4>>(x);
}
```

Converting an object in bytes using `std::memcpy`:
```C++
[[nodiscard]] std::array<std::byte, 4> int_to_bytes_memcpy(int x) noexcept
{
    std::array<std::byte, 4> result = {};
    std::memcpy(&result, &x, sizeof(x));
    return result;
}
```

### Use-case: convert an array of bytes to an object

Method | Valid C | Valid C++
| --- | --- | --- |
| `std::bit_cast` (from C++20) | n/a | Y |
| `std::start_lifetime_as` (from C++23) | n/a | Y |
| placement `new` | n/a | Y |
| `std::memcpy` | Y | Y |

* `std::start_lifetime_as` can be used to start a new object given an array of bytes. Of course, the storage must be aligned for the desired type, and the type must be trivially copyable. Note that `std::start_lifetime_as` does not call any constructor.
* Use placement `new` to construct an object on a given storage and call the constructor. Again, beware that the storage is properly aligned for the object type.

```C++
[[nodiscard]] int bytes_to_int_bit_cast(std::array<std::byte, 4> x) noexcept
{
    return std::bit_cast<int>(x);
}
```

```C++
[[nodiscard]] int bytes_to_int_lifetime(std::array<std::byte, 4> x) noexcept
{
    return *start_lifetime_as<int>(x.data());
}
```

## How can the compiler help?

Enable:
* `-fstrict-aliasing`
* `-Wstrict-aliasing`
* `-Wold-style-cast`

Sanitizer:
* Address sanitizer: `-fsanitize=address`
* Undefined Behavior sanitizer: `-fsanitize=undefined`
* Type sanitizer: `-fsanitize=type` (experimental)

## References

* C++ reference - [Type aliasing](https://en.cppreference.com/w/cpp/language/reinterpret_cast#Type_aliasing)
* [What is the Strict Aliasing Rule and Why do we care?](https://gist.github.com/shafik/848ae25ee209f698763cffee272a58f8) ([alternative](https://accu.org/journals/overload/28/160/anonymous/))
* [Type punning in modern C++ - Timur Doumler - CppCon 2019](https://www.youtube.com/watch?v=_qzMpk-22cc)
* [Taking a Byte Out of C++ - Avoiding Punning by Starting Lifetimes - Robert Leahy - CppCon 2022](https://www.youtube.com/watch?v=pbkQG09grFw)
* [The correct way to do type punning in C++](https://andreasfertig.com/blog/2025/03/the-correct-way-to-do-type-punning-in-cpp/)
* [The correct way to do type punning in C++ - The second act](https://andreasfertig.com/blog/2025/04/the-correct-way-to-do-type-punning-in-cpp-the-second-act/)
* [Practical Type Punning in C++11 and higher](https://blog.hiebl.cc/posts/practical-type-punning-in-cpp/)
* [What is the modern, correct way to do type punning in C++?](https://stackoverflow.com/questions/67636231/what-is-the-modern-correct-way-to-do-type-punning-in-c)
* C++ Core Guidelines - [C.183: Don’t use a union for type punning](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Ru-pun)


 
 
