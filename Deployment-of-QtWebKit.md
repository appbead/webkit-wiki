### Dependencies of QtWebKit library
* Qt libraries (see https://doc.qt.io/qt-5.10/deployment.html for details how to deploy Qt)
    * QtCore
    * QtGui
    * QtNetwork (note that you need to ship OpenSSL to get HTTPS working!)
    * QtQml
    * QtQuick
    * QtWebChannel
    * QtOpenGL
    * QtPositioning
    * QtSensors
* ICU libraries
    * Windows: copy ICU dll's bundled with QtWebKit package
    * macOS: system ICU libraries are used, but it's possible to build with custom ICU, which may be useful e.g. for AppStore distribution
    * Linux: ICU libraries are required for QtCore, so they should already be deployed
* libxml2 and libxslt
    * Windows: copy dll's bundled with QtWebKit package
    * macOS, Linux: system libraries are used

### For Widgets API (QWebView, QGraphicsWebView, or headless QWebPage)

* Deploy QtWebKit library and its dependencies, listed above
* Deploy QtWidgets and QtWebKitWidgets libraries

### For QML API (WebKit2)

* Deploy binaries of QtWebProcess, QtWebNetworkProcess. QtWebDatabaseProcess
* Deploy QtWebPluginProcess if you need to support NPAPI plugins
* Deploy QML imports

