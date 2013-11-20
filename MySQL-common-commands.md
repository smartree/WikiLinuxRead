```
// see user information.
sql> use mysql;
sql> select user, name from user;
```

```
// grant remote privileges
sql> grant all privileges on *.* to 'loginName'@'192.168.10.131' identified by ‘password’;

// flush sql
sql> flush privileges;
```

##MySQL dump

```
$ mysqldump -u <username> -p <password> --opt database > backup.sql
$ mysqld -u <username> -p <password> <database_name> < backup.sql
```