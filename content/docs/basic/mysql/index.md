---
# type: docs 
title: Mysql 基本操作
linkTitle: Mysql
date: 2022-11-07T16:47:52+08:00
featured: true
draft: false
comment: false
toc: true
reward: true
pinned: false
carousel: false
series:
categories: []
tags: 
 - Mysql
images: []
---

Mysql 基本操作内容

<!--more-->
**## 1. 更新密码 ##**
--
>代码
~~~Sql
update mysql.user set authentication_string=PASSWORD('123456'), plugin='mysql_native_password' where user='root';
flush privileges;
~~~


**## 2. 压缩备份及还原 ##**
--
>mysqldump 备份并压缩sql文件

    mysql>mysqldump -h主机ip -u用户名 -p密码（也可不输入） 数据库名   | gzip > 压缩后文件位置

>mysql直接用压缩文件恢复

    mysql>gunzip < backupfile.sql.gz | mysql -u用户名 -p密码（也可不输入） 数据库名


**## 3. 更改存储位置 ##**
--
>基本操作

    1、创建目录

    mkdir -p /data/mysql

    2、停止mysql服务

    systemctl stop mysqld.service

    3、移动数据默认文件夹到新位置

    mv /var/lib/mysql　/data/mysql/

    4、修改my.cnf配置文件

    #socket=/var/lib/mysql/mysql.sock

    socket=/data/app/mysql/mysql.sock

    #datadir=/var/lib/mysql

    datadir=/data/mysql/

    5、更改新目录的文件属主

    chown -R mysql:mysql /data/mysql/mysql

    6、启动mysql服务

    systemctl start mysqld.service

> 检查目录权限

更改完datadir目录后，需要把相应权限加入到apparmor，把新的目录添加到`/etc/apparmor.d/usr.sbin.mysqld` 

    /data/mysql/ r,
    /data/mysql/** rwk,

修改完后重启apparmor服务的启动 mysql 服务

    sudo systemctl restart apparmor
    sudo systemclt start mysql


**## 4. 内存缓存配置 ##**

> 配置变量

    show variables like '%table_definition_cache%';
    show variables like '%table_open_cache%';
    show variables like 'table_cache';

> 状态查看

    show global status like 'Open%_table_definitions';show global status like 'Open%_tables';show global status like 'Open%_files';show global status like 'Table_open_cache%';

相关链接 
`https://www.cnblogs.com/zhoujinyi/archive/2012/11/29/2795079.html` 
`https://blog.csdn.net/enmotech/article/details/104681439`