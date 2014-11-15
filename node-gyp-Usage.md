```
// output the build commands.
node-gyp --verbose rebuild

// build Debug version
node-gyp configure --debug

// generate xcode build project.
node-gyp configure -- -f xcode
```