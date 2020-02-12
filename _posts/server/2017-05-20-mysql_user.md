---
layout: post
title: mysql远程连接
---

mysql远程连接
============

mysql -u用户名 -p

show databases;
show tables;

```
CREATE USER 'username'@'host' IDENTIFIED BY 'password';
GRANT ALL ON *.* TO 'username'@'host';
```

如果连不上
（/usr/local/etc/my.cnf ）
修改my.cnf 里面 bind-address值, 127.0.0.1 改为 0.0.0.0

客户端连接caching-sha2-password问题
```
#修改加密规则 
ALTER USER 'root'@'localhost' IDENTIFIED BY 'password' PASSWORD EXPIRE NEVER; 
#更新密码
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '{NewPassword}';
```

忘记root密码
```
先暂停mysql
mysqld_safe --skip-grant-tables&mysql -u root mysql登入
use mysql;
UPDATE user SET Password = PASSWORD('newpass') WHERE user = 'root';
FLUSH PRIVILEGES;
```
