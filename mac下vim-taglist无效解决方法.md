vim的tagslist插件是需要系统安装ctags程序，虽然mac自带有ctags程序，但这个ctags不是exuberant的，导致vim的插件taglist无效。

解决方法从[官网](http://ctags.sourceforge.net/)下载源码编译：

```bash
    ./configure
    make -j4
```

编译后，把原来的ctags程序(在`/usr/bin`目录下)删除。然后再把编译后的ctags程序放到`/usr/bin`目录

另外还可以在vimrc文件中通过设置`Tlist_Ctags_Cmd`设置ctags路径。

```vim
    """里面的是编译后的ctags路径，要包含ctags，不能只是目录
    let Tlist_Ctags_Cmd="your_path/ctags" 
```