### Partial revert of patch in git

When you revert patches removing Qt code from WebKit, sometimes it is easier to split this work ino steps. In particular, this is useful for enormous Tools patch.

    git show <commit> -- <path> | git apply --reverse

Source: http://stackoverflow.com/questions/5669358/can-i-do-a-partial-revert-in-git

### Finding useful downstream QtWebKit patches
Script that finds all patches in downstream QtWebKit repo, which were merged after Qt5x2 integration and were not cherry-picked from upstream in given source directory (requires git >= 2.4):

    git log --no-merges --invert-grep --grep=bugs.webkit.org/show_bug --grep=trac.webkit.org/changeset --grep=webkit.org/b/ --grep=git-svn-id: d441d6f39bb846989d95bcf5caf387b42414718d~1.. "$@"

### List Qt-specific source in format suitable for PlatformQt.cmake:

    find "$1" -name qt -type d -exec find {} -name '*.cpp' \;