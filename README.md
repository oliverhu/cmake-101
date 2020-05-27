## What is CMake?

Make (or rather a Makefile) is a buildsystem - it drives the compiler and other build tools to build your code. CMake is a generator of buildsystems. It can produce Makefiles, it can produce Ninja build files, it can produce KDEvelop or Xcode projects, it can produce Visual Studio solutions.

## Why learn CMake?

I've primarily exposed to the Java build system. Want to get some basic understanding of the build systems for C/C++, recent projects require me to have a good grip of C/C++ projects.

This project is a mix of many open source blogs & projects for record. The default documentation on CMake official website is as bad as many other open source projects.

## Prereq
$ sudo apt install libboost-dev
$ sudo apt install libboost-all-dev

## Q & A

> Q: I  am new to CMake and a bit confused with the PUBLIC, PRIVATE and INTERFACE keywords related to target_link_libraries(). Documentation mentions that they can be used to specify both the link dependencies and the link interface in one command. What does link dependencies and link interface actually mean?

A: If you are creating a shared library and your source cpp files #include the headers of another library (Say, QtNetwork for example), but your header files don't include QtNetwork headers, then QtNetwork is a PRIVATE dependency.

If your source files and your headers include the headers of another library, then it is a PUBLIC dependency.

If your header files but not your source files include the headers of another library, then it is an INTERFACE dependency.

Other build properties of PUBLIC and INTERFACE dependencies are propagated to consuming libraries. http://www.cmake.org/cmake/help/v3.0/manual/cmake-buildsystem.7.html#transitive-usage-requirements

## References

https://tuannguyen68.gitbooks.io/learning-cmake-a-beginner-s-guide/content/chap1/chap1.html (only chap1 works)

http://derekmolloy.ie/hello-world-introductions-to-cmake/

https://cliutils.gitlab.io/modern-cmake/
