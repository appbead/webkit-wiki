**Please write to webkit-qt@lists.webkit.org mailing list and join #qtwebkit on irc.freenode.net in case you are willing to help QtWebKit project!**

Here is a list of things that will greatly help QtWebKit project and will help you to learn more about it before diving deeper:

### Improve build system and scripts

You will need some experience with CMake and qmake build systems, knowledge of Perl and/or Python will help. No advanced C++ skills are needed to take these items.

* Improve Qt-specific parts of build system to follow best practices
* Make CMake's automoc work only over Qt-specific files
* Identify and port missing features of old qmake-based build system to CMake, e.g., -fdebug-types-section and force_static_libs_as_shared. Upstream changes which are not specific to Qt.
* Refactor CMake files to minimize amount of Qt-specific code (work with upstream)
* Analyze scripts which were used for QtWebkit testing in past, compare with what WebKit project uses today, restore/reimplement Qt-specific bits were appropriate

### Improve documentation

[Webkit Wiki](http://trac.webkit.org/wiki) contains lots of useful information, including old documentation of QtWebKit port. Unfortunately, not all of it is up to date.

* Find out what things are still up-to-date, add links to them, or copy valuable bits here.
* Fix outdated pages directly on WebKit Wiki (needs discussion)

### Spread the word

Try to find large open-source projects, development communities, commerical or non-commerical organizations which are using QtWebKit right now, and ask them if they are interested in this project and can help.

For example, PhantomJS team is already contributing to our project.

### Attract funding

If we have funding, on later stages of project (see [Roadmap]) we may consider hiring part-time (or full-time) developer(s) to speed up progress.

### Help to submit port-independent patches to upstream

QtWebKit branch maintained by Qt community has accumulated a number of local patches, some of them, like [this](https://codereview.qt-project.org/#/c/73757/), may fix bugs affecting other ports.

* Help us to identify such patches
* Check if respective bugs can be reproduced in upstream, using e.g. GTK+ port on Linux, or WinCairo on Windows. If so, contact patch authors and tell them to submit patches to webkit.org