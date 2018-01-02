test262_harness_cpp
===================

Source code and projects for a test harness that is able to run tests from the [Official ECMAScript Conformance Test Suite](https://github.com/tc39/test262) over several C / C++ Javascript / ECMAScript runtimes available on the net.

Simply include the source code of the Javascript / ECMAScript engine of your choice into the project, plus the runtime that is associated with the engine, and you're ready to go.

Support for the following Javascript / ECMAScript engines is included:

* Duktape
* TinyJS
* TinyJS's 42tiny_js branch

Other C / C++ engines can be easily added, as long as they can be added to the project either as source code or libraries - examine the various runtime_***.h/.cpp sources to give you an idea
of how the engine is expected to be called for the various test.

The source code of the test harness is written in C++, without external dependencies on third-party libraries - except for the runtimes themselves. test262_harness_cpp runs as a command-line application, which expects the following arguments:

* -t /path/to/tests/directory : The directory that contains the test262 tests. Point it to the top-level directory that contains the /test and /harness directories.
* -o /path/to/output/results.txt : The path to the results file containing the fail/pass status of the various tests in the suite.

The following is an example of the output results file generated by test262_harness_cpp when run against Duktape:

```
[->PASS:NON_STRICT<-] /Users/heribertodelgado/Projects/test262-master/test/annexB/built-ins/escape/escape-above-astral.js
[->PASS:STRICT<-] /Users/heribertodelgado/Projects/test262-master/test/annexB/built-ins/escape/escape-above-astral.js
[->FAIL:NON_STRICT<-] /Users/heribertodelgado/Projects/test262-master/test/annexB/built-ins/escape/to-string-err-symbol.js
ReferenceError -  identifier 'Symbol' undefined
[->FAIL:STRICT<-] /Users/heribertodelgado/Projects/test262-master/test/annexB/built-ins/escape/to-string-err-symbol.js
ReferenceError -  identifier 'Symbol' undefined
[->PASS:NON_STRICT<-] /Users/heribertodelgado/Projects/test262-master/test/annexB/built-ins/escape/prop-desc.js
[->PASS:STRICT<-] /Users/heribertodelgado/Projects/test262-master/test/annexB/built-ins/escape/prop-desc.js
```

Compilation Instructions
------------------------

Included with test262_harness_cpp is an Xcode 8.2 project that includes the main components of the test harness. The command-line application can also be compiled for other platforms, provided that you specify an appropriate implementation of directories.h / .cpp for your platform.

To create the command-line application using the supplied components:

MacOS:
* Rename directories_posix.h / .cpp in the project folder to directories.h / .cpp
* Rename runtime_duktape.h / .cpp, or runtime_tinyjs.h / .cpp or runtime_42tinyjs.h / .cpp (depending on the Javascript / ECMAScript engine you chose to run the tests) to runtime.h / .cpp
* Open the test262_harness_cpp project by using Xcode 8.2 or later
* Include all the renamed .h / .cpp files into the newly opened project
* Include the source code files of the engine you chose into the project
* Build the project (either by using Project / Build or clicking on the Run button in Xcode.)

Other platforms:
* Create a copy of directories_posix.h / .cpp and provide a suitable implementation for your platform if it's not POSIX-compliant already, and rename it to directories.h / .cpp
* Rename runtime_duktape.h / .cpp, or runtime_tinyjs.h / .cpp or runtime_42tinyjs.h / .cpp (depending on the Javascript / ECMAScript engine you chose to run the tests) to runtime.h / .cpp
* Include the files harness.h / .cpp, metadata.h / .cpp, main.cpp, and all copied / renamed files into your build system.
* Include the source code or libraries of the Javascript / ECMAScript engine you chose into the build ssystem
* Invoke the build command of your build system.

Licensing
---------

The project is provided under the terms of the [MIT License](https://opensource.org/licenses/MIT). Feel free to use this project and modify it to your leisure in order to run the tests of the Javascript / ECMAScript engine of your choice.