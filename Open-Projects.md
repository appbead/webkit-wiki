If you want to help us and start contributing to QtWebKit project, here is a list of thing that you can start from.

### Improve build system and scripts

You will need some experience with CMake and qmake build systems, knowledge of Perl and/or Python will help. No advanced C++ skills are needed to take these items.

* Allow QtWebKit to be properly configured with CMake on Windows and OS X (though compilation fixes are welcome too!)
* Improve Qt-specific parts of build system to follow best practices
* Identify and port missing features of old qmake-based build system to CMake, e.g., -fdebug-types-section and force_static_libs_as_shared. Upstream changes which are not specific to Qt.
* Refactor CMake files to minimize amount of Qt-specific code (work with upstream)