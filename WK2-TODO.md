* Do we really need this in `ProcessLauncher::launchProcess()`
```
#if OS(UNIX)
    setpriority(PRIO_PROCESS, webProcessOrSUIDHelper->pid(), 10);
#endif
```
We can lower priority of "inactive" web processes (or even use SCHED_IDLE), and raise it back on activation. Look what Mac port does

* ProcessLauncher::launchProcess() really needs code cleanup, it's a mess. Especially how commandLine is constructed
* Do we still need SUID sandbox? It's hard to use and complicates the code


ShareableResource - improves the network cache performance, by mmaping big resources and sending only the file descriptor to the web process instead of the actual file data

https://bugs.webkit.org/show_bug.cgi?id=144380


### Breaking patches - analyze their fixes
* https://bugs.webkit.org/show_bug.cgi?id=131353 "Unify and factor out page overlay implementations"
* https://bugs.webkit.org/show_bug.cgi?id=137164 "Move PageOverlay[Controller] to WebCore"

1f2f334f0e9 [CoordinatedGraphics] Possible wrong rendering with scrolling https://bugs.webkit.org/show_bug.cgi?id=146958
1caf14b1723 [EFL][CoordinatedGraphics] All EFL layout tests are broken since r174231 https://bugs.webkit.org/show_bug.cgi?id=137443
abea5c8dce6 [EFL] Fix build break since r174231 and r174256 https://bugs.webkit.org/show_bug.cgi?id=137384
474a058dd2a Make page overlay functionality working on coordinated graphics. https://bugs.webkit.org/show_bug.cgi?id=131425