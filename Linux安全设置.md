##SSH

ssh设置文件是`/etc/ssh/sshd_config`，可以做ssh端口设置，限制root登录，设置RSA等提高服务器安全。

```
#限制root帐号登录
PermitRootLogin no
```

设置完后，执行`sudo service ssh restart`命令生效

##查看服务器Log

相关的Log文件都在`/var/log/`目录下。

/var/log/auth.log.1 是身份认证的日志，查看哪些IP尝试连接登录过服务器，用来查看是否有人想入侵你的服务器。

另外，安装`fail2ban`防止别人暴力破解服务器密码。
