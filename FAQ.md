### Why CMake?

Previously almost every WebKit port was using its own build system, and Qt port was using qmake. However, in recent years WebKit project is switching to CMake-based build system, which is shared between all ports. EFL, GTK, AppleWin and WinCairo are already using it, AppleMac supports it as experminental option. The only remaining upstream port not using CMake is iOS.

So, using CMake gives us 2 benifits:
* Avoid extra work needed to update qmake-based build system to current state of the art (especially parts dealing with custom code generators), and then maintain it.
* Be a part of WebKit community, contributing improvements to shared build system which could be used (and further improved!) by developers of other ports.