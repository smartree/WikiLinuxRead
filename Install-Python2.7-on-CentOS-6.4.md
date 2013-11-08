CentOS 6.4 only ships with Python 2.6. We need to compile python source to install python2.7

##How to install python2.7

Preparations:

```shell
# yum groupinstall "Development tools"
# yum install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel
```

Donwload python2.7 source and install:

```shell
# wget http://python.org/ftp/python/2.7.3/Python-2.7.3.tar.bz2
# tar xf Python-2.7.3.tar.bz2
# cd Python-2.7.3
# ./configure --prefix=/usr/local
# make && make altinstall
```
Pay attantation to **altinstall**, not install. 
 