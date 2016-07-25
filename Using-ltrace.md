If your system is supported by `ltrace` (e.g., Linux), use it to get quick understanding of what WebKit code is executed when processing particular test case. It may be more productive than setting random prints or breakpoints if you don't know where to start.

```
ltrace -C -e '*WebCore*@libQt5WebKit.so*' -o bad.log \
    WebKitBuild/Release/bin/QtTestBrowser -use-test-fonts \
    LayoutTests/fast/css/pseudo-first-line-border-width.html
```

* `-C` - demangle C++ symbols
* `@libQt5WebKit.so*` - trace calls only in `libQt5WebKit.so` library
* `*WebCore*` - filter out symbols that are not from `WebCore`
* `-o bad.log` - save all output to file for further analysis with `grep` :)

BTW, don't forget that `strace` utility (or similar, like `sysdig`, `dtruss`) is useful if you are interested in syscalls.