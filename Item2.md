##C++转型操作符
  * static_cast: 所有的编译器隐式转换都可以由它完成, 如int->double这种 
  * const_cast: 去除const变量的const,即除常量性
  * dynamic_cast: 用于指向base类指针/引用向下转换,转换成derived类的指针/引用; 如果不成功,返回null(指针)/抛出exception(引用);用于运行时识别指针对象/引用对象
  * reinterpret_cast: 与编译平台相关,常用于不同指针之间互换,如int*->double*; 比static_cast更低层次的转换,但这种转型不具移植性.

>C语言强制类型转换是`(type) expression`, C++为什么要提供4个新的类型转换符?

可以在源码中快速查找到哪些地方使用了类型转换;每次转型比C有明确的意图,相比之下C的所有的转型都是同一代码