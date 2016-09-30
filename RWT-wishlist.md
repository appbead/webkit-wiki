* Running layout tests on device which does NOT have python, git, full-featured shell, storage space. Connection with SSH, NFS can be used to get test sources and write results. Should be implemented as a driver similar to Xvfb one.

* In pixel mode when text-only failure occurs, but image comparison succeeds, save images anyway. Otherwise it's hard to distinguish failing text-only tests from this category (rebaseline-server support may be needed!)
* When running `--compare-port=` there should be an easy way to copy & git add matching results to LayoutTests/platform/qt (like rebaseline-server does for tests from queue)
* Parsing of large TestExpectations file takes too long (https://github.com/annulen/webkit/issues/283)
* I suspect run-webkit-tests could be made faster
   * Reduce CPU consumption by python in test run
   * It may be possible to reduce disk I/O by getting test lists from git, maybe even file contents. I observed such effect in a different project, just listing files from large dir hierarchy takes a lot of time with cold cache and uses a lot of system calls, while using mlocate database is ~100x faster. git has similar property - it stores objects in flat dir (e.g. see explanation why `git grep` is faster than `grep`). If git is not fast enough we can switch to mlocate.
   * It may be beneficial to run tests with `offscreen` QPA plugin instead of `xvfb-run`, however not all tests can succeed in this mode. At very least, OpenGL won't work (we don't run WebGL tests now), I also suspect drag&drop and maybe other test kinds can fail. We may need hybrid driver which doesn't use Xvfb for test that can be run without it. andersca and litherum may have additional info

```
<annulen>	andersca_: what was the reson for this change: https://bugs.webkit.org/show_bug.cgi?id=148746 ?
<annulen>	*reason
<andersca_>	annulen: it's the first step of a patch i never finished
<andersca_>	annulen: where you can specify set-up data inside a test fiel
<andersca_>	annulen: we already support it for WKTR
<annulen>	andersca_: where can I see an example of such set-up data?
<andersca_>	annulen: hmm, myles would know
<annulen>	litherum: ^
```

* Detect expectation files in `LayoutTests/platform/qt` left over from tests which no longer exist. See also https://github.com/annulen/webkit/issues/214
* Better detection of "accidental" failures. Often RWT execution results in a few unexpected failures and/or flakes, which are gone if just these tests are executed. Talk to other WebKit people how do they mitigate it, maybe problem is specific to Qt (e.g. we have tests that disrupt execution of others).
* Related: detection of tests that break execution of following tests.
* Compare selected tests with WebKit in another dir - find regressions after previous snapshot, after WebKit upgrade, compare behavior with other ports
* Compare TestExpectation files with legacy QtWebKit reusing webkitpy machinery. Find regressions, find issues which had meaningful comments and/or associated bug reports in old expectations