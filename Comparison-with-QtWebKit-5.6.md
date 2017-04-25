| Feature       |5.8            |Alpha|
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
| Smooth scrolling | ✔            | ✔ |
| Tiled backing store | ✔            | ✘ (Will come back someday) |
| WebGL          | ✔   | ✔ |
| Web SQL Database | ✔            | ✔ |
| Accelerated compositing | ✔   | ✔ |
| NPAPI Plugins  | ✔            | ✔ (Not available on macOS yet) |
| Qt Plugins     | ✔            | ✔ |
| QML API        | ✔            |✔ (not available on Windows and macOS yet, see wk2 branch |
| QML API: Downloads | ✔            | ✔ |
| QML API: Authentication | ✔            | ✘ (Planned) |
| QML API: Custom URL Schemes | ✔            | ✘ (Planned) |
| QML API: WebGL | ✔            | ✘ (Planned) |
| QML API: NPAPI plugins | ✔ (Only X11)            | ✘ (WIP, only X11) |
| Security fixes | ✘            | ✔ |

### Important behavior changes
* Mixed content is blocked by default. To restore old behavior use ...
* JPEG and PNG images no longer use Qt plugins (qpng and qjpeg) on Windows and macOS (actually, on any OS if Qt build uses bundled libraries)