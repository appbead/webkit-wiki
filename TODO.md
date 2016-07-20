* Start using static analyzers: scan-build, clang-tidy. For Qt-specific issues: Clazy, Krazy2(?)

* Find out if we still need TextureMapperImageBuffer (non-GL code path)

    It was broken (see https://bugs.webkit.org/show_bug.cgi?id=143214#c20) and was removed in cd4e4ff

* Review Qt timer usage

    Qt 5 introduced 3 types of timers: Qt::PreciseTimer, Qt::CoarseTimer, and Qt::VeryCoarseTimer. By default, CoarseTimer is used. We need to verify if it is the most appropriate timer type in all places where Qt timers are used, fix otherwise.

### WK2

Wk2 should not be tied to QML, e.g. `QQuickNetworkReply` class

### OpenGL / WK2

* Check OpenGL function lookup code

    https://bugs.webkit.org/show_bug.cgi?id=127299 removes code which was used by Qt with QT_OPENGL_ES_2 defined

* Find out how GLX surfaces work in trunk

    Qt port had integration into GraphicsSurfaceGLX.cpp, but it was removed in r171672. EFL refactored GLX support in r146458 so it is still supported, just in a different way.


### Defines we might want to enable

OPENTYPE_VERTICAL, OPENTYPE_MATH

ENABLE_CSS3_TEXT_DECORATION_SKIP_INK
