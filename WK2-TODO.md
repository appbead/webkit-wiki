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