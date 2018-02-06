# Building QtWebKit on OS X

### Prerequisites

The best way to install all needed software is via [Homebrew](http://brew.sh)

You need to install:
* XCode - https://developer.apple.com/downloads
* XCode Command Line Tools - (after you installed XCode) `xcode-select --install`
* CMake
* Qt 5 (minimum supported version is 5.2)
* libpng
* libjpeg or libjpeg-turbo

### Quick installation of some dependencies
```
# For buildng with Qt >= 5.10
brew install libpng libjpeg-turbo cmake
# For building with Qt < 5.10
brew install libpng libjpeg cmake
```

### Optional tools

* [ninja](https://ninja-build.org) - significantly increases the compilation speed.
```
brew install ninja
```

### Warning

`Mono.framework` presence on build machine is known to deceive CMake into using its headers for libraries like libpng and sqlite. It leads to crashes when using built QtWebKit. Please remove it before proceeding to the next step.

**UPD** Maybe setting `CMAKE_FIND_FRAMEWORK` to `LAST` can help

### Building

If you don't have `qmake` in your `$PATH`, you must provide the path to it via `-DQt5_DIR`:

```
./Tools/Scripts/build-webkit --qt --cmakeargs="-Wno-dev -DQt5_DIR=<path_to_your_Qt_installation>/lib/cmake/Qt5"
```

In case of Qt >= 5.10 you may also need to help cmake with finding libjpeg-turbo. Following cmake arguments should be used:
```
-DJPEG_LIBRARY=/usr/local/opt/jpeg-turbo/lib/libturbojpeg.0.dylib -DJPEG_INCLUDE_DIR=/usr/local/opt/jpeg-turbo/include
```

For example, if you have Qt 5.10 installed in `$HOME/Qt`, then the command will be:
```
./Tools/Scripts/build-webkit --qt --cmakeargs="-Wno-dev -DQt5_DIR=$HOME/Qt/5.10/clang_64/lib/cmake/Qt5 -DJPEG_LIBRARY=/usr/local/opt/jpeg-turbo/lib/libturbojpeg.0.dylib -DJPEG_INCLUDE_DIR=/usr/local/opt/jpeg-turbo/include"
```

Then you need to install resulting binaries. If your build was using ninja, run
```
ninja -C WebKitBuild/Release install
```
otherwise
```
make -C WebKitBuild/Release install
```

QtWebKit will be installed into your Qt directory, side by side with other Qt modules, and will be available for building your projects.

### Troubleshoot

* Application crashes on macOS in `WebCore::PNGImageDecoder::decode` on `setjmp` call

PNG headers don't match used library, see section **Warning** above.