In general, most of [WebKit's contribuition guidelines](https://webkit.org/contributing-code/) apply, except that we use GitHub instead of Bugzilla for Qt-specific changes.

1. All code is required to follow [WebKit coding style](https://webkit.org/code-style-guidelines) and should pass style check performed by Tools/Scripts/check-webkit-style.
  * Exceptions can be made for old QtWebKit code restored from WebKit history
2. Qt-specific code should be submitted as a pull request against `qtwebkit-stable` branch.
3. Generic WebKit modifications, relevant for upstream ports, should be submitted directly to upstream (please contact us in case you are not sure what changes are appropriate for upstream). Share bugzilla link with us when patch is ready for review!

When cherry-picking patches from Qt Project's branch of QtWebkit, make sure that Qt-specific code is guarded with #if PLATFORM(QT)

All contributed code should use LGPL 2 or BSD license; see [[Licensing]]