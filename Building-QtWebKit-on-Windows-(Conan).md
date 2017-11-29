This approach is used currently in CI system for building release binaries.

### Preparation

There is no need to repeat this steps for each build, just do it when you build first time

* Install C++ compiler - this manual works only for **Visual Studio 2015 or 2017** or **MinGW version shipped with Qt SDK**. Using other versions of MinGW is possible but some adjustments to steps below will be needed (feel free to ask if you really need this). As for Visual Studio, **older versions just won't work**
* Install Perl >= 5.14 (e.g. ActivePerl or StrawberryPerl)
* Install Python 2.7 and Ruby >= 1.9
* Install Conan (see https://www.conan.io/downloads)
* Run `conan remote add qtproject https://api.bintray.com/conan/qtproject/conan`
* Clone git repositories:
```
git clone git://code.qt.io/qt/qt5.git
cd qt5
git checkout 5.9
perl init-repository --module-subset=qtbase,qtdeclarative
git clone git://code.qt.io/qt/qtwebkit.git
```
* Install Qt 5.9 binaries from http://download.qt.io/archive/qt/5.9

If you want to use different version of Qt, replace 5.9 in checkout command and in your download URL with required version.

You may also want to build Qt from git sources that you've just downloaded, in this case you may need to add more modules to `--module-subset`. Full configuration requires `qtlocation`, `qtsensors`, `qtwebchannel`, and in case of MinGW also `qtmultimedia`.