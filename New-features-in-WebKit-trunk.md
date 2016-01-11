### JavaScriptCore

* Fetch API
* Partial ES6 support (https://webkit.org/blog/4054/es6-in-webkit/), including tail call optimization
* JavaScript now uses C stack
* FTL JIT - ultimate JIT tier which compiles JS using LLVM (https://webkit.org/blog/3362/introducing-the-webkit-ftl-jit/)
    * New B3 backend for FTL is in development, it does not depend on LLVM and is much faster and more portable
* WebAssembly support is in development

### WebCore

* JIT for CSS selectors (https://webkit.org/blog/3271/webkit-css-selector-jit-compiler/)
* MediaSource and MediaStream (WebRTC) support in GStreamer MediaPlayer implementation
* Content Blocking API (https://webkit.org/blog/3476/content-blockers-first-look/)