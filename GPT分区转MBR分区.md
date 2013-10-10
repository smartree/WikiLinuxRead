今天在清空chromeOS的安装U盘时，发现在windows无法把它格式化，尽管在磁盘管理器那里尝试删除分区，还是不成功。
在磁盘管理那里，发现整个U盘分成很多个块和分区。清空的方法很简单：把U盘的分区全部删除，重新建立一个分区就好了。

在linux下使用`fdisk`命令，但是输入命令后提示:

`Warning!! Unsupported GPT (GUID Partition Table) detected. Use GNU Parted`

说这是GPT分区格式，`fdisk`不支持，原来chromeOS是用GPT分区表的！

需要使用`gdisk`把GPT分区转换成MBR分区:
```
// install
sudo apt-get install gdisk
// input your storage device node.
sudo gdisk /dev/sdc
r // switch to recovery mode
g // GPT to MBR
```

转换完后，使用`fdisk`根据提示删除和创建新的分区。

创建完分区后需要在分区上格式化(创建文件系统)后才能用:
```
// format partition, FAT32
sudo mkfs.vfat /dev/sda1
```

PS. 查看设备节点命令：
```
sudo fdisk -l
```