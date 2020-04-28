# CMake C++ Project Template

## Using Ninja

I used `ninja` instede of `make` because of fast performance. 

This is a C++ Project Template for me, I use it for all my C++ Projects.

## Division with a remainder library

Thank you for your interest in this project!

Are you just starting with `CMake` or C++?

Do you need some easy-to-use starting point, but one that has the basic moving parts you are likely going to need on any medium sized project?

Do you believe in test-driven development, or at the very lest — write your tests *together* with the feature code? If so you'd want to start your project pre-integrated with a good testing framework.

Divider is a minimal project that's kept deliberately very small. When you build it using CMake/make (see below) it generates:

 1. A tiny **static library** `lib/libdivision.a`,
 2. **A command line binary `bin/divider`**, which links with the library,
 3. **An executable unit test** `bin/divider_tests`  using [Google Test library](https://github.com/google/googletest).

## Usage

### Prerequisites

You will need:

 * A modern C/C++ compiler
 * CMake & Ninja installed (on a Arch Linux, run `pacman -S cmake ninja`)
 
### Building The Project

#### Git Clone

First we need to check out the git repo:

```bash
❯ mkdir ~/workspace
❯ cd ~/workspace
❯ git clone \
    https://github.com/SakibFarhad/cmake-project-template \
    my-project
❯ cd my-project
```

#### Project Structure

`lib`, `bin` directory will be created automatically. Those are populated by `ninja install`.

The rest should be obvious: `src` is the sources, `include` for headers and `test` is where we put our unit tests.

Now we can build this project, and below we show three separate ways to do so.

#### Building Manually

```bash
❯ rm -rf build && mkdir build
❯ git submodule init && git submodule update
❯ cd build
❯ cmake -G Ninja ..
❯ ninja && ninja install
❯ cd ..
```


#### Running the tests

```bash
❯ bin/divider_tests
[==========] Running 5 tests from 1 test case.
[----------] Global test environment set-up.
[----------] 5 tests from DividerTest
[ RUN      ] DividerTest.5_DivideBy_2
[       OK ] DividerTest.5_DivideBy_2 (1 ms)
[ RUN      ] DividerTest.9_DivideBy_3
[       OK ] DividerTest.9_DivideBy_3 (0 ms)
[ RUN      ] DividerTest.17_DivideBy_19
[       OK ] DividerTest.17_DivideBy_19 (0 ms)
[ RUN      ] DividerTest.Long_DivideBy_Long
[       OK ] DividerTest.Long_DivideBy_Long (0 ms)
[ RUN      ] DividerTest.DivisionByZero
[       OK ] DividerTest.DivisionByZero (0 ms)
[----------] 5 tests from DividerTest (1 ms total)

[----------] Global test environment tear-down
[==========] 5 tests from 1 test case ran. (1 ms total)
[  PASSED  ] 5 tests.
```

#### Running the CLI Executable

Without arguments, it prints out its usage:

```bash
❯ bin/simple_divider

Divider © 2020 Brick Inc.

Usage:
	simple_divider <numerator> <denominator>

Description:
	Computes the result of a fractional division,
	and reports both the result and the remainder.
```

But with arguments, it computes as expected the denominator:

```bash
❯ bin/simple_divider 112443477 12309324

Divider © 2020 Brick Inc.

Division : 112443477 / 12309324 = 9
Remainder: 112443477 % 12309324 = 1659561
```

### Using it as a C++ Library

We build a static library that, given a simple fraction will return the integer result of the division, and the remainder.

We can use it from C++ like so:

```cpp
#include <iostream>
#include <division>

Fraction       f = Fraction{25, 7};
DivisionResult r = Division(f).divide();

std::cout << "Result of the division is " << r.division;
std::cout << "Remainder of the division is " << r.remainder;
```

## File Locations

 * `src/*` — C++ code that ultimately compiles into a library
 * `include/*` — C++ header files
 * `test/lib` — C++ libraries used for tests (eg, Google Test)
 * `test/src` — C++ test suite
 * `bin/`, `lib` are all empty directories, until the `ninja install` install the project artifacts there.

Tests:

 * A `test` folder with the automated tests and fixtures that mimics the directory structure of `src`.
 * For every C++ file in `src/A/B/<name>.cpp` there is a corresponding test file `test/A/B/<name>_test.cpp`
 * Tests compile into a single binary `test/bin/runner` that is run on a command line to run the tests.
 * `test/lib` folder with a git submodule in `test/lib/googletest`, and possibly other libraries.

#### Contributing

**Pull Requests are WELCOME!** Please submit any fixes or improvements, and I promise to review it as soon as I can at the project URL:

 * [Project Github Home](https://github.com/SakibFarhad/cmake-project-template)
 * [Submit Issues](https://github.com/SakibFarhad/cmake-project-template/issues)
 * [Pull Requests](https://github.com/SakibFarhad/cmake-project-template/pulls)

### License

&copy; 2017-2020 Md. Sakib Ibne Farhad.

Open sourced under MIT license, the terms of which can be read here — [MIT License](http://opensource.org/licenses/MIT).

### Acknowledgements

This project is a derivative of the [CMake Tutorial](https://cmake.org/cmake-tutorial/), and is aimed at saving time for starting new projects in C++ that use CMake and GoogleTest.
