新机器配置windows下的chromium编译环境后，发现一个奇怪问题：

>每次改动源文件保存后，都会整个文件被修改了，每一行自动在后面加上windows下的换行符cr+lf(显示为^M).

这个问题在以前没有碰到过。之后找出原因，git设置出问题，应该要设置`git config --global core.autocrlf false`把autocrlf选项关闭。

如果该选项为true，则表示git会自动将文本文件（最经典是源码）的换行符转换当前操作系统的换行符(windows下为cr+lf，linux下为lf, mac下为cr)。例如：源码文件是linux下保存的，在windows下签出的时候，自动把lf转换层cr+lf，在签入的时候，则把cr+lf转换成lf回去。

如果需要在多操作系统下，一般是设置为true。windows下的msysgit默认是true，linux下则为false。

对于一般的源码文件是没有问题的，但是如果是bash文件，windows下的cygwin bash文件，这个就要注意了。设置为true后，签出的bash文件为多了\r\n, cygwin执行时会识别不出\r的。这个问题在编译Chromium就遇到了。在拉chromium代码时，要先把该选项设置为false在windows平台下，这样拉下来的所有源文件都不会被修改，以\n结尾。

**题外话**

vim检测当前换行符判断文件是unix或dos下文件。如果是unix文件，则以\n为换行符；如果是windows文件，则以\r\n为换行符。

在`:w`保存后，如果是与当前系统相同的文件，则不会显示相应信息；如果不同，则会显示类似`[unix]`,`[dos]`的字样。

在vim中要把文件中`^M`结尾的字符去掉（即\r\n转成\n），除了使用`dos2unix`命令外，还可以在vim中使用：`set fileformat=unix`然后再保存该文件。