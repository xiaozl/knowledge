---
# type: docs 
title: 使用浏览器远程云端桌面方案
date: 2022-11-15T15:08:58+08:00
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
 - Nginx
images: []
---

在云服务虚拟化过程中，对外提供云服务时，可以动态创建云虚拟机服务，

用户可以通过浏览器登录到远端桌面上，linux桌面及window桌面都可以，

把服务软件装在云端，用户登录到云端即可使用。

整个链路流程可以如下

    用户浏览器-->Nginx-->websockify-->spice

>用户浏览器
    
需要使用版本比较高的浏览器，最好是用高版本chrome

>Nginx

Nginx 做为高效的前置代理服务，主要是websocket代理
参考`https://datawookie.dev/blog/2021/08/websockify-novnc-behind-an-nginx-proxy/`

>websockify

Websockify是一个WebSocket到TCP代理或桥。这允许浏览器连接到任何应用程序/服务器/服务。

可以把前置的websocket 协议转换到后端的spice 协议 参考`https://github.com/novnc/websockify`


>spice

远程桌面协议

参考 `https://www.spice-space.org/spice-html5.html` `https://github.com/eyeos/spice-web-client` `https://github.com/freedesktop/spice-html5`


相关联的内容

    video 里面的内容进行操作，playsinline
    Qemu-ga
    red hat
    spice agent 远程桌面访问
    virtio-win
    open stack   

可应用到培训行业，把软件装到云服务器中，学员可通过浏览器远程到云桌面进行操作，后台可以查看用户操作情况。