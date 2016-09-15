**WARNING: This document is a work in progress**

This instruction os based on guide https://wiki.qt.io/MinGW-64-bit#MinGW-builds_.28with_OpenSSL.2C_ICU_and_QtWebKit.29

Install
* Qt SDK for MinGW
* MSYS2 (https://msys2.github.io/)
* CMake
* Ninja (https://github.com/ninja-build/ninja/releases)

Launch MSYS2 shell

Set up paths
```
  export PATH=$PATH:/c/Utils/CMake/cmake-3.6.2-win32-x86/bin/
# We will use MinGW shipped with Qt SDK
  export PATH=$PATH:/c/Qt/Tools/mingw530_32/bin/
# Add ninja to PATH
  export PATH=$PATH:/c/Utils/ 
```

Install dependencies
```
     pacman -S base-devel
     pacman -S mingw32/mingw-w64-i686-libjpeg-turbo
     pacman -S mingw32/mingw-w64-i686-icu
     pacman -S mingw32/mingw-w64-i686-libpng
     pacman -S mingw32/mingw-w64-i686-sqlite3
```

Run cmake and build QtWebKit
```
mkdir build
cd build
CMAKE_PREFIX_PATH=/c/Qt/5.7/mingw53_32 CC=i686-w64-mingw32-gcc CXX=i686-w64-mingw32-g++ cmake /e/WebKit-new-qt-stable/ -G Ninja -DPORT=Qt -DCMAKE_PREFIX_PATH="/c/msys64/mingw32"
ninja
```