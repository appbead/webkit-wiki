1. All code should pass style check performed by Tools/Scripts/check-webkit-style.
2. Qt-specific code should be submitted as a pull request against qtwebkit-1 branch.
3. Generic WebKit modifications, relevant for ports leaving in upstream, should be submitted to upstream (please contact us in case you are not sure what changes are appropriate for upstream).

When cherry-picking patches from Qt Project's branch of QtWebkit, make sure that Qt-specific code is guarded with #if PLATFORM(QT)