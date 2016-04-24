### Use case 1: Embedded systems
* WebKit engine tends to use less memory than Chromium because of different design decisions.
* QtWebKit is using Qt to render web content, so if Qt is ported to some platform, it can use browser immediately. Chromium uses different graphics system (Skia) which may require additional porting efforts.
* QtWebKit has smaller binary size, because it shares a lot of code with Qt.
* WebKit engine allows flexible customization of feature set, which allows to shrink binaries further by omitting useless code.
* WebKit engine often supports different variants of platform integration code, which are used by different ports, allowing to write integration code for custom platforms without much hassle (e.g., custom MediaPlayer backends).
* QtWebEngine is licensed under LPGLv3 which prohibits its use in locked-down devices.

### Use case 2: Linux desktop
* QtWebKit (especially WebKit1 version, i.e. QWebView and friends) is highly customizable on Qt level. This feature makes projects like KDEWebKit possible.
* Some users are not satisfied by ever growing CPU and memory usage of modern browsers, and are even ready to sacrifice some milliseconds of page loading time for lower resource usage. Industry tends to ignore them.
* It would be better to have a choice of browsers based on different engines on Linux, not just a choice of Chromium skins.

### Use case 3: Web page processing tools
* WebKit1 API of QtWebKit provides direct R/W access to DOM from C++ code, allowing to write high-performance tools. 
* It also provides facilities for off-screen rendering, which is used by projects like PhantomJS

### Use case 4: Legacy applications
* There is a lot of code written with use of QtWebKit API. However, QtWebKit branch currently maintained by Qt Project cannot receive security updates anymore, because it lags too far behind WebKit upstream.