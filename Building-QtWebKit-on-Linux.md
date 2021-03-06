You need to install the next dependencies:

* Qt >= 5.4 (Core, Gui, Network, Sql, OpenGL, Test, Widgets, Positioning, Sensors)
    * For QML API: Declarative, WebChannel (or you can disable it with -DENABLE_WEBKIT2=OFF cmake flag)
* CMake >= 2.8.12 (>= 3.2 is recommended)
* ninja
* sqlite >= 3.6.16
* ICU >= 52.1
* ruby >= 1.9
* perl >= 5.10.0
* python 2.7.x
* bison >= 2.1
* flex >= 2.5.34
* gperf >= 3.0.1
* libxml2 >= 2.8.0 (2.6.x will probably work)
* libxslt >= 1.1.7
* libjpeg v8 or v9 (IJG) or libjpeg-turbo
* libpng
* zlib
* libhyphen
* glib >= 2.36 (gio, gobject)
* gstreamer >= 1.0.3 (app, pbutils, video, mpegts, tag, audio, fft); you also need GStreamer 1.0 plugins for codec support

Optional dependencies:
* fontconfig
* libwebp

> Q: Why do you have so many dependencies?

> A: See [[FAQ]]

For Ubuntu use the next command

    sudo apt-get install build-essential perl python ruby flex gperf bison cmake \
    ninja-build libfontconfig1-dev libicu-dev libsqlite3-dev zlib1g-dev libpng12-dev \
    libjpeg-dev libxslt1-dev libxml2-dev libhyphen-dev

You can then build QtWebKit with cmake:

    mkdir -p WebKitBuild/Release
    cd WebKitBuild/Release
    cmake -DPORT=Qt -DCMAKE_BUILD_TYPE=Release ../..
    make -jN # Replace N with number of your CPU cores
    sudo make install

If you are not using system-wide installation of Qt, you should add `-DQt5_DIR=$your_Qt_path/lib/cmake/Qt5` to cmake arguments, e.g.

    cmake -DPORT=Qt -DCMAKE_BUILD_TYPE=Release \
        -DQt5_DIR=/opt/Qt5.8.0/5.8/gcc_64/lib/cmake/Qt5 ../..

Note: this manual previously suggested using CMAKE_PREFIX_PATH, but it may cause build errors related to misdetection of ICU libraries with Qt SDK 5.8.0 and 5.9.0

### Cross-compilation

Cross-compilation with CMake is described in [official CMake documentation](https://cmake.org/cmake/help/v3.0/manual/cmake-toolchains.7.html#cross-compiling). Basically, you need CMake toolchain file (for example, see ToolchainMIPS.cmake in the root of this repository), and all required dependencies compiled for your target. In order to reduce number of dependencies, you may want to disable some features.

### Building for running test suite

If you're contributing to QtWebKit, optionally run the `Tools/Scripts/update-qtwebkit-libs` script (see [JHBuild](https://github.com/annulen/webkit/wiki/JHBuild)) to build all dependencies inside the source tree, in order to get reproducible test results. Then use the `build-webkit` script to get separate debug/release builds:

    Tools/Scripts/build-webkit --qt --release  # or --debug

### Installation

Currently you have to install QtWebKit in order to build your applications against it. Installation prefix is controlled by `CMAKE_INSTALL_PREFIX` variable, you may even set it to your Qt prefix (*warning*: it will replace existing QtWebKit files if you have one installed!).

Run the following command to perform installation:

    cd WebKitBuild/Release && sudo make install

or if you build with `ninja` (default behavior of `build-webkit`, if `ninja` is installed):

    cd WebKitBuild/Release && sudo ninja install

### Installation Troubleshoot

If you are building with ninja and see error like this:
```
CMake Error at Source/WebKit/cmake_install.cmake:129 (FILE):
  file INSTALL cannot find
  "/mnt/ssd2/WebKit/WebKit-new-qt-stable/WebKitBuild/Release/Source/WebKit/CMakeFiles/CMakeRelink.dir/libQt5WebKitWidgets.so.5.602.1".
Call Stack (most recent call first):
  Source/cmake_install.cmake:94 (INCLUDE)
  cmake_install.cmake:37 (INCLUDE)
```
run the next command:
```
sed -ie 's|Source/WebKit/CMakeFiles/CMakeRelink\.dir|lib|' Source/WebKit/cmake_install.cmake
sed -ie 's|Source/WebKit/qt/declarative/CMakeFiles/CMakeRelink\.dir|imports/QtWebKit|' Source/WebKit/qt/declarative/cmake_install.cmake
sed -ie 's|Source/WebKit/qt/declarative/experimental/CMakeFiles/CMakeRelink\.dir|imports/QtWebKit/experimental|' Source/WebKit/qt/declarative/experimental/cmake_install.cmake
```

Another solution is building with `CMAKE_BUILD_WITH_INSTALL_RPATH=ON`, but in this case binaries won't run before installation without setting LD_LIBRARY_PATH

### Building only JSC

To build only JSC, replace `build-webkit` with `build-jsc`

Use this command to run JSC tests:

    Tools/Scripts/run-layout-jsc -t LayoutTests/ -j build/qt-jsc/Release/bin/jsc -r results