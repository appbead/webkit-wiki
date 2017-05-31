You just point CMAKE_PREFIX_PATH to Qt installation which is static, and it automatically switches to static mode

On systems with GNU ld (default on Linux, also used by MinGW) you also need to set -DUSE_THIN_ARCHIVES=OFF

If you get errors, look at bug #454, maybe you hit the same issue

### Configuration of static Qt build

Qt can be built with bundled libraries: libpng, zlib, libjpeg, sqlite. These libraries are used by QtWebKit independently, and may cause conflicts in case of version mismatch. Therefore, it's recommended to configure Qt to use system version of these libraries, or don't use them at all.