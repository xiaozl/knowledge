---
# type: docs 
title: Nssm window把exe封装成服务
date: 2022-12-08T16:13:33+08:00
featured: true
draft: false
comment: false
toc: true
reward: true
pinned: false
carousel: false
series:
categories: []
tags: []
images: []
---

Window 可以使用nssm.exe 把exe文件封装成window服务

    参考：
    https://blog.csdn.net/wjw465150/article/details/125910144

<!--more-->

~~~SEHELL
 nssm.exe install `serviceName` gnb.exe -c `path` --crypto=none
~~~