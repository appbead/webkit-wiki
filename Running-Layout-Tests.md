# Preparations

- Run the `Tools/Scripts/update-qtwebkit-libs` script (see [JHBuild](https://github.com/annulen/webkit/wiki/JHBuild)) to build all dependencies inside the source tree, in order to get reproducible test results.
- Run `find WebKitBuild/DependenciesQT/Source/ -name '*.debug' -exec cp {} WebKitBuild/DependenciesQT/Root/lib \;` (workaround for bug #402)
- (Re)build QtWebKit with the above content in place using `Tools/Scripts/build-webkit`
- Clone the [qtwebkit-testfonts](https://github.com/annulen/webkit-test-fonts.git) repo and export the `WEBKIT_TESTFONTS` variable to point to it.

# Running tests

Normally you should use one of the following commands:
```
# Add --no-show-results when running over SSH!

# Run all tests with Release build
Tools/Scripts/run-webkit-tests --qt -1 --no-new-test-results --child-processes=4 -p

# Run a few (e.g. failed) tests with Release build
Tools/Scripts/run-webkit-tests --qt -1 --no-new-test-results --child-processes=4 -p \
    --results-directory=./tmp test1 test2 ...

# Run all tests with Debug build
Tools/Scripts/run-webkit-tests --qt -1 --no-new-test-results --child-processes=4 -p \
    --debug
```

# Core dumps

- run this command as super-user: 
```
$ su
# echo "$(pwd)/coredumps/core-pid_%p-_-process_%e" > /proc/sys/kernel/core_pattern
# ^D
```
- enable core dumps: 
```
$ ulimit -c unlimited
```
- create dir and set the WEBKIT_CORE_DUMPS_DIRECTORY environment variable: 
```
$ mkdir -p $(pwd)/coredumps
$ export WEBKIT_CORE_DUMPS_DIRECTORY=$(pwd)/coredumps
```

**WARNING**: results page suggests to use `%E` instead of `%e`, but actually script looks for name without path. Problem is that `%e` will use thread name if it is set, instead of executable name.

* When done with core dumps, prevent their creation to avoid disk filling
```
$ ulimit -c 0
```

# Rebasing test expectations

When new test failure occurs, it may be caused by different reasons:
* Bug was introduced by recent change (aka "regression")
* Bug was fixed by recent change, and new results are closer to current standards ("progression")
* Dependency of WebKit or testing infrastructure (e.g., Apache) was updated, causing test output change which is not better or worse than before

When change is not caused by regression, we should update expected results to make test pass again. Visual way to do this is to use `rebaseline-server`:

    Tools/Scripts/webkit-patch rebaseline-server WebKitBuild/Release/layout-test-results

To open rebaseline-server UI in QtWebKit, use

    Tools/Scripts/run-minibrowser --qt http://localhost:8127/

### Other possible invocations with description of options

```
Tools/Scripts/run-webkit-tests --qt -1 --no-new-test-results --child-processes=4 \
    -p --debug canvas compositing fast js
```
Here:
* `-1` - Test WebKit 1, not WebKit 2
* `-p` - Enable pixel tests
* `--child-processes=4` - Run 4 tests in parallel. In most cases you want to make it equal or less than CPU cores number (otherwise tests can start timing out because of CPU drain). However, when dealing with test sets with lots of timeout it makes sense to increase number of processes to make more DRTs waiting for nothing in parallel.
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
* `--exit-after-n-crashes-or-timeouts=N`
* `--no-ref-tests` - Use when you are doing rebaseline, which is not applicable to ref-tests
* `--skip-failing-tests`
* `--force` - Run tests as all of them are expected to pass

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

# Running JSC tests

```Tools/Scripts/run-javascriptcore-tests --qt --root=WebKitBuild/Release --no-build```

### Windows
* Add `perl` before the script name
* Add 'c:\msys64\usr\bin` to `PATH` (for `make` and `sh`)

### run-layout-jsc

Following command runs only a small subset of tests, but quite representative. Can run on device in busybox shell, no other dependencies:

```Tools/Scripts/run-layout-jsc -t LayoutTests/ -j build/qt-jsc/Release/bin/jsc -r results```

#### More info
* http://trac.webkit.org/wiki/QtWebKitContrib#Runningthetests
* http://trac.webkit.org/wiki/WebKitGtkLayoutTests
* http://trac.webkit.org/wiki/TestExpectations
* http://trac.webkit.org/wiki/NewRunWebKitTests
