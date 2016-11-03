### Why CMake?

Previously almost every WebKit port was using its own build system, and Qt port was using qmake. However, in recent years WebKit project is switching to CMake-based build system, which is shared between all ports. EFL, GTK, AppleWin and WinCairo are already using it, AppleMac supports it as experminental option. The only remaining upstream port not using CMake is iOS.

So, using CMake gives us 2 benifits:
* Avoid extra work needed to update qmake-based build system to current state of the art (especially parts dealing with custom code generators), and then maintain it.
* Be a part of WebKit community, contributing improvements to shared build system which could be used (and further improved!) by developers of other ports.

### Why C++11? / Why GCC 4.8 is required, I'm still using older cross-toolchain!

WebKit project started using C++11 since 2012, and was gradually extending its use since then. Version of WebKit shipped with Qt 5.2 and later (based on WebKit from mid-2013) was intentionally de-C++11-ized to support all compilers supported by Qt.

However, several years have passsed and now WebKit makes thorough use of most of C++11 features, so it is no longer feasible to convert all this code to C++98.

As for GCC 4.8 requirement, this is the first GCC release which supports complete feature list of C++11. If you are required to use older version, e.g. GCC 4.7, you may try it and share your results. Note that with GCC older than 4.7 your chances are much lower.

### Why so many dependencies besides Qt?

* **libpng** and **libjpeg** are optional dependencies in QtWebKit 5.6, but now are promoted to be mandatory. They are needed to build Qt anyway (though their sources are bundled with Qt), and having single code path for PNG and JPEG will allow to have same rendering and performance characteristics independently on how QtWebKit is built.
* **sqlite** - similar to libraries above, QtWebKit 5.6 can use sqlite sources from Qt installation, but we don't provide this feature
* **libxml2** and **libxslt** - similar to libraries above, but avoiding them required maintainance of spearate parser code for XML and XSLT. This opens a way to additional bugs, performance issues, and security issues (because it is web-facing code)
* **libhyphen** implements feature which is missing in QtWebKit 5.6 (CSS Hyphenation), it can be disaled using -DUSE_LIBHYPHEN=OFF cmake option)
* **ICU** was a requirement since Qt 5.0. [1]

### Why do I have to disable feature X explicitly if library Y was not found? It was disabled automagically with qmake!

There is some difference in how new build system deals with features: in new build system there is default full-featured configuration and nothing is silently skipped when dependency is missing. You have to disable features deliberately because:
* This way you understand what features do you disable
* Build result does not depend on system configuration, so we can say that QtWebKit supports X on your OS (unless you deliberately disabled it)
* No distributor can produce crippled packages missing some features by simply forgetting to add necessary dependencies

[1] An unofficial way to build QtWebKit 5.x without ICU exists, but using it leads to degradation of Unicode support on all platforms (except possibly WinCE). Related code was removed from WebKit upstream, and we see no sense in restoring it.