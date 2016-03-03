Items in this list need manual check, or even better indenitfying corresponding LayoutTest and passing it.

* Typesetting features: kerning, ligatures, small caps and letter spacing
* Subpixel rendering

    WebKit switched from int to floating point geometry computations in many places, but some Qt painting code deals only with integer geometries. Check if we need to fix anythings.

* MIME sniffing code

    MIME sniffing was added into WebKit in https://bugs.webkit.org/show_bug.cgi?id=46968 as a generic component with Qt implementation, however other ports didn't use it and it was removed from trunk. Find out how do other ports solve this issue. It may happen that MIMESniffing will be useful for WinCairo or some other port. It was also used by Blackberry port, but Blackberry was removed shortly after Qt. Soap seems to implement MIME sniffing inside library.

* We may have this bug: https://bugs.webkit.org/show_bug.cgi?id=154554

    See FontCache::createFontPlatformData