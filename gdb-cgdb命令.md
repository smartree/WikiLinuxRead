##gdb
* `r`: 运行（run）
* `c`： 继续运行（continue）
* `n`： 下一条语句（next）
* `s`： 进入函数体（step）
* `info b`: 列出所有的断点, b(breakpoint缩写)
* `del`: 清空所有断点。 
* `l file_name`: 显示file_name源码， l（list缩写）
* `b file_name:linux_num`: 在file_name源文件第line_num行设置断点， b（break）
* `bt`: 查看当前栈帧， bt(backtrace缩写)
* `attach pid`: attach到指定pid的进程。 多进程调试

**目录相关**
* `cd dir_name`: 切换工作目录， 生成的调试可执行文件不会包含源文件的路径，gdb会在当前目录查找相应源文件。
* `directory dir_name`: 设置gdb搜索源文件的目录， 常用于多文件调试

**运行参数args**
* `show args`： 显示程序运行参数
* `set args`: 设置程序运行参数， `set args 1 2 3`

##cgdb

**gdb窗口**
* `esc`: 转到cgdb窗口

**cgdb窗口**

与vim快捷键基本一致
* `jk`: 向上/向下移动
* `/` : 搜索
* `ctrl+b/f`: 向上/下翻页
* `空格`： 设置/取消当前行断点
* `i`： 转到gdb窗口
* `o`: 打开文件列表