### Skip ChangeLogs in git grep

When searching for some generic terms or function names often used in code, you often get lots of matches in ChangeLog files which usually are not interesting (heck, we have git log for thet purpose with exactly same descriptions).

To fix it, add `':!*ChangeLog*'` at the end of your command, e.g.

    git grep -i PrivateBrowsingEnabled Source/ ':!*ChangeLog*'


### Partial revert of patch in git

When you revert patches removing Qt code from WebKit, sometimes it is easier to split this work ino steps. In particular, this is useful for enormous Tools patch.

    git show <commit> -- <path> | git apply --reverse

Source: http://stackoverflow.com/questions/5669358/can-i-do-a-partial-revert-in-git

### Finding useful downstream QtWebKit patches
Script that finds all patches in downstream QtWebKit repo, which were merged after Qt5x2 integration and were not cherry-picked from upstream in given source directory (requires git >= 2.4):

    git log --no-merges --invert-grep --grep=bugs.webkit.org/show_bug --grep=trac.webkit.org/changeset --grep=webkit.org/b/ --grep=git-svn-id: d441d6f39bb846989d95bcf5caf387b42414718d~1.. "$@"

*UPD* Above filter turned out to be too agressive, this is probably more appropriate:

    git log --no-merges --invert-grep --grep=git-svn-id: d441d6f39bb846989d95bcf5caf387b42414718d~1..

### List Qt-specific source in format suitable for PlatformQt.cmake:

    find "$1" -name qt -type d -exec find {} -name '*.cpp' \;