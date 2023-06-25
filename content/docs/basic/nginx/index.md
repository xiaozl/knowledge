---
# type: docs 
title: Nginx 基本操作
linkTitle: Nginx
date: 2022-11-23T16:04:27+08:00
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

Nginx 基本操作内容

<!--more-->

**## 1. 配置后端https反向代理 ##**
--
>代码
~~~Shell
        location /test {
            expires off;
            proxy_redirect     off;
            proxy_set_header   Host             "globe.adsbexchange.com";
            proxy_set_header   X-Forwarded-For  $proxy_add_x_forwarded_for;
            #add_header  Nginx-Cache "$upstream_cache_status";

            proxy_pass https://globe.adsbexchange.com/re-api/?binCraft&zstd&box=-90,90,-180,180;
            proxy_set_header referer "https://globe.adsbexchange.com/?zoom=2&lat=0&lon=0";
            proxy_set_header user-agent "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36";
            proxy_ssl_session_reuse off;
            proxy_ssl_server_name on;
            proxy_ssl_name "globe.adsbexchange.com";
            proxy_ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
            proxy_set_header X-Real-IP $remote_addr;
        }

~~~
