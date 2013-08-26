编译使用gtk api的源程序，需要gtk lib的编译选项，否则编译不过

```
g++ -o main main.cpp `pkg-config gtk+-2.0 --cflags` `pkg-config gtk+-2.0 --libs`
```