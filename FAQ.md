### Why CMake?

Previously almost every WebKit port was using its own build system, and Qt port was using qmake. However, in recent years WebKit project is switching to CMake-based build system, which is shared between all ports. EFL, GTK, AppleWin and WinCairo are already using it, AppleMac supports it as experminental option. The only remaining upstream port not using CMake is iOS.

So, using CMake gives us 2 benifits:
* Avoid extra work needed to update qmake-based build system to current state of the art (especially parts dealing with custom code generators), and then maintain it.
* Be a part of WebKit community, contributing improvements to shared build system which could be used (and further improved!) by developers of other ports.

### Why C++11? / Why GCC 4.8 is required, I'm still using older cross-toolchain!

WebKit project started using C++11 since 2012, and was gradually extending its use since then. Version of WebKit shipped with Qt 5.2 and later (based on WebKit from mid-2013) was intentionally de-C++11-ized to support all compilers supported by Qt.

However, several years have passsed and now WebKit makes thorough use of most of C++11 features, so it is no longer feasible to convert all this code to C++98.

As for GCC 4.8 requirement, this is the first GCC release which supports complete feature list of C++11. If you are required to use older version, e.g. GCC 4.7, you may try it and share your results. Note that with GCC older than 4.7 your chances are much lower.