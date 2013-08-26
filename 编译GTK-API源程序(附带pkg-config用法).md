编译使用gtk api的源程序，需要gtk lib的编译选项，否则编译不过

```
g++ -o main main.cpp `pkg-config gtk+-2.0 --cflags` `pkg-config gtk+-2.0 --libs`
```

`pkg-config`是linux下一个命令，用于在编译源码中提供依赖库信息，如寻找头文件信息、链接动态链接库等。
用法：
```
// 输出入相应头文件 -I/path/abc/
pkg-config name --cflags
// 输出相应链接库 -llibname
pkg-config name --libs
```
