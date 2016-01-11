Please write to webkit-qt@lists.webkit.org mailing list in case you are willing to help QtWebKit project!

Here is a list of things that will greatly help QtWebKit project and will help you to learn more about it before diving deeper:

### Improve build system and scripts

You will need some experience with CMake and qmake build systems, knowledge of Perl and/or Python will help. No advanced C++ skills are needed to take these items.

* Allow QtWebKit to be properly configured with CMake on Windows and OS X (though compilation fixes are welcome too!)
* Improve Qt-specific parts of build system to follow best practices
* Identify and port missing features of old qmake-based build system to CMake, e.g., -fdebug-types-section and force_static_libs_as_shared. Upstream changes which are not specific to Qt.
* Refactor CMake files to minimize amount of Qt-specific code (work with upstream)
* Analyze scripts which were used for QtWebkit testing in past, compare with what WebKit project uses today, restore/reimplement Qt-specific bits were appropriate

### Support non-Linux platforms

In particular, the next platforms are very desirable to have support for:

* OS X (>= 10.10)
* Windows (>= 7) without WebKit 2 API (MinGW or MSVC >= 2015)
* Linux on 32-bit x86 (just needs testing) and other CPU architectures (amount of needed work will vary a lot)
* Other POSIX-compliant operating systems like *BSD, with Clang or GNU toolchain