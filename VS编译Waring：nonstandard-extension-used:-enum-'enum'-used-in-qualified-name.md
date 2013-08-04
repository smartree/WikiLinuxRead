今天编译编译chromium的时候，出现下面compile warning message:

`nonstandard extension used: enum 'enum' used in qualified name`

查了一下，发现是使用类中枚举类型出错误，不符合标准，不需要在前头加枚举类型的名字，这是个语法错误。
```
// C4482.cpp
// compile with: /c /W1
struct S {
   enum E { a };
};

int i = S::E::a;   // C4482
int j = S::a;   // OK
```

参考链接：http://msdn.microsoft.com/en-us/library/ms173704(v=vs.80).aspx