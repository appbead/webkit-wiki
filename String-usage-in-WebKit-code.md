A lot of Qt port code was designed around though of WTF::String as 16-bit string, like QString. However, for a long time it's not true and many fast paths in WebKit pass 8-bit ASCII values end to end. We should avoid unnecessary encoding change until it's really required to improve speed and reduce memory usage.

https://trac.webkit.org/wiki/EfficientStrings

* Avoid redundant QString usage when dealing with WTF::String values
* Use ASCIILiteral instead of QLatin1String and others where literal WTF::String is needed
* Use String(const char*) to make WTF::String from latin1 C string
* Use String::fromUTF8(const char*)to make WTF::String from UTF8 C string

Qt API usage:
* When API accepts QByteArray, use QByteArrayLiteral for literals
* When API accepts QString, use QStringLiteral for literals

http://doc.qt.io/qt-5/QString.html#more-efficient-string-construction

https://wiki.qt.io/Using_QString_Effectively