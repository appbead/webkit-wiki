You just point CMAKE_PREFIX_PATH to Qt installation which is static, and it automatically switches to static mode

* Building QML API is not supported, you should pass -DENABLE_WEBKIT2=OFF to cmake [1].
* On systems with GNU ld (default on Linux, also used by MinGW) you also need to set `-DUSE_THIN_ARCHIVES=OFF`.
* On Windows (if you need static runtime) you need to set `-DUSE_STATIC_RUNTIME=ON` (msvc only).

If you get errors, look at bug #454, maybe you hit the same issue

Note that linking executable with static QtWebKit may require explicit linking of some libraries which Qt or QtWebKit depend upon.

### Configuration of static Qt build

Qt can be built with bundled libraries: libpng, zlib, libjpeg, sqlite. These libraries are used by QtWebKit independently, and may cause conflicts in case of version mismatch. Therefore, it's recommended to configure Qt to use system version of these libraries, or disable those that can be disabled.

### See also

https://github.com/ariya/phantomjs/issues/15018

### Notes

[1] Reason 1: WebKit 2 builds several executables for running background processes, and all of them have to link with the same set of libraries. With static libraries it implies linking all WebKit code into all executables, which multiplies binary size 3-5 times.

Reason 2: QML in general is not advertizing support for static builds, it's tricky to get it right.

If you are adventurous enough and have been able to get along with QML in static builds, feel free to provide patch implementing background processes as multi-call binary (i.e. one binary, `main()` selects what to run based on executable name) and resolving all related build system issues.