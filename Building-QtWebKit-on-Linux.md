You need to install the next dependencies:

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

For Ubuntu use the next command

    sudo apt-get install build-essential perl python ruby-dev flex gperf bison cmake ninja \
    libfontconfig1-dev libicu-dev libsqlite3-dev zlib1g-dev libpng12-dev libjpeg-dev libxslt1-dev libxml2-dev 

I'm using the next command to build QtWebKit:

    WEBKIT_OUTPUTDIR=`pwd`/build/qt \
    Tools/Scripts/build-webkit --qt \
        --release \
        --cmakeargs="-DCMAKE_PREFIX_PATH=/opt/Qt5.4.0/5.4/gcc_64/"

To build only JSC, replace `build-webkit` with `build-jsc`

Use this command to run JSC tests:

    Tools/Scripts/run-layout-jsc -t LayoutTests/ -j build/qt-jsc/Release/bin/jsc -r results