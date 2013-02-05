mac自带的vim，很多属性都不支持，基本的clipboard，python，ruby都不支持。
还是得下载源码编译：

1. 从[vim官网](http://www.vim.org/sources.php)下载vim73源码。
2. 解压后进入目录，执行命令，生成makefile文件:
```bash
    ./configure --with-features=huge --enable-pythoninterp --enable-rubyinterp
```

3. 编译:`make -j4`
4. 把mac原来的vim保存起来(在/usr/bin下)后，执行下面命令安装:`sudo make install`

通过命令：`vim --version`

查看当前vim的支持属性，+代表支持，-代表不支持