在导入Chromium代码时, 发现Souce Insight只导入了`.h`文件, `.cc`文件没有导入.
Source Insight对C++项目的导入,其文件过滤没有包含`*.cc`文件, 需要自己手动设置导入:

1. `options`->`document options`->在`document type`中选择`C++ Source`->在右边的`File Filter`里加上`*.cc`文件
2. 重新添加项目文件:
     `project`->`Add and Remove Project files`