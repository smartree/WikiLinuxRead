我们在调试LLVM/Clang代码的时候, 很常用的方法是在程序代码某些环节,添加`print`语句输出某些变量的过程以帮助我们定位问题. 当问题解决后,再把这些debug的语句删除, 再提交代码. 但是这个方法每次都得先添加`print`语句, 到最后再删掉, 这样太麻烦了.

那么有没一种方法既能保留程序里的Debug信息, 然而又可以对程用户隐藏这些信息呢? 答案是当然有得, LLVM提供了`DEBUG`宏和`-debug`命令行参数来解决我们这个问题.

`DEBUG`宏能够包含任意的执行语句, 通常用法是`DEBUG(llvm::dbgs() << "This is debug message.")`. 里面的语句只在程序在被提供`-debug`命令参数的时候执行, 也就是说我们要看Debug信息, 在启动程序时, 添加`-debug`, 像`clang -debug XXX`.

`DEBUG`宏使用, 需要在使用的源文件中添加`#define DEBUG_TYPE "my_tools"`. 另外有一点注意的是`-debug`会输出程序中所有的Debug信息, 这里面会包含别人代码. 如果想只输出自己的感兴趣那一部分, 使用`-debug-only=my_tools`.

官方更详细的文档: http://llvm.org/docs/ProgrammersManual.html#the-debug-macro-and-debug-option