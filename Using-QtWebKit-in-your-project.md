First of all you need to build QtWebKit (according to instructions for you OS), and install it (`ninja install` if you build with Ninja). In installation prefix you will get layout of directories, similar to what other Qt modules provide. 

By default QtWebKit uses Qt installation root as its CMAKE_INSTALL_PREFIX. You may want to change this value if you don't want to overwrite existing QtWebKit module (if it's present).

### QMake

As usual, just add `QT += webkitwidgets` or `Qt += webkit` to your `.pro` file.

However, to make this working when QtWebKit is installed outside of your Qt installation, you need to set `QMAKEPATH` variable in the environment or in `.qmake.conf` file.

For example, if your `CMAKE_INSTALL_PREFIX` in `/usr/local`, you need either to set `QMAKEPATH=/usr/local` in environment when you run qmake, or create `.qmake.conf` file in the same directory with your `.pro` file with the next contents:

```
QMAKEPATH += /usr/local
```

### CMake

After you've installed QtWebKit into Qt installation prefix, all documented ways to use Qt modules from cmake should work. Read below if you are installed to different prefix.

When invoking cmake you need to add argument `-DCMAKE_PREFIX_PATH=<installation prefix>`, for example `-DCMAKE_PREFIX_PATH=/usr/local`. If you are already you using `-DCMAKE_PREFIX_PATH=` to specify path to Qt SDK, and it already has QtWebKit installed, **prepend** QtWebKit prefix path to Qt SDK path, and separate them with semicolon, e.g.

```
cmake .. -DCMAKE_PREFIX_PATH="/tmp/install-webkit;/opt/Qt5.4.0/5.4/gcc_64"
```

In your `CMakeLists.txt` use command like
```
find_package(Qt5WebKitWidgets)
```
to find QtWebKit, and command like 
```
target_link_libraries(myapp Qt5::WebKitWidgets)
```
to use it in your application.

**WARNING**: Don't use `qt5_use_modules()`, it will force usage of QtWebKit installed within Qt SDK prefix.

### pkg-config

```
pkg-config --cflags Qt5WebKit
pkg-config --lflags Qt5WebKitWidgets
```
You may need to set PKG_CONFIG_PATH to use it. pkg-config will also need to find core Qt libraries, in this case, like with cmake, put QtWebKit path before Qt path if you already have QtWebKit installed.