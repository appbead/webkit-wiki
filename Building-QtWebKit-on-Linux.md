You need to install the next dependencies:

* Qt >= 5.4 (Core, Gui, Network, Sql, OpenGL, Test, Widgets, Positioning, Sensors)
* CMake >= 2.8.12
* ninja
* sqlite >= 3.6.16
* ICU >= 52.1
* ruby >= 1.9
* perl >= 5.10.0
* python 2.7.x
* bison >= 2.1
* flex >= 2.5.34
* gperf >= 3.0.1
* libxml2 >= 2.8.0 (2.6.x will probably work)
* libxslt >= 1.1.7
* libjpeg v8 or v9 (IJG) or libjpeg-turbo
* libpng
* zlib
* libhyphen
* glib >= 2.36 (gio, gobject)
* gstreamer >= 1.0.3 (app, pbutils, video, mpegts, tag, audio, fft); you also need GStreamer 1.0 plugins for codec support

Optional dependencies:
* fontconfig
* libwebp

> Q: Why do you have so many dependencies?

> A: See [[FAQ]]

For Ubuntu use the next command

    sudo apt-get install build-essential perl python ruby flex gperf bison cmake \
    ninja-build libfontconfig1-dev libicu-dev libsqlite3-dev zlib1g-dev libpng12-dev \
    libjpeg-dev libxslt1-dev libxml2-dev libhyphen-dev

I'm using the next command to build QtWebKit:

    WEBKIT_OUTPUTDIR=`pwd`/build/qt \
    Tools/Scripts/build-webkit --qt \
        --release \
        --cmakeargs="-DCMAKE_PREFIX_PATH=/opt/Qt5.4.0/5.4/gcc_64/"

If you wish to install it globally (usually on `/usr/local`), you may then run the following command:

    cd build/qt/Release && sudo ninja install

You can also build with cmake directly:

    mkdir build/qt/Release
    cd build/qt/Release
    cmake -DPORT=Qt -DCMAKE_BUILD_TYPE=Release -G 'CodeBlocks - Ninja'

To build only JSC, replace `build-webkit` with `build-jsc`

Use this command to run JSC tests:

    Tools/Scripts/run-layout-jsc -t LayoutTests/ -j build/qt-jsc/Release/bin/jsc -r results