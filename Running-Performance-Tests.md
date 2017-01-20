```
Tools/Scripts/run-perf-tests --release --platform=qt -1
```
As with layout tests you can specify directory to run tests from.

NB: Performance tests measure not only speed, but also memory consumption.

https://trac.webkit.org/wiki/Performance%20Tests

> If you're running a performance test locally in order to verify your patch doesn't regress or improves the performance of WebKit, you may find --output-json-path useful. Specify a file path such as perf-test.json and run-perf-tests will automatically store the results in the JSON file and creates perf-test.html that visualizes the test results. Execute run-perf-tests multiple times with the same output JSON path and it will automatically aggregate results in the JSON and the corresponding HTML document. 