### Why CMake?

Previously almost every WebKit port was using its own build system, and Qt port was using qmake. However, in recent years WebKit project is switching to CMake-based build system, which is shared between all ports. EFL, GTK, AppleWin and WinCairo are already using it, AppleMac supports it as experminental option. The only remaining upstream port not using CMake is iOS.