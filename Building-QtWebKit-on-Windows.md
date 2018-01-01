# Requirements
You must have following programs in your `PATH` environment variable:

* Visual Studio >= 2015 **IMPORTANT:** due to modern C++11 features, VS2015 is the minimum supported version. Visual Studio 2015 Community will be enough to build QtWebkit.
* Qt >= 5.6 - http://www.qt.io/developers (older Qt versions may work as well, but you will need to build Qt yourself)
* CMake >= 2.8.12
* Ruby >= 1.9 - you can download convenient installer [here](http://rubyinstaller.org)
* Perl (5.22 or 5.20) - [ActivePerl](http://www.activestate.com/activeperl) by ActiveState will be enough.
* Python - we heavily advise to use 2.7 version. Python 3 is not officially supported.

You also need to clone http://code.qt.io/cgit/qt/qt5.git and add `gnuwin32/bin` from cloned repository into `%PATH%`.

**NOTE:** QtWebKit requires additional dependencies such as libpng, libjpeg, zlib, sqlite, etc. No needs to download and build them, the build script (`build-webkit`) downloads all necessary dependencies on first run and keeps them up to date.

**WARNING:** Building in Cygwin is not supported. Building in MSYS2 shell is possible with 3rd party patches, and only for MinGW compiler. For MSVC, use cmd.exe shell only.

# Optional tools

* [ninja](https://ninja-build.org) - significantly increases the compilation speed.

# Building QtWebkit

_Optional step:_ You can change the default output build directory (`WebKitBuild`) by specifying environment variable `WEBKIT_OUTPUTDIR`.

Due to [#705](../issues/705) if sources come from a release tarball create a `WebKitLibraries` directory in unpacked sources.

Use the following command to build QtWebkit:

```
perl Tools/Scripts/build-webkit --qt --release --cmakeargs="-Wno-dev -DCMAKE_PREFIX_PATH=c:\Qt\Qt5.6.0\5.6\msvc2015"
```
but paying attention to:

- this command dowloads 3rd party dependencies; most of them are statically built but icu is built dynamically so if you have Qt built with icu you should use the same version as precompiled and downloaded into `WebKitLibraries`)
- update `CMAKE_PREFIX_PATH` - it must point to your Qt installation directory
- replace `--release` to `--debug` if you want to build a debug build
- if you want 64bit build add to cmake args appropriate toolchain specification e.g. `-G \"Visual Studio 14 Win64\"` (it is important to prepend quotes with backslashes as options to cmake are already quoted)
- for debug build, due to libraries genenerated during build exceeding 2GB, it is required to select 64bit toolchain (not to confuse with target architecture) with additional flag to cmake: `-T host=x64` (it is safe to add this also to release builds but an important not is that this option requires cmake in version at least 3.8)
- if Qt configured without passing option `-opengl dynamic` it is required to add `-DQT_USES_GLES2_ONLY=ON` to cmake args
- keep compilation path short (path to sources of length 24 works with more than 56 fails due to command line length limit generated during build - generally the shorter the safer)

To build QtWebKit successfully you **must** follow these rules:

- Make sure you don't have `MSYS`, `Cygwin` or `MINGW` bin folders in your `PATH` variable.
- Make sure that path to the `bin` folder of `ActivePerl` listed first in your `PATH` variable. Git on Windows has its own Perl executable which doesn't work with WebKit scripts.

To build JSC only, replace `build-webkit` with `build-jsc`.

# TODO: Running tests

# FAQ

Q: When I use ninja to build QtWebkit I can't find any generated solution or project files for Visual Studio. How can I change that?

A: Both scripts (`build-webkit` and `build-jsc`) accepts the optional argument `--no-ninja` which disables `ninja`. But be aware, you can't mix MSVC build and ninja. They are not compatible. You must use different build directory (or just delete CMake cache).
