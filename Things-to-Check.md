Items in this list need manual check, or even better indenitfying corresponding LayoutTest and passing it.

* Typesetting features: kerning, ligatures, small caps and letter spacing
* Subpixel rendering

    WebKit switched from int to floating point geometry computations in many places, but some Qt painting code deals only with integer geometries. Check if we need to fix anythings.

* MIME sniffing code

    MIME sniffing was added into WebKit in https://bugs.webkit.org/show_bug.cgi?id=46968 as a generic component with Qt implementation, however other ports didn't use it and it was removed from trunk. Find out how do other ports solve this issue. It may happen that MIMESniffing will be useful for WinCairo or some other port. It was also used by Blackberry port, but Blackberry was removed shortly after Qt. Soap seems to implement MIME sniffing inside library.

* We may have this bug: https://bugs.webkit.org/show_bug.cgi?id=154554

    See FontCache::createFontPlatformData

### Qt bugs
* https://bugreports.qt.io/browse/QTBUG-34280
* https://bugreports.qt.io/browse/QTBUG-34277
* https://codereview.qt-project.org/#/c/72627/ - maybe not needed after https://bugs.webkit.org/show_bug.cgi?id=120593
* QTBUG-35208 - ?
* https://codereview.qt-project.org/#/c/73823/ - shouldn't it use direction of current element instead of application?
* https://bugreports.qt.io/browse/QTBUG-34203 https://codereview.qt-project.org/#/c/72425/
* QTBUG-35996 - old patch is for generic WK2 code and does not apply https://codereview.qt-project.org/#/c/75037/
* https://codereview.qt-project.org/#/c/76500/
* QTBUG-36591
* QTBUG-37043 https://codereview.qt-project.org/#/c/80043/
* QTBUG-37029
* QTBUG-37636
* QTBUG-38809 (test case?)
* QTBUG-38841 626e0c352765ecbe4211861b00d6ed56d974204e
* QTBUG-38067
* 29dd87ecc570ebc51890e0587e73e7a144d892aa
* 9e99dad77b3e885e5c5a1622ba12fbc947984250
* QTBUG-38356 27428976e442973a4dd1cf323f555dd2583a3ee9
