在C++中常在头文件见到extern "C"修饰函数，那有什么作用呢？ 是用于C++链接在C语言模块中定义的函数。

C++虽然兼容C，但C++文件中函数编译后生成的符号与C语言生成的不同。因为C++支持函数重载，C++函数变异后生成的符号带有函数参数类型的信息，而C则没有。

例如`int add(int a, int b)`函数经过C++编译器生成.o文件后，`add`会变成形如`add_int_int`之类的, 而C的话则会是形如`_add`, 就是说：相同的函数，在C和C++中，编译后生成的符号不同。

这就导致一个问题：如果C++中使用C语言实现的函数，在编译链接的时候，会出错，提示找不到对应的符号。此时`extern "C"`就起作用了：告诉链接器去寻找`_add`这类的C语言符号，而不是经过C++修饰的符号。

C++调用C函数的例子: 引用C的头文件时，需要加`extern "C"`

```
//cExample.h
#ifndef C_EXAMPLE_H
#define C_EXAMPLE_H
int add(int x,int y);
#endif

//cExample.c
#include "cExample.h"
int add( int x, int y ) {
  return x + y;
}

//cppExample.cpp
extern "C" {
  #include "cExample.h"
}

int main(int argc, char* argv[]) {
  add(2,3); 
  return 0;
}
```

```bash
//Generate cExample.o file
gcc -c cExample.c
g++ -c cppExample.cpp
g++ -o cExample.o cppExample.cpp -o main
```

注意，如果`cppExample.cpp`中没有`extern "c"`的话，会在最后一步链接的时候出错。

C中调用C++函数：`extern "C"`在C中是语法错误，需要放在C++头文件中。

```
// cppExample.h
#ifndef CPP_EXAMPLE_H
#define CPP_EXAMPLE_H
extern "C" int add( int x, int y );
#endif

// cppExample.cpp
#include "cppExample.h"
int add( int x, int y ) {
  return x + y;
}

// cExample.c
extern int add( int x, int y );
int main() {
  add( 2, 3 ); 
  return 0;
}
```

**Reference**: http://www.cppblog.com/macaulish/archive/2008/06/17/53689.html