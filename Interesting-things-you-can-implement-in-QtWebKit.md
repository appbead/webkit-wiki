Please contact us if you are interested in following stuff. Implementation of these items is not in our schedule yet, but we are ready to guide you in case you want to join in.

### Import QObject-derived classes as ES2015 classes

Curently it is possible to inject any QObject QWebFrame::addToJavaScriptWindowObject(), however now ES2015 has native suppoty for classes. It would be cool if you could create instances of QObject-derived class in JavaScript, or even inherit from them.

### Full-fledged C++ API for WebKit2, including WebProcess side

* Integrate WK2 view into widget, just like it is done for QtWebEngine
* Allow injection of user plugin into WebProcess, similar to WebExtensions in WebKitGTK. Code of this plugin will have API to access DOM (maybe even the same QWebElement and friends), and use Qt Bridge. Communication between plugin and UI process will use the same IPC code as WebKit2 internals.