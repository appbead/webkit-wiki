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

# Snapshots

Snapshots are prepared with `Tools/qt/make-snapshot.pl` script. Run it in target repository being working directory, e.g.:

    ../WebKit/Tools/qt/make-snapshot.pl

where `../WebKit` is path to original non-stripped repo.

### About manifest file

Manifest file controls what files from git repository end up in release tarball (as well as snapshots repositories here on Gihub and at code.qt.io). While simply skipping LayoutTests cuts off most of bloat, approach taken by WebKitGTK port with make-dist.py script allows to reduce size much further, and also get rid of files with dubious license.

You can see current manifest at https://github.com/annulen/webkit/blob/qtwebkit-stable/Tools/qt/manifest.txt, it is loosely based on manifest of GTK port.