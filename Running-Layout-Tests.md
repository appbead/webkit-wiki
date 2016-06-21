```
WEBKIT_OUTPUTDIR=$(pwd)/build/qt-clang \
Tools/Scripts/run-webkit-tests --qt --no-build -1 --no-show-results --no-new-test-results
```

Here:
* `WEBKIT_OUTPUTDIR` - same as when you are building QtWebKit, not needed if default (`WebKitBuild`) is used
* `-1` - Test WebKit 1, not WebKit 2
* `--no-show-results` - Avoid if you want to see results as HTML in a browser
* `--no-new-test-results` - 

Additional options:
* `-p` - Enable pixel tests
* `--debug` - Test Debug build instead of Release
* `--child-processes=4` - Run 4 tests in parallel
* `--debug-rwt-logging` - Debug testing machinery

After argument list you can pass directory to run tests in (for example, `fast`), or individual test file

Results are produced in `$WEBKIT_OUTPUTDIR/Release/layout-test-results` (or `Debug`)

#### More info
* http://trac.webkit.org/wiki/QtWebKitContrib#Runningthetests
* http://trac.webkit.org/wiki/WebKitGtkLayoutTests
* http://trac.webkit.org/wiki/TestExpectations
* http://trac.webkit.org/wiki/NewRunWebKitTests
