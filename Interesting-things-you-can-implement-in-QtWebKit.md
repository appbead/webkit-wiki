Please contact us if you are interested in following stuff. Implementation of these items is not in our schedule yet, but we are ready to guide you in case you want to join in.

### Built-in PDF viewer via QtPDF module (under run time and build time options)

https://github.com/annulen/webkit/issues/232

* QtPDF is based on PDFium, but renders things with QPainter instead of Skia.
* It might be possible to support JS in PDF with JSC engine, replacing JS_Runtime_Stub. Needs work on QtPDF side to allow plugin-like loading of JS bridge implementation

### Revive Android support

**UPD** https://github.com/daewoong-jang/webkit-android - up-to-date Android port of WebKit with WK2 upport

Legacy QtWebKit was known to compile for Android (though port was never supported officially). See patches
* https://codereview.qt-project.org/#/c/68640/
* https://codereview.qt-project.org/#/c/71548/
* https://codereview.qt-project.org/#/c/88045
* https://codereview.qt-project.org/#/c/95969/
* https://codereview.qt-project.org/#/c/97993/

See also https://github.com/ericwlange/webkit - newer port of JavaScriptCore to Android.

### Full-fledged C++ API for WebKit2, including WebProcess side

* Integrate WK2 view into widget, just like it is done for QtWebEngine
* Allow injection of user plugin into WebProcess, similar to WebExtensions in WebKitGTK. Code of this plugin will have API to access DOM (maybe even the same QWebElement and friends), and use Qt Bridge. Communication between plugin and UI process will use the same IPC code as WebKit2 internals.

### Full-fledged DOM bindings, similar to GObject bindings of GTK port

QWebElement API and Qt bridge allow to get/set any property of DOM element, and call any JS methods of element. However, it can only be done with evaluateJavaScript, which means JS engine is always involved, and to pass arguments you may need to use string operations.

Alternative is to generate QWebElement-derived classes for each kind of element. This classes can have appropriate Qt propertes, slots, and signal (for events). User will be able to use them via signal-slot connections, or downcast QWebElement to appropriate element class and use it's API from C++ in a strongly-typed manner, or inherit from element class and create customized element, in the spirit of WebComponents [1]

See also http://trac.webkit.org/wiki/QtWebKitTodo#DeferredDOMAPIItems

### QtScript-like API for use of JavaScriptCore without QWebFrame

QtScript module is based on older JavaScriptCore version, and lots of things are similar between QtScript and QtWebKit Bridge. It should not be hard to provide API for JSC+bridge so that it is possible to avoid overhead of full DOM environment. Also it would be possible to run scripts in non-GUI thread while GUI thread continues to use QtWebKit's WK1 API (note that JSC is thread-safe, while WebCore isn't).

There is no goal to provide separate library that does not include WebCore, having it linked to QtWebKit library or part of it is quite acceptable.