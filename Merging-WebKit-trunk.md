This text is an excerpt from QtWebKit2.3-MERGE by carewolf, may need updates for our current workflow

## 1. First find a build-version of trunk where the bot is green.
You can do this by looking at http://build.webkit.sed.hu/builders/x86-64 Linux Qt Release/
or browsing older build version by version number http://build.webkit.sed.hu/builders/x86-64 Linux Qt Release/builds/43099.

## 2. Once you find a good build version, find the SVN version and look that up that commit in the git log on gitorius, and
copy the header and footer of the commit to this file.
Personally I also keep a local branch called backstage that I reset to this commit. This can be used to make diffs against 
and thereby monitor the differences between the trees.

## 3. Merge in one of the following two ways.

### 3.1 git merge <git-version> -Xpatience
This is usually recommended, fix any merge errors, revert commits that shouldn't have been merged, and ensure everything builds before pushing.

### 3.2 git cherry-pick <former git-version>..<new git-version>
This cherry-picks an entire range of commits one commit at a time. If there is a lot of conflicts in the merge, this can help by making it 
possible to merge one commit at a time, or skip entire commits. Unfortunately it is prone to memory-leaks and will crash with out of memory
errors if merging more than a 100 commits at a time. So only cherry-pick a few days of commits. 
Since cherry-pick does not update the merge point, you need to follow this up with a git merge -sours <git-version> commmit, which performs
a virtual merge without changing anything. If you don't do this later merging will fail in ugly ways.

### 4. Wait for bots to report the tree green before merging qtwebkit-2.3-staging to qtwebkit-2.3. Also do not update qtwebkit-2.3 more than once
every few weeks, it is supposed to be more stable for other parties to build and test against.

