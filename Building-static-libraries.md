You just point CMAKE_PREFIX_PATH to Qt installation which is static, and it automatically switches to static mode

On systems with GNU ld (default on Linux, also used by MinGW) you also need to set -DUSE_THIN_ARCHIVES=OFF

If you get errors, look at bug #454, maybe you hit the same issue