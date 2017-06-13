https://trac.webkit.org/changeset/217896/webkit  Assertion failure in com.apple.WebKit.WebContent.Development in com.apple.JavaScriptCore: JSC::DFG::SpeculativeJIT::nonSpeculativePeepholeBranchNullOrUndefined + 141

+ https://trac.webkit.org/r217894 [CMake] Only force response files for Ninja with CMake < 3.2 on Linux

https://bugs.webkit.org/show_bug.cgi?id=164532  [WK2] Network cache speculative revalidation can cause loads to hang

https://bugs.webkit.org/show_bug.cgi?id=164094 + https://bugs.webkit.org/show_bug.cgi?id=164350 (Qt fix needed probably) + r208319

https://bugs.webkit.org/show_bug.cgi?id=161546 Need to updateEditorState if an element change edit-ability without changing selection (?)

https://trac.webkit.org/r216240 [GStreamer] Do not report more errors after the first one 

https://trac.webkit.org/r216239 [GStreamer] Fix handling of gst errors in MediaPlayerPrivateGStreamer::handleMessage

https://trac.webkit.org/r216135  Async image decoding should be disabled for snapshots, printing and preview

https://bugs.webkit.org/show_bug.cgi?id=170767  [GStreamer] Dailymotion live stream videos don't play

https://bugs.webkit.org/show_bug.cgi?id=171051 Increase large animation cutoff

​https://bugs.webkit.org/show_bug.cgi?id=170332 [GTK+] Crash in WebCore::ImageFrame::ImageFrame()

https://bugs.webkit.org/show_bug.cgi?id=168839 Download attribute should be sanitized before being used as suggested filename

https://bugs.webkit.org/show_bug.cgi?id=166420  Crash in WebCore::CoordinatedGraphicsLayer::notifyFlushRequired

(?) https://trac.webkit.org/r214561  Animated SVG images are not paused in pages loaded in the background

+ https://bugs.webkit.org/show_bug.cgi?id=167901 Animated GIFs fail to play in multi-column layout 

http://trac.webkit.org/changeset/201709 - [css-grid] Horizontal scroll must account for grid container's height

http://trac.webkit.org/changeset/202166 - we need somethink like this for embedded targets


https://bugs.webkit.org/show_bug.cgi?id=156136

https://trac.webkit.org/changeset/201895

https://trac.webkit.org/r202712

https://trac.webkit.org/changeset/202819 (?)

https://trac.webkit.org/changeset/202857

https://bugs.webkit.org/show_bug.cgi?id=134915 - consider something like this?

+ https://trac.webkit.org/r203240 

+ https://bugs.webkit.org/show_bug.cgi?id=159858 DFG CSE is broken for MultiGetByOffset

https://bugs.webkit.org/show_bug.cgi?id=158297

https://trac.webkit.org/r204339 

https://bugs.webkit.org/show_bug.cgi?id=152316

+ https://bugs.webkit.org/show_bug.cgi?id=161985 - JSC warnings

https://trac.webkit.org/changeset/209821  CSP: Allow HTTPS URL to match HTTP source expression

 https://trac.webkit.org/r211867 [GTK] Reduce TiledBackingStore tile coverage when on memory pressure state

and other patches about memory pressure


# OWR

https://trac.webkit.org/r204409

https://trac.webkit.org/r204410 

# Qt-5x2

```
20fab5c87d0f1e64d7678f5a5972888aefc3b2d0
```

### Qt
```
4ecb913768ff0806c6efdff4567ef5907f597e4a
0fb890062142f95432daaa58d4e093c9dcf18044
```

https://bugs.webkit.org/show_bug.cgi?id=113393



### Mac player

https://bugs.webkit.org/show_bug.cgi?id=159812

https://bugs.webkit.org/show_bug.cgi?id=160326

https://bugs.webkit.org/show_bug.cgi?id=160519

https://bugs.webkit.org/show_bug.cgi?id=135164

https://bugs.webkit.org/show_bug.cgi?id=162701

https://bugs.webkit.org/show_bug.cgi?id=163641

https://bugs.webkit.org/show_bug.cgi?id=163983 + r208161 + r208171 + r208175

### Conflicts

https://bugs.webkit.org/show_bug.cgi?id=160474

https://bugs.webkit.org/show_bug.cgi?id=160010

https://bugs.webkit.org/show_bug.cgi?id=166357

+ https://bugs.webkit.org/show_bug.cgi?id=166422

https://bugs.webkit.org/show_bug.cgi?id=160212

https://bugs.webkit.org/show_bug.cgi?id=160211

