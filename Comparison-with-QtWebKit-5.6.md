| Feature       |5.8            |TP5|
| ------------- |:-------------:|:-------------:|
| ES2015          | ✘             | ✔ |
| Responsive images| ✘          | ✔ |
| HTML `<template>` | ✘           | ✔ |
| CSS selectors `::read-write` and `::read-only` | ✘           | ✔ |
| CSS property `-webkit-initial-letter`| ✘           | ✔ |
| Fullscreen API | ✘           | ✔ |
| WebAudio      | ✘           | ✔ (Experimental with GStreamer) |
| MediaSource   | ✘           | ✔ (Experimental with GStreamer) |
| Encrypted Media | ✘           | ✘ (Planned for GStreamer, help needed) |
| APNG images   | ✘             | ✔ |
| B3 JIT compiler | ✘           | ✔ (Not available on Windows yet) |
| CSS selector JIT | ✘           | ✔  |
| Indexed Database | ✔            | ✔ |
| Indexed Database in Workers | ✔            | ✘ (supported in WebKit trunk) |
| Private browsing | ✔            | ✘ (Planned) |
| Smooth scrolling | ✔            | ✘ (Available in latest snapshot) |
| WebGL          | ✔   | ✔ |
| Web SQL Database | ✔            | ✔ |
| Accelerated compositing | ✔   | ✔ |
| NPAPI Plugins  | ✔            | ✔ (Not available on macOS yet) |
| Qt Plugins     | ✔            | ✔ |
| QML API        | ✔            | ✘ (WIP; try out wk2 branch on Linux) |
| QML API: Downloads | ✔            | ✘ |
| QML API: HTML 5 Video | ✔            | ✘ |
| QML API: WebGL | ✔            | ✘ |
| Security fixes | ✘            | ✔ |

### Important behavior changes
* Mixed content is blocked by default. To restore old behavior use ...
* JPEG and PNG images no longer use Qt plugins (qpng and qjpeg) on Windows and macOS (actually, on any OS if Qt build uses bundled libraries)