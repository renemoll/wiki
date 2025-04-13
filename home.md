---
title: Wiki
description: 
published: true
date: 2025-04-13T21:46:26.872Z
tags: 
editor: markdown
dateCreated: 2024-03-26T11:44:10.044Z
---

# Notes on

[Improving C++ Compilation Times: Tools & Techniques - Vittorio Romeo - ACCU 2023](https://www.youtube.com/watch?v=PfHD3BsVsAM)
[Slides](https://accu.org/conf-docs/PDFs_2023/XImprovingCompilationTimesToolsandTechniques.pdf)

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

It’s Not As Simple As “Use A Memory Safe Language"
- https://www.youtube.com/watch?v=iQ-eTaW6-cM

C++ lets you do the wrong thing easily (by default)


Quality markers -> Tools used?
 - static analysis
 - undefined behavior interpreter
 - model checking
 - property testing
 - fuzzing
 - dynamic analysis
 - isolated execution
 - resource limits

#


* https://damirlj.substack.com/p/lock-free-message-queue
* https://www.geeksforgeeks.org/hexagonal-architecture-system-design/
* https://github.com/cloudyourcar
* https://en.cppreference.com/w/cpp/utility/source_location
* https://openlibrary.org/
* https://untools.co/
* https://github.com/mastupristi/memoryLayout
* https://www.sonarsource.com/products/sonarlint/
* https://isocpp.org/blog/2019/09/cppcon-2019-de-fragmenting-cpp-making-exceptions-and-rtti-more-affordable-a
* https://www.open-std.org/jtc1/sc22/wg21/docs/papers/2018/p1105r1.html
* https://dev.jimgrey.net/2024/07/03/lessons-learned-in-35-years-of-making-software/
* https://www.developertoarchitect.com/lessons/
* https://vitaut.net/posts/2024/binary-size/
* https://softwaredoug.com/blog/2024/09/07/your-team-needs-juniors
* https://read.perspectiveship.com/p/one-on-ones

* https://hackaday.com/2024/10/17/ubiquitous-successful-bus-version-2/

* https://spectrum.ieee.org/lean-software-development
* https://berthub.eu/articles/posts/a-2024-plea-for-lean-software/

* https://github.com/pyladiesams/intro-to-explainabilty-in-finance-oct2024

* https://github.com/qnope/Erased
* https://godbolt.org/#g:!((g:!((g:!((g:!((h:codeEditor,i:(j:1,source:'class+Rect%0A%7B%0A++++int+a%3B%0A++++float+b%3B%0Apublic:%0A++++constexpr+Rect(int+a,+float+b)%0A++++:+a(a),b(b)%7B%7D%0A%7D%3B%0A%0Aint+main()%0A%7B%0A++++constexpr+Rect+rect+%3D+Rect(1,2.0f)%3B%0A%7D'),l:'5',n:'0',o:'C%2B%2B+source+%231',t:'0')),k:100,l:'4',m:51.694915254237294,n:'0',o:'',s:0,t:'0'),(g:!((h:codeEditor,i:(j:2,source:'class+Rect%0A%7B%0A++++int+a%3B%0A++++float+b%3B%0Apublic:%0A++++Rect(int+a,+float+b)%0A++++:+a(a),b(b)%7B%7D%0A%7D%3B%0A%0Aint+main()%0A%7B%0A++++Rect+rect+%3D+Rect(1,2.0f)%3B%0A%7D'),l:'5',n:'0',o:'C%2B%2B+source+%232',t:'0')),header:(),k:100,l:'4',m:48.30508474576271,n:'0',o:'',s:0,t:'0')),k:34.75791334251309,l:'3',n:'0',o:'',t:'0'),(g:!((h:compiler,i:(compiler:g63,filters:(b:'0',commentOnly:'0',directives:'0',intel:'0'),options:'-std%3Dc%2B%2B11+-O0',source:1),l:'5',n:'0',o:'x86-64+gcc+6.3+(Editor+%231,+Compiler+%231)',t:'0')),header:(),k:28.154966278965773,l:'4',n:'0',o:'',s:0,t:'0'),(g:!((h:compiler,i:(compiler:g63,filters:(b:'0',commentOnly:'0',directives:'0',intel:'0'),options:'-std%3Dc%2B%2B11+-O0',source:2),l:'5',n:'0',o:'x86-64+gcc+6.3+(Editor+%232,+Compiler+%232)',t:'0')),header:(),k:37.08712037852113,l:'4',n:'0',o:'',s:0,t:'0')),l:'2',n:'0',o:'',t:'0')),version:4
* https://bitbashing.io/comparing-floats.html
* https://www.kitware.com/navigating-cmake-dependencies-with-cps/
* https://berthub.eu/articles/posts/on-long-term-software-development/
* https://github.com/perghosh/Data-oriented-design/wiki/Imperative-vs-declarative
* https://www.cl.cam.ac.uk/archive/rja14/book.html
* https://berthub.eu/articles/posts/totemic-books-for-many-fields/
* https://berthub.eu/articles/posts/tracking-free-audience-statistics/

memory safety & code analysis
* https://github.com/google/syzkaller
* https://codeql.github.com/docs/codeql-overview/supported-languages-and-frameworks/
* https://chromium.googlesource.com/chromium/src/+/HEAD/docs/dangling_ptr.md
* https://github.com/microsoft/binskim
* https://github.com/ossf/Memory-Safety/blob/main/docs/best-practice-non-memory-safe-by-default-languages.md
* https://memorysafety.openssf.org/memory-safety-continuum/
* https://github.com/Jarod42/ccccc
* https://github.com/frite/mccabe
* http://splint.org/
* https://covemountainsoftware.com/2021/03/01/a-survey-of-concurrency-bugs/
* https://github.com/lljbash/clangd-tidy?tab=readme-ov-file
* https://clang.llvm.org/docs/SafeBuffers.html#id5
* https://stackoverflow.com/questions/40325957/how-do-i-add-valgrind-tests-to-my-cmake-test-target
* https://github.com/jedrzejboczar/elf-size-analyze
* https://security.googleblog.com/2024/11/retrofitting-spatial-safety-to-hundreds.html?m=1#fn1
* http://www.moserware.com/2008/02/does-your-code-pass-turkey-test.html

embedded
* https://rtic.rs/2/book/en/
* https://community.arm.com/arm-community-blogs/b/tools-software-ides-blog/posts/what-is-new-in-llvm-19
* https://barenakedembedded.com/how-to-use-cpp-with-stm32-hal/
* https://github.com/4ms/mdrivlib/blob/main/target/stm32mp1/drivers/spi.hh
* https://www.kauailabs.com/public_files/vmx-pi/apidocs/hal_cpp/html/class_v_m_x_i_o.html#a86a61e3dff04ef7b10add6acf35d3ab9
* https://embeddedartistry.com/blog/2017/09/06/debugging-9-indispensable-rules/
* http://efton.sk/STM32/gotcha/index.html

cyber
* https://blog.google/technology/safety-security/tackling-cybersecurity-vulnerabilities-through-secure-by-design/
* https://berthub.eu/articles/posts/cyber-security-pre-war-reality-check/

