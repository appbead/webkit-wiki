# Building QtWebKit on OS X

### Prerequisites

The best way to install all needed software is via [Homebrew](http://brew.sh)

You need to install:
* XCode - https://developer.apple.com/downloads
* XCode Command Line Tools - (after you installed XCode) `xcode-select --install`
* CMake
* Qt 5 (minimum supported version is 5.2)
* libpng

### Quick installation of some dependencies
```
brew install libpng cmake
```

### Building

If you don't have `qmake` in your `$PATH`, you must provide the path to it via `-DCMAKE_PREFIX_PATH`:

```
./Tools/Scripts/build-webkit --qt --cmakeargs="-Wno-dev -DCMAKE_PREFIX_PATH=<path_to_your_Qt_installation>"
```

For example, if you have Qt 5.6 installed in `$HOME/Qt`, then the command will be:
```
./Tools/Scripts/build-webkit --qt --cmakeargs="-Wno-dev -DCMAKE_PREFIX_PATH=/Users/vitaly/Qt/5.6/clang_x64"
```
