Chromium源码在Windows平台编译，有可能出现下面的编译错误：

```
warning C4819: The file contains a character that cannot be represented in the
current code page (949). Save the file in Unicode format to prevent data loss
```

是文件编码导致的。可以采取下面的做法：

1. 用编辑器打开该文件，以utf-8编码保存
2. 一个更彻底的方法通过系统设置:`control panel` -> `Regions` -> `Administrative` -> `Change system locale`, 选择`English`