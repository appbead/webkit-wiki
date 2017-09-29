JavaScript execution in WebKit can be performed in several "tiers", and if there is a bug its important to know which tier is affected (or it maybe just unrelated issue not caused by JavaScript VM).

Try running QtWebKit-based application with following environment variables. On each step, unset previously added variables (unless you know exactly what you are doing):
* `JSC_useJIT=0` - try running JS in interpreted-only mode, no compilation
* `JSC_useLLInt=0` - avoid using interpreter, use only JIT
* `JSC_useDFGJIT=0` - disable DFG and FTL tiers of JIT, leaving only baseline JIT
* `JSC_useFTLJIT=0` - disable FTL JIT (only makes sense if it is enabled in your build; FTL is not available on 32-bit platforms and on Windows)

<add here how to run application with variables>

More in-depth manual intended for WebKit developers and advanced users: https://webkit.org/blog/6411/javascriptcore-csi-a-crash-site-investigation-story