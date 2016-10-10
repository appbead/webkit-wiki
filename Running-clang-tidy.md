Re-run cmake with enabled `CMAKE_EXPORT_COMPILE_COMMANDS` option 

Apply modernization rule to Qt-related files and headers they include:
```
find Source/ -ipath '*qt*.cpp' -exec \
    clang-tidy -p=build/qt-clang/Debug --header-filter=./Source {} -checks=-*,modernize-use-override -fix \;
```