### What?

JHBuild is a tool for automated build of package collections. It is extensively used by GNOME project, though there are some other prominent users. In WebKit it is used by GTK and EFL ports for a long time.

### Why?

To maintain stable layout test results we need to avoid changes in libraries like freetype, fontconfig, harfbuzz. Previously common practice was to use fixed Linux distro (e.g. Ubuntu 12.04) and install all dependencies of Qt and QtWebKit from packages (possibly with help of metapackage [1]). This approach has following downsides:

* It effectively prevents this system from being up-to-date and secure. Even if you pin some packages and update others, pinned packages may have security updates affecting other parts of the system (e.g. UI of build slave)
* Upgrade from one distro version to another is likely to cause massive baseline changes, because all packages are upgraded at once (with jhbuild you can upgrade only one package and only when you really need it)
* Contributors have to use VM image like [2] to be able to pass layout tests. With jhbuild it should be possible to get reproducible results on any distro (unless module set is incomplete).

JHBuild is not the unique solution to solve this problem, many similar systems exist, but it has already been integrated into WebKit tooling, and all modules except `qt` are reused from other ports.

### Commands [3]

* Build everything from scratch

`Tools/Scripts/update-qtwebkit-libs`

* Build after change in module set or configuration without starting from scratch

`JHBUILD_WIPE_ON_CHANGE=0 Tools/Scripts/update-qtwebkit-libs`

* (Almost) direct use of `jhbuild`:

```
Tools/jhbuild/jhbuild-wrapper --qt <commands>
Tools/jhbuild/jhbuild-wrapper --qt info <module_name>
Tools/jhbuild/jhbuild-wrapper --qt build <module_name>
Tools/jhbuild/jhbuild-wrapper --qt uninstall <module_name>
# Force rebuild of module without rebuilding dependencies
Tools/jhbuild/jhbuild-wrapper --qt buildone -f <module_name>
# List all modules
Tools/jhbuild/jhbuild-wrapper --qt list

```

### Qt debug info

    find WebKitBuild/DependenciesQT/Build/ -name '*debug' -exec cp {} WebKitBuild/DependenciesQT/Root/lib \;

### Troubleshoout

#### jhbuild dies without any visible explanation of error

Check if taball checksums are correct.

### References

[1] https://launchpad.net/~u-szeged/+archive/ubuntu/sedkit

[2] http://webkit.sed.hu/blog/20101028/qtwebkit-builder-and-tester-virtual-machine

[3] https://developer.gnome.org/jhbuild/stable/command-reference.html.en