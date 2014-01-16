```
// see the VLOG(1) in all full pathname with */storage_monitor.cc
./chrome --vmdule=*/storage_monitor.cc=1
```

Remove most logging calls before checking in.  For the rare case when logging needs to stay in the codebase for a while, prefer DVLOG(1) to other logging methods.  This avoids bloating the release executable and in debug can be selectively-enabled at runtime by command-line arguments, like this: `./chrome --v=2 --vmodule=foo=1,*bar/baz*=3`.  This will globally print all log levels up through 2, but only through 1 for foo.cc and 3 for any module with the string bar/baz in its full pathname.