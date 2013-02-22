tmpfs是基于内存的虚拟文件系统， 由于是基于内存的，因此文件读取/写入速度比硬盘上的要快！ 但是也有个缺点，断电后内容都会消失。

ubuntu默认开启tmpfs，挂载在/run/shm下（网上很多说是/dev/shm,其实/dev/shm只是/run/shm的链接而已）,
默认容量是内存的一半。 

把系统/tmp目录放到内存以提高速度。
修改/etc/fstab：

```bash
#修改run/shm的最大容量
tmpfs /run/shm tmpfs defaults,size=5120M 0 0
#把/tmp目录挂载到内存
tmpfs /tmp tmpfs defaults,size=2048M,noatime 0 0
```

把chrome的cache目录放到内存：
```
google-chrome --disk-cache-dir="/run/shm/chrome-cache"
```