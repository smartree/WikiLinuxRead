1. 安装[`aria2`](https://aria2.github.io/): `brew install aria2`(OSX)，`sudo apt-get install aria2`(Linux)
2. 安装Chrome的扩展[百度网盘助手](https://chrome.google.com/webstore/detail/baiduexporter/mjaenbjdjmgolhoafkohbhhbaiedbkno), 扩展安装后，在百度云盘上选中文件，会多出一个`导出下载`的选项。选项里面有`Aria2 RPC`和`导出下载`两种方式：

 * 选择`导出下载`，会有一个命令行，直接复制到命令下运行，会以命令行方式下载
 * `ARIA RPC`方式，则更友好，有Web界面管理，不过需要额外的工作：
    * 创建`aria2.conf`设置文件，[参考](https://blog.icehoney.me/posts/2015-01-31-Aria2-download)
    * 执行`aria2c --conf-path="/Users/xxxxxx/.aria2/aria2.conf" -D` 
    * 在百度网盘中，选中你想要下载的文件，然后选择`ARIA2 RPC`方式下载 
    * 在http://ziahamza.github.io/webui-aria2 查看和管理你的下载任务 



```
#用户名
#rpc-user=user
#密码
#rpc-passwd=passwd
#上面的认证方式不建议使用,建议使用下面的token方式
#设置加密的密钥
#rpc-secret=token
#允许rpc
enable-rpc=true
#允许所有来源, web界面跨域权限需要
rpc-allow-origin-all=true
#允许外部访问，false的话只监听本地端口
rpc-listen-all=true
#RPC端口, 仅当默认端口被占用时修改
#rpc-listen-port=6800
#最大同时下载数(任务数), 路由建议值: 3
max-concurrent-downloads=5
#断点续传
continue=true
#同服务器连接数
max-connection-per-server=5
#最小文件分片大小, 下载线程数上限取决于能分出多少片, 对于小文件重要
min-split-size=10M
#单文件最大线程数, 路由建议值: 5
split=10
#下载速度限制
max-overall-download-limit=0
#单文件速度限制
max-download-limit=0
#上传速度限制
max-overall-upload-limit=0
#单文件速度限制
max-upload-limit=0
#断开速度过慢的连接
#lowest-speed-limit=0
#验证用，需要1.16.1之后的release版本
#referer=*
#文件保存路径, 默认为当前启动位置
dir=/Users/<user_name>/Downloads
#文件缓存, 使用内置的文件缓存, 如果你不相信Linux内核文件缓存和磁盘内置缓存时使用, 需要1.16及以上版本
#disk-cache=0
#另一种Linux文件缓存方式, 使用前确保您使用的内核支持此选项, 需要1.15及以上版本(?)
#enable-mmap=true
#文件预分配, 能有效降低文件碎片, 提高磁盘性能. 缺点是预分配时间较长
#所需时间 none < falloc ? trunc « prealloc, falloc和trunc需要文件系统和内核支持
file-allocation=prealloc
```