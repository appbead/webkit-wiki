You might be wondering why so many projects (including this one) are calling themselves "WebKit" and how they relate to each other. Let's try to clarify it.

### WebKit

Actually, there is only one project called "WebKit", and its headquarters are at https://webkit.org/. All other related projects are either "ports" or forks of WebKit. Ports can be defined as a collections of code added to shared WebKit source tree, implementing platform-dependent functionality using APIs provided by particular platform (e.g., Qt libraries in QtWebKit, Cocoa and CoreFoundation in Mac and iOS).

* Official ports: Mac (OS X), iOS, GTK+, EFL, AppleWin, WinCairo
* Downstream ports (examples): EAWebKit, Haiku, QtWebKit
* Forks: Blink (derived from previously existing Chromium port)

### QtWebKit

QtWebKit was an official port of WebKit until October of 2013, when Qt Project made a decision to focus on Chromium-based QtWebEngine project. After that change, QtWebKit code was removed from WebKit trunk.

However, development of QtWebKit was continued in a branch, maintained by Qt Project (http://code.qt.io/cgit/qt/qtwebkit.git/). This branch was forked from WebKit trunk in mid-2013 and contains fixes and new features in Qt-specific code, as well as many upstream patches cherry-picked from trunk. It also includes patches removing use of C++11 features, allowing to build QtWebKit on all platforms supported by Qt Project.

This branch was released as a part of Qt 5.2 - 5.5 (QtWebKit module). It will also be (unofficially) released as a part of Qt 5.6 (though QtWebKit has status "Removed" in 5.6)

### This repository

Code in this repository is based on current WebKit trunk, but patches that removed Qt port in 2013 are being reverted. It is not directly derived from Qt Project branch described in paragraph above, however goal is to incorporate all improvements made there. It is a downstream port of WebKit, however we are trying to get our changes into upstream wherever it makes sense and aligns with goals of WebKit project.