### Memory allocation
* New memory allocator bmalloc is now used instead of tcmalloc

### JavaScriptCore

* Fetch API
* Nearly complete ES6 support (https://webkit.org/blog/4054/es6-in-webkit/), including proper tail calls
* JavaScript now uses C stack
* FTL/B3 - new JIT tier providing more aggressive optimizations than DFG JIT (currenly available only for x86_64)
* More optimizations for ASM.js code
* WebAssembly support is in development
* Various performance improvements
* Improved Inspector and other tooling

### WebCore

* JIT for CSS selectors (https://webkit.org/blog/3271/webkit-css-selector-jit-compiler/)
* Various new web standards are now supported in GStreamer MediaPlayer implementation: MediaSource, MediaStream (WebRTC), WebAudio, <track> element.
* Content Blocking API (https://webkit.org/blog/3476/content-blockers-first-look/)