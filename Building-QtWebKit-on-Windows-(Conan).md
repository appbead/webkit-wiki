This approach is used currently in CI system for building release binaries.

### Preparation

There is no need to repeat this steps for each build, just do it when you build first time

* Install C++ compiler - this manual works only for **Visual Studio 2015 or 2017** or **MinGW version shipped with Qt SDK**. Using other versions of MinGW is possible but some adjustments to steps below will be needed (feel free to ask if you really need this). As for Visual Studio, **older versions just won't work**
* Install Perl >= 5.14 (e.g. ActivePerl or StrawberryPerl)
* Install Python 2.7 and Ruby >= 1.9
* (optionally, will speed up build a bit) Download Ninja from https://github.com/ninja-build/ninja/releases and put ninja.exe into location that it is present in `%PATH%`
* Install Conan (see https://www.conan.io/downloads)
* Run `conan remote add qtproject https://api.bintray.com/conan/qtproject/conan --insert`
* Clone git repositories:
```
git clone git://code.qt.io/qt/qt5.git
cd qt5
git checkout 5.9
perl init-repository --module-subset=qtbase,qtdeclarative
git clone git://code.qt.io/qt/qtwebkit.git
```
* Install Qt 5.9 binaries from http://download.qt.io/archive/qt/5.9

If you want to use different version of Qt, replace 5.9 in checkout command and in your download URL with required version.

You may also want to build Qt from git sources that you've just downloaded, in this case you may need to add more modules to `--module-subset`. Full configuration requires `qtlocation`, `qtsensors`, `qtwebchannel`, and in case of MinGW also `qtmultimedia`.

### Installing QtWebKit dependencies

* Make build directory, below I assume that it is `qt5-build/qtwebkit` at the same directory level as your `qt5`
* Run following command in the build directory 

# **NOTE: don't try to adjust Windows version in paths to your OS version, it must be used exactly as it's written**

MSVC 2015 32-bit:
```
conan install -f ..\..\qt5\coin\provisioning\qtci-windows-10-x86\conanfiles\qtwebkit.txt -s arch=x86 -s compiler="Visual Studio" -s compiler.version=14 -s compiler.runtime=MD -g cmake
```

MSVC 2015 64-bit:
```
conan install -f ..\..\qt5\coin\provisioning\qtci-windows-10-x86\conanfiles\qtwebkit.txt -s arch=x86_64 -s compiler="Visual Studio" -s compiler.version=14 -s compiler.runtime=MD -g cmake
```

MSVC 2017 32-bit:
```
conan install -f ..\..\qt5\coin\provisioning\qtci-windows-10-x86\conanfiles\qtwebkit.txt -s arch=x86 -s compiler="Visual Studio" -s compiler.version=15 -s compiler.runtime=MD -g cmake
```

MSVC 2017 64-bit:
```
conan install -f ..\..\qt5\coin\provisioning\qtci-windows-10-x86\conanfiles\qtwebkit.txt -s arch=x86_64 -s compiler="Visual Studio" -s compiler.version=15 -s compiler.runtime=MD -g cmake
```

MinGW-w64 5.3.0 32-bit as bundled with Qt:
```
conan install -f ..\..\qt5\coin\provisioning\qtci-windows-7-x86\conanfiles\qtwebkit.txt -s arch=x86 -s compiler=gcc -s compiler.version=5.3 -s compiler.libcxx="libstdc++11" -g cmake
```

### Building QtWebKit

* Set environment variable `SQLITE3SRCDIR` to absolute path of `qt5\qtbase\src\3rdparty\sqlite`, e.g.
```
set SQLITE3SRCDIR=c:\qt5\qtbase\src\3rdparty\sqlite
```
* In build directory, run following commands in shell where `qmake` and compiler are available, i.e. same setup that you use for building any qmake-based project normally.
```
qmake -r ../../qt5/qtwebkit
cd release
ninja
```
If you didn't install `ninja`, run command that is shown in qmake output, it is `jom` or `nmake` for MSVC, or `mingw32-make` for MinGW (use `-j` to specify number of parallel jobs)

For debug build, do `cd debug` instead of `cd release`.

If you need to rebuild QtWebKit later, e.g. after updating git sources, just go to `release` directory again and re-run the last command