https://bugs.webkit.org/show_bug.cgi?id=160366

https://bugs.webkit.org/show_bug.cgi?id=160425 + https://bugs.webkit.org/show_bug.cgi?id=160438 

https://bugs.webkit.org/show_bug.cgi?id=160470 https://bugs.webkit.org/show_bug.cgi?id=160470 Cleanup HTMLMediaElement track lists

https://bugs.webkit.org/show_bug.cgi?id=160488 Update breaking rules to match ICU 57

https://bugs.webkit.org/show_bug.cgi?id=160806 Fix in ConnectionMac

https://bugs.webkit.org/show_bug.cgi?id=143653 + https://bugs.webkit.org/show_bug.cgi?id=160905 Upgrade-Insecure-Request state is improperly retained between navigations

https://bugs.webkit.org/show_bug.cgi?id=160261 concatAppendOne should allocate using the indexing type of the array if it cannot merge

https://bugs.webkit.org/show_bug.cgi?id=160228 [JSC] Fix a bunch of use-after-free of DFG::Node

https://bugs.webkit.org/show_bug.cgi?id=160282 StringView should have an explicit m_is8Bit field

https://bugs.webkit.org/show_bug.cgi?id=160832 Make JSValue::strictEqual() handle failures to resolve JSRopeStrings

https://bugs.webkit.org/show_bug.cgi?id=160792 OverridesHasInstance should not branch across register allocations

https://bugs.webkit.org/show_bug.cgi?id=161927  DFG NewArrayBuffer node should watch for "have a bad time" state change.

https://bugs.webkit.org/show_bug.cgi?id=161031 %TypedArray%.prototype.slice needs to check that the source and destination have not been detached

https://bugs.webkit.org/show_bug.cgi?id=161202 https://bugs.webkit.org/show_bug.cgi?id=161256 Crash when getting font bounding rect (MATHML)

https://bugs.webkit.org/show_bug.cgi?id=161893 ParkingLot is going to have a bad time with threads dying

https://bugs.webkit.org/show_bug.cgi?id=162520 Do not follow redirects when sending violation report

https://bugs.webkit.org/show_bug.cgi?id=163359 RenderRubyRun should not mark child renderers dirty at the end of layout.

https://bugs.webkit.org/show_bug.cgi?id=162459 Array.prototype.join should do overflow checks on string joins

https://bugs.webkit.org/show_bug.cgi?id=163149 [WebGL] Revise vertex array attribute checks to account for lazy memory allocation.

+ https://bugs.webkit.org/show_bug.cgi?id=163862 Do not update selection rect on dirty lineboxes

https://bugs.webkit.org/show_bug.cgi?id=154377 Invoking Object.prototype.__proto__ accessors directly should throw a TypeError

https://bugs.webkit.org/show_bug.cgi?id=164081 JSFunction::put() should not allow caching of lazily reified properties

https://bugs.webkit.org/show_bug.cgi?id=162708 + r206637 Change the MemoryCache and CachedResource adjustSize functions to take a long argument

+ https://bugs.webkit.org/show_bug.cgi?id=163877 Prevent hit tests from being performed on an invalid render tree

https://bugs.webkit.org/show_bug.cgi?id=164163 Do a better job of protecting Frame objects in the context of JavaScript calls

https://bugs.webkit.org/show_bug.cgi?id=163814 REGRESSION (Safari 10 / r189445): WKWebView and WebView no longer allow async XMLHttpRequest timeout to exceed 60 seconds

https://bugs.webkit.org/show_bug.cgi?id=164650 + r208619  We recursively grab a lock in the DFGBytecodeParser causing us to deadlock

https://webkit.org/b/164702 WebContent crash due to checked unsigned overflow in WebCore: WebCore::RenderLayerCompositor::requiresCompositingLayer

https://bugs.webkit.org/show_bug.cgi?id=165145 Use 'childOfType' template when retrieving Shadow DOM elements

https://bugs.webkit.org/show_bug.cgi?id=165503 https://bugs.webkit.org/show_bug.cgi?id=165542 https://bugs.webkit.org/show_bug.cgi?id=165542 performance.now() should truncate to 100us

https://trac.webkit.org/r206023  - ASAN MSE


### Emoji

https://bugs.webkit.org/show_bug.cgi?id=159755

https://bugs.webkit.org/show_bug.cgi?id=160102

https://bugs.webkit.org/show_bug.cgi?id=160349

https://bugs.webkit.org/show_bug.cgi?id=160008

https://bugs.webkit.org/show_bug.cgi?id=161664