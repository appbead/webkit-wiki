```
WEBKIT_OUTPUTDIR=$(pwd)/build/qt-clang \
Tools/Scripts/run-webkit-tests --qt --no-build --no-show-results -1
```

Here:
* `WEBKIT_OUTPUTDIR` - same as when you are building QtWebKit, not needed if default (`WebKitBuild`) is used
* `--no-show-results` - Avoid if you want to see results as HTML in a browser
* `-1` - Test WebKit 1, not WebKit 2

Additional options:
* `--debug` - Test Debug build instead of Release
* `--debug-rwt-logging` - Debug testing machinery
* `--pixel` - Enable pixel tests

After argument list you can pass directory to run tests in (for example, `fast`), or individual test file

#### More info
* http://trac.webkit.org/wiki/QtWebKitContrib#Runningthetests
* http://trac.webkit.org/wiki/WebKitGtkLayoutTests
