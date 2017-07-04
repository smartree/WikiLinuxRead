以`OS X`为事例：

1. 安装`mit-scheme`: `brew install mit-scheme`
2. 安装`wlwrap`: `brew install wlrap`
3. 下载这个[list](https://gist.githubusercontent.com/bobbyno/3325982/raw/fc0208d287e56adc12b4c76114fcd21a107082ad/mit_scheme_bindings.txt), 保存到`$HOME/.scheme_completion.txt`
4. 执行`wlwrap -r -c -f `$HOME`/.scheme_completion scheme` 进入`mit-scheme`终端，编写程序。


**Note**: 
其实第一步已经完成基本的安装，在终端输入`scheme`命令，就可以运行`scheme`程序。但是`mit-scheme`太难用：不支持方向键编辑，不支持反向查找历史命令记录。但是我们可以使用`wlrap`支持这些特性，这样用着也更方便。

## Reference

http://deathking.github.io/2015/08/07/armored-your-mit-scheme/