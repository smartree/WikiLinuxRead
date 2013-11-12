Centos安装完mysql,appache这些，都不会自动启动服务，需要手动`/etc/init.d/*** start`

可以设置自动启动：
```
// show all services
chkconfig --list

// set auto on
chkconfig <service> on
chkconfig <service> off

// add in to list
chkconfig --add ...
chkconfig --del ...
```