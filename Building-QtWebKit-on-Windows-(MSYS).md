**WARNING: This document is a work in progress**

This instruction is based on guide https://wiki.qt.io/MinGW-64-bit#MinGW-builds_.28with_OpenSSL.2C_ICU_and_QtWebKit.29

### Obtain QtWebKit sources

You need to `mingw_build` branch from this repo.

### Install dependencies

* Qt SDK for MinGW
* MSYS2 (https://msys2.github.io/)
* Ninja (https://github.com/ninja-build/ninja/releases)
* CMake (you can install it with pacman as well, see below)

Launch MSYS2 shell and execute commands
```
# base-devel has much more than actually needed
# TODO: find precise package subset
     pacman -S base-devel

     pacman -S mingw32/mingw-w64-i686-libjpeg-turbo
     pacman -S mingw32/mingw-w64-i686-icu
     pacman -S mingw32/mingw-w64-i686-libpng
     pacman -S mingw32/mingw-w64-i686-sqlite3
     pacman -S mingw32/mingw-w64-i686-libwebp
```

Open "MinGW shell" link provided by Qt installation, cd to location of QtWebKit sources and do following:
```
mkdir build
cd build
cmake .. -DCMAKE_BUILD_TYPE=Release -G Ninja -DPORT=Qt -DCMAKE_PREFIX_PATH=c:\msys64\mingw32 -DENABLE_API_TESTS=OFF -DENABLE_TEST_SUPPORT=OFF
ninja QtTestBrowser
```

You may also need to extend `%PATH%` before running cmake, e.g. `set PATH=%PATH%;C:\Utils`

PATH without perl dlls:
```
PATH=C:\Qt\5.7\mingw53_32\bin;C:/Qt/Tools/mingw530_32\bin;C:\Python27\;C:\Python27\Scripts;C:\Windows\system32;C:\Windows;C:\Windows\System32\Wbem;C:\Program Files (x86)\Windows Kits\8.1\Windows Performance Toolkit\;C:\Windows\System32\WindowsPowerShell\v1.0\;C:\Strawberry\perl\bin;C:\Ruby23-x64\bin;C:\Utils\Conan\conan;C:\Utils\Conan.io\conan;C:\Utils\Conan.io\conan;C:\CMake\bin;C:\GnuWin32\bin  
```

### Building conan packages

* Install fresh msys2
* export PATH=/C/Qt/Tools/mingw530_32/bin:/C/Utils/Conan/conan:$PATH
* pacman -S make (don't want to use mingw32-make for uniformity, but...)
* Create conan.conf for MinGW

`conan install libxslt/1.1.29@annulen/stable --build=missing -o shared=True -o libxml2:shared=True -s compiler=gcc -s compiler.version=4.9 -s compiler.libcxx="libstdc++"`

` conan install libxslt/1.1.29@annulen/stable --build=missing -s compiler=gcc -s compiler.version=4.9 -s compiler.libcxx="libstdc++"`

### Building Qt
* Install DirectX SDK: http://www.microsoft.com/en-us/download/details.aspx?id=6812
* `set SQLITE3SRCDIR=..\qt5\qtbase\src\3rdparty\sqlite`
* `..\qt5\configure  -confirm-license -opensource -nomake examples -qt-zlib -qt-libpng -qt-libjpeg`
