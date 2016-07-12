* Bug: Queue UI is overlapped by status bar and sometimes by text diff
* Bug: don't list reftests, it is not possible to rebaseline them
* Improve color scheme for better text visibility
* Copy test path to clipboard with one click (or allow to select text in dropdown list)
* Make UI more responsive, should be usable on 1280x1024 without constant scrolling. Heck, even on 1920x1080 scrolling is needed sometimes. Wiki tells "The UI works best on a 30 inch monitor", it's a no-go for most users. Possible options (one may or may not exclude others):
    * Shrink image areas to fit screen when there are large blank margins
    * Use horizontal scroll bars in image areas, connected to each other
    * Loupe should have flexible zoom level to allow comparison of larger areas
    * Wrap image area which does not fit in a row to another row. Requires more vertical scrolling, but it is more handy than horizontal
* Queue should be persistent: either in LocalStorage or on server side. Closing browser should not discard queue.
* Link to local files instead of trac.webkit.org
* Set default baseline target?