# Requirements
You must have following programs in your `PATH` environment variable:

* Visual Studio 2015 **IMPORTANT:** due to modern C++11 features, VS2015 is the minimum supported version. Visual Studio 2015 Community will be enough to build QtWebkit.
* Qt >= 5.6 - http://www.qt.io/developers
* CMake >= 2.8.12
* Ruby >= 1.9 - you can download convenient installer [here](http://rubyinstaller.org)
* Perl (5.22 or 5.20) - [ActivePerl](http://www.activestate.com/activeperl) by ActiveState will be enough.
* Python - we heavily advise to use 2.7 version. Python 3 is not officially supported.

Following requirements you can download [here](http://gnuwin32.sourceforge.net):

* bison
* flex
* gperf

# Optional tools

* [ninja](https://ninja-build.org) - significantly increases the compilation speed.

# Building QtWebkit

_Optional step:_ You can change the default output build directory (`WebKitBuild`) by specifying environment variable `WEBKIT_OUTPUTDIR`.

Use the following command to build QtWebkit (don't forget to check `CMAKE_PREFIX_PATH`. It must point to your Qt installation directory):

```
perl Tools/Scripts/build-webkit --qt --release --cmakeargs="-Wno-dev -DCMAKE_PREFIX_PATH=c:\Qt\Qt5.6.0\5.6\msvc2015"
```

To build JSC only, replace `build-webkit` with `build-jsc`.

# TODO: Running tests

# FAQ

Q: When I use ninja to build QtWebkit I can't find any generated solution or project files for Visual Studio. How can I change that?

A: Both scripts (`build-webkit` and `build-jsc`) accepts the optional argument `--no-ninja` which disables `ninja`. But be aware, you can't mix MSVC build and ninja. They are not compatible. You must use different build directory (or just delete CMake cache).

Q: What architectures supported?

A: Primary architecture is x86_64 (64-bit). X86 is less supported and not tested well.