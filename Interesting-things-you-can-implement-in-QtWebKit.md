Please contact us if you are interested in following stuff. Implementation of these items is not in our schedule yet, but we are ready to guide you in case you want to join in.

### Import QObject-derived classes as ES2015 classes

Curently it is possible to inject any QObject QWebFrame::addToJavaScriptWindowObject(), however now ES2015 has native support for classes. It would be cool if you could create instances of QObject-derived class in JavaScript, or even inherit from them.

### Full-fledged C++ API for WebKit2, including WebProcess side

* Integrate WK2 view into widget, just like it is done for QtWebEngine
* Allow injection of user plugin into WebProcess, similar to WebExtensions in WebKitGTK. Code of this plugin will have API to access DOM (maybe even the same QWebElement and friends), and use Qt Bridge. Communication between plugin and UI process will use the same IPC code as WebKit2 internals.

### Full-fledged DOM bindings, similar to GObject bindings of GTK port

QWebElement API and Qt bridge allow to get/set any property of DOM element, and call any JS methods of element. However, it can only be done with evaluateJavaScript, which means JS engine is always involved, and to pass arguments you may need to use string operations.

Alternative is to generate QWebElement-derived classes for each kind of element. This classes can have appropriate Qt propertes, slots, and signal (for events). User will be able to use them via signal-slot connections, or downcast QWebElement to appropriate element class and use it's API from C++ in a strongly-typed manner, or inherit from element class and create customized element, in the spirit of WebComponents [1]

See also http://trac.webkit.org/wiki/QtWebKitTodo#DeferredDOMAPIItems

[1] http://w3c.github.io/webcomponents/spec/custom/