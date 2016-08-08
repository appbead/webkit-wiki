```
Tools/Scripts/run-webkit-tests --qt -1 --no-new-test-results --child-processes=4 \
    -p --debug canvas compositing fast js
```
Here:
* `-1` - Test WebKit 1, not WebKit 2
* `-p` - Enable pixel tests
* `--child-processes=4` - Run 4 tests in parallel
* `--no-new-test-results` - Don't create expectations when they are missing
* `--debug` - Use Debug build instead of Release
* `canvas compositing fast js` - run test from these directories only

```
WEBKIT_OUTPUTDIR=$(pwd)/build/qt-clang \
Tools/Scripts/run-webkit-tests \
--qt -1 --no-show-results --no-new-test-results --no-retry-failures
```
Here:
* `WEBKIT_OUTPUTDIR` - same as when you are building QtWebKit, not needed if default (`WebKitBuild`) is used
* `--no-show-results` - Avoid if you want to see results as HTML in a browser
* `--no-retry-failures` - Don't run failed tests once again

Additional options:
* `--debug` - Test Debug build instead of Release
* `--debug-rwt-logging` - Debug testing machinery
* `--results-directory=` - Set different output dir (by default `WEBKIT_OUTPUTDIR/layout-test-results` is used)
* `--compare-port=mac-yosemite` - Use expectations from different port (useful for tests with missing results)

Add new expectations
* `--new-baseline`

After argument list you can pass directory to run tests in (for example, `fast`), or individual test file

Results are produced in `$WEBKIT_OUTPUTDIR/Release/layout-test-results` (or `Debug`)

```
Tools/Scripts/run-webkit-tests --qt -1 --no-new-test-results --child-processes=4 -p --no-ref-tests --no-retry-failures fast
```

### WARNING
run-webkit-tests does not keep unknown environment variables, e.g. `JSC_useJIT=0` is discarded. You need to run DRT manually.

### Why DRT and QtTestBrowser may have different rendering?

* Fonts: `-use-test-fonts` option of QtTestBrowser to the rescue
* Additional objects in JS runtime, for example `window.testRunner`, `window.eventSender`, `window.textInputController`

### Running manually

```
WebKitBuild/Release/bin/DumpRenderTree -v LayoutTests/fast/shrink-wrap/rect-shrink-wrap.html

# GTK
TEST_RUNNER_TEST_PLUGIN_PATH= TEST_RUNNER_INJECTED_BUNDLE_FILENAME=WebKitBuild/Release/lib/libTestRunnerInjectedBundle.so WebKitBuild/Release/bin/WebKitTestRunner -v -p LayoutTests/fast/shrink-wrap/rect-shrink-wrap.html
```

#### More info
* http://trac.webkit.org/wiki/QtWebKitContrib#Runningthetests
* http://trac.webkit.org/wiki/WebKitGtkLayoutTests
* http://trac.webkit.org/wiki/TestExpectations
* http://trac.webkit.org/wiki/NewRunWebKitTests
