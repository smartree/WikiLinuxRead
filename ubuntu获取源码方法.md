以下载ls的源码为例说明:

首先要知道ls是属于哪个包的，可以通过下面命令：
```bash
    #dpkg -S 'command name' 通用格式
    $ dpkg -S /bin/ls
```
得到如下结果：
```bash
    coreutils: /bin/ls
```
注意这里要把ls的所在路径全写出来，直接用ls的话，会输出很多无关内容的。
如果不知道命令所在的目录，可以用下面命令查看：
```bash
    $ which 'command'
```
就可以知道ls程序是在coreutils包里面，我们只需要下载coreutils包的源码即可找到ls的源码。
通过`apt-get source`命令下载：
```bash
    /usr/local/src/$ sudo apt-get source coreutils
```
上面命令就会把coreutils下载到/usr/local/src/目录下。

要是想编译的话，按照标准的GNU程序编译即可：
```bash
    sudo ./configure
    make
```
当make成功后，会在src的目录下生成可执行文件，直接运行即可。