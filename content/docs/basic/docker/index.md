---
# type: docs 
title: Docker 基本操作
linkTitle: Docker
date: 2022-11-07T16:59:29+08:00
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
 - Docker
images: []
---

Docker及docker-compose打包成镜像的基本操作

<!--more-->
**## 1. 基本操作 ##**
>编译

    docker build -t srv6:1.2.1 .

>启动运行

    docker run --privileged --restart=always --name=srv6 -d -t -p 8001:80 -p 1883:1883  80574810606a

    docker run  --restart=always --name=srv6 -d -t -p 8001:80 -p 1883:1883  80574810606a

    docker run --privileged --restart=always --name=srv6 -d -t -p 8001:80 -p 1883:1883 --security-opt apparmor=unconfined  80574810606a


    docker run --privileged --restart=always --name=srv6_12 -d -t -p 8003:80 -p 1885:1883  93aa33bb04be

>gzip 压缩导出镜像

    docker save <myimage>:<tag> | gzip > <myimage>_<tag>.tar.gz
    docker save srv6:1.6.1|gzip > srv6_1.6.1.tar.gz

>导入镜像

    gunzip -c <myimage>_<tag>.tar.gz | docker load