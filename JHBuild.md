### Commands

* Building everything from scratch

`Tools/Scripts/update-qtwebkit-libs`

* Building after change in module set or configuration

`JHBUILD_WIPE_ON_CHANGE=0 Tools/Scripts/update-qtwebkit-libs`

* (Almost) direct use of `jhbuild`:

```
Tools/jhbuild/jhbuild-wrapper --qt <commands>
Tools/jhbuild/jhbuild-wrapper --qt list             # List all packages
Tools/jhbuild/jhbuild-wrapper --qt info qt          # Package "qt" information
Tools/jhbuild/jhbuild-wrapper --qt buildone -f qt   # Force rebuild "qt" package
```
