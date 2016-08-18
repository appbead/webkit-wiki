This is a work in progress; see https://trac.webkit.org/wiki/WebKitGTK/Releasing for example of good document

### Make tarball

```
Tools/gtk/make-dist.py -t qtwebkit -p Qt --version tp3 -c Tools/qt/manifest.txt
```

* `-t` sets base name of tarball
* `-c` option unpacks generated `.tar` file and builds it
* You may need to set environment variables when running `make-dist.py`, if default build options are not suitable, e.g.
```
CMAKE_PREFIX_PATH=/opt/Qt5.4.0/5.4/gcc_64 CC=/usr/bin/clang CXX=/usr/lib/ccache/clang++ Tools/gtk/make-dist.py ...
```
