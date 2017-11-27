Re-run cmake with enabled `CMAKE_EXPORT_COMPILE_COMMANDS` option 

Apply modernization rule to Qt-related files and headers they include:
```
find Source/ -ipath '*qt*.cpp' -exec \
    clang-tidy -p=build/qt-clang/Debug --header-filter=./Source {} \
    -checks=-*,modernize-use-override -fix \;
```
Without fix it will only issue warnings, not change code

Hack to skip override added to destructors:
```
git diff | grep -v '~' | egrep '^\+' | less
```

TODO: specify style, so `modernize-loop-convert` does not write code like `auto & thing`

## Clazy

Similarly:
```
find Source/ -ipath '*qt*.cpp' -exec \
    clazy-standalone -p=WebKitBuild/Release --header-filter=./Source {} \
    -checks=level1 \;
```


## Wishlist

### modernize-use-override

* Don't add `override` to dtors
* Add `final` in `final` classes

### modernize-loop-convert

* Use `auto*` for pointers
* Detect if begin/end iterators are saved before cycle begins, get rid of them
* Omit `m_` suffix in loop variable
* Drop braces if cycle reduces to single statement
* (Hard) Apply change only if there is clear improvement: less lines, index was used 2 times or more, etc. 