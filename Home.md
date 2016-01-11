# QtWebKit Reloaded

This is a project aiming to upgrade QtWebKit to modern WebKit code base.

## Why?

If you wonder why do we need QtWebKit when shiny new QtWebEngine is available, please look at our [[use cases list|Use cases of QtWebKit]]

## Interested and ready to help?

Here is our list of [[open projects|Open Projects]].

Master contains exact mirror of upstream WebKit repository at git://git.webkit.org/WebKit.git. Things not directly related to Qt port, like MIPS support, are developed against master, and go through code review on webkit.org.

Development of QtWebKit currently happens in qtwebkit-1 branch. Warning: it can be rebased to master at any time, so please be careful.

## System requirements

The next configurations are going to be supported:

* OS: Linux (X11 and EGLFS)
* CPU architectures: x86_64, MIPS
* Compiler: g++ >= 4.8
* Qt >= 5.4 (right now 5.2 will probably be enough)

## Build requirements

* sqlite >= 3.6.16
* ICU >= 52.1
* ruby >= 1.9
* perl
* python 2
* bison
* flex
* gperf

I'm using the next command to build QtWebKit:

    WEBKIT_OUTPUTDIR=`pwd`/build/qt-jsc \
    Tools/Scripts/build-jsc --qt --no-ftl-jit \
        --release \
        --cmakeargs="-DCMAKE_PREFIX_PATH=/opt/Qt5.4.0/5.4/gcc_64/"

and this command to run tests:

    Tools/Scripts/run-layout-jsc -t LayoutTests/ -j build/qt-jsc/Release/bin/jsc -r results

## Contacts
Mailing list: webkit-qt@lists.webkit.org

IRC: #qtwebkit on irc.freenode.net
