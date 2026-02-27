---
title: Error handling
description: 
published: true
date: 2026-02-27T15:01:51.122Z
tags: 
editor: markdown
dateCreated: 2026-02-27T10:58:02.909Z
---

# On error handling

How should I handle errors in my software? A question I have been pondering about for a bit the last few weeks. Is a specific strategy I can apply to everything, everywhere all at once? Should I use (more) exceptions and/or asserts? And how useful are those assert statements anyway, as they only work in debug builds. What about those design by contract and related philosophies, is that something I should look into?

Luckily I am not the only one asking these kinds of questions, so I did some reading and came to this article. The goal there is to summerize "general knowledge" and specialize towards guidelines.

## Different kinds of errors
> introduce user/system/bug
> explain issue with each

Lets start by categorizing the types of errors. From there we can specialize to specific strategies.

The main sources of errors are: user related, system related and bugs. Let's dive a bit deeper into each:
* *User errors* are **actions** from the person using your software and making a mistake or using it differently from your intentions. Note: not another programmer.
* *System errors* are responces from the operating system indicating that a certain request cannot be fullfilled. (what when a resource becomes unavailable? you may get a notification or an error when using the resource.)
* *Bugs* are errors originating from using the software/api incorrectly. 

User errors are not really errors the software has to fix. This may sound a bit strange, however I believe programmers should expect the user to do wrong thing at some point. Think of providing invalid input, delting a file your software needs, or even just pressing a button at the wrong time. Your software should handle these scenarios, by always parsing the input before taking further action.

System errors can be as unpredictable as user errors, most of the time you won't encounter any until that one time. The question to ask here is, is this an exceptional error or could this be expected? In other words, is it ok for the action to fail, maybe retry a few times, or is there nothing you can do to recover. And who decides what is exceptional or expected? If you write the complete application you can determine it on your own. If you are writing a library, or API, the user that said library/API will want to have a say.

Bugs, or programming errors, include a wide range of possible errors from invalid parameter values, to unexpected states, to buffer overflows, to division by zero, to rounding errors. Who should check what at which moment? Say you have a function with pre- and post-conditions, can you expect the called of your function to always adhere to the pre-conditions? Should your function check all inputs, all the time? Or do you accept that if the user of your function uses it wrong, they will get undefined behaviour?

## Guidelines

User errors are to be expected, a user can input anything and your application has to "deal" with it. This means parsing user input. (article on parsing vs validation)

System errors can ocour and require individual analysis on what to do.
> what is normal vs exceptional

Bugs should be prevented, otherwise found as soon as possible and fixed.
What can you do?
* Make APIs easy to use and hard to misuse
  * using strong types can avoid many checks (if this pointer not null, is this integer positive or negative)
* Use the tools available: compiler warnings, static analysis
* Test: BDD/TDD/ whatever type of test but do write tests and include corner cases (AI's can help with this)
* Run your test on your machine with dynamic analysis
* And finally, use run-time checks

> Perform detection as soon as possible, 
> How to reach as soon as possible:
> * detect issues at compile time
> * detect issues trough compiler warnings
>   * configuration -> use bob
> * detect issues trough static analysis
>    * integrate tools into the build
> * detect issues trough unit testing (with dynamic analysis)
>    * integrate tools into the build
>    * test edge cases (on exposes API)
> * detect issues trough runtime checks
>    * contracts/asserts/checks


# References

* [Choosing the right error handling strategy](https://www.foonathan.net/2016/09/error-handling-strategy/)



# Scratchpad


System error -> Wether or not the application needs to be robust against these errors depends on the application. Same applies to libraties. When you cannot gaurantee a working state, termination is the solution.

Programming errors are bugs and therefore should be fixed. 
 * should be caught as soon as possible.
 * for a library/module, it should be clear on the interface what goes wrong (not 10 levels deep in the call stack) to make it clear as a programmer error and nog a library error.

