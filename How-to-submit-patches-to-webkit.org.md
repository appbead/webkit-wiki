Note: WebKit uses Bugzilla as a code review tool, i.e. it has the same role as Gerrit in Qt project. Occasionally, it is used for bug reporting, but most issues are created solely for code submission.

* https://webkit.org/contributing-code/
* http://trac.webkit.org/wiki/CodeReview
* http://trac.webkit.org/wiki/UsingGitWithWebKit
* Some information of http://trac.webkit.org/wiki/QtWebKitContrib is still relevant

How I (annulen) do it now:

1. Create feature branch from master
2. Develop or cherry-pick patch implementing feature. Next steps expect that feature is implemented as exactly 1 commit on top of master.
3. Run Tools/Scripts/check-webkit-style, fix any errors it finds
4. Open new bug on https://bugs.webkit.org in WebKit product, choose proper component, use the same bug title as git commit title. Put in some description, e.g. description from git commit.
5. Tools/Scripts/prepare-ChangeLog -b <your new bug id> -g HEAD
6. Fix changes in ChangeLog files
7. Tools/Scripts/webkit-patch upload --request-commit -g HEAD

Some tips:
* In my setup upstream WebKit is cloned from git://git.webkit.org/WebKit.git, it is my "origin" remote. Master of annulen/webkit is periodically synced with upstream, but tends to be outdated. Mirrot at WebKit/webkit tends to lag behind git.webkit.org, but very slightly.
* If you are not sure in your patch and you need us to review it before upstream reviewers, at step 7 use

    Tools/Scripts/webkit-patch upload --no-review -g HEAD

Look at Tools/Scripts/webkit-patch --help and Tools/Scripts/webkit-patch help upload for more details

Glossary:
* Commit Queue (cq): thingy that lands patches for those who don't have committer rights. --request-commit sets cq+ flag on patch.
* Early Warning System (EWS): system akin to Qt CI, but it runs before (or in parallel to) code review. After patch is landed, it is built on larger number of platforms (https://build.webkit.org/waterfall), and may require rollback.
* r+, r=me: reviewer has approved your patch