RebaselineServer is a tool that helps to analyze results of LayoutTests, and update ("rebase") expected results. See https://trac.webkit.org/wiki/RebaselineServer for more info.

There is alternative tool, garden-o-matic, but AFAIU it is intended for gardening on buildbot slave, not for local results. See https://trac.webkit.org/wiki/Rebaseline

### Bugs 
* Bug: Queue UI is overlapped by status bar and sometimes by text diff
* Bug: don't list reftests, it is not possible to rebaseline them
    * `garden-o-matic` gets this right
* Bug: footer is not stick to the bottom, it is scrolled with page and permanently hides part of test results. It also scrolls with page in horizontal direction, which harms usability
* Bug: if test doesn't have expected result (MISSING), text and image actual results are not shown. Requires modification of full_results.json contents to include `"actual": "TEXT"` or `"actual": "IMAGE+TEXT"` for tests with MISSING expectation

### Performance

* Add all files from queue with a single git command. Right now separate HTTP request to server is issued for each file.

Or maybe just do `git add` immediately instead of using queue, and `git reset` for "unqueue" action ("x"). This solves persistence issue (see below) and may be fast enough.

### Ergonomical issues
* Improve color scheme for better text visibility
* Copy test path to clipboard with one click (or allow to select text in dropdown list)
* Make UI more responsive, should be usable on 1280x1024 without constant scrolling. Heck, even on 1920x1080 scrolling is needed sometimes. Wiki tells "The UI works best on a 30 inch monitor", it's a no-go for most users. Possible options (one may or may not exclude others):
    * Shrink image areas to fit screen when there are large blank margins
    * Use horizontal scroll bars in image areas, connected to each other
        * Initial scroll position - where most significant image differences where found
    * Loupe should have flexible zoom level to allow comparison of larger areas
        * Take loupe component from `garden-o-matic`?
    * Wrap image area which does not fit in a row to another row. Requires more vertical scrolling, but it is more handy than horizontal
    * Shortcuts to navigate between areas (expected image, actual image, diff image, expected text, etc.)
* Loupe should always be positioned inside current scroll window
* Footer should always fit in one line, otherwise on small screen it eats up too much space
* Queue should be persistent: either in LocalStorage or on server side. Closing browser should not discard queue.
* Link to local files instead of trac.webkit.org (it's slow and can reference files which are not present in trunk)
* Show expected result from other port instead of current expectation. Add `<select>` near "expected" area?
    * Use local files (see previous item)
    * Will help with footer height issue because expectation list will be moved from footer to othewr place

### Nice to have

* Set default baseline target? It's boring to set it manually to `qt` each time
* Use `run-minibrowser` instead of launching default browser?
* Add appropriate failure entries to TestExpectations from UI for current test, instead of adding it to queue. Do we need separate queue for TestExpectations changes?
* Add keyboard shortcuts hint ;-)
* Indicate that queue is being processed (not obvious when activated with `r`)
* Remember last reviewed test case (or at least last enqueued), using the same approach as with persistent queue