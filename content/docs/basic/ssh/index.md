---
# type: docs 
title: SSH
date: 2022-11-14T16:13:56+08:00
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
 - SSH
images: []
---

SSH 基本操作内容

<!--more-->
**## 1. SSH生成反向代理用户 ##**
--
>代码
~~~Shell
useradd -m proxyssh  #建立用户
mkdir -p /home/proxyssh/.ssh
echo 'GatewayPorts yes' >> /etc/ssh/sshd_config  #开启反向代理
echo 'Match User proxyssh' >> /etc/ssh/sshd_config  #配置proxyssh 用户
echo 'ChrootDirectory /home/limitproxyssh' >> /etc/ssh/sshd_config #只允许当前用户访问指定空目录
mkdir -p /home/limitproxyssh  #创建空目录

chown -R proxyssh:proxyssh /home/proxyssh/.ssh  #用户关联
~~~

把自动认证账号加入到authorized_keys中 ~ADD ./vrs6/ssh/authorized_keys /home/proxyssh/.ssh~

~~~Shell
ssh-rsa AAAAB3NzaC1y........+mlBuw7NL8EcZF83 proxyssh@localhost
~~~

RSA 密钥生成 百度~

RAS生成的密钥 用私钥 去访问 公钥