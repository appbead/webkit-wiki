* Add `bool isBeforeUnload` (or enum) parameter to `QWebPage::javaScriptConfirm()` to distinguish beforeunload event
* `QWebPage::chooseFile` should be superceded by `chooseFiles` allowing multifile choice without using `ChooseMultipleFilesExtension`
* Change `consoleMessageReceived` from signal to virtual to be more in line with QtWebEngine?