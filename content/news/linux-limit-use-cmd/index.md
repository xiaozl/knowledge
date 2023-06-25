---
# type: docs 
title: linux 限制特定用户使用命令做法
date: 2022-11-09T14:57:37+08:00
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
 - linux
images: []
---

在linux中，如果要对特定用户只允许使用 特定的命令行参数时进行的做法

<!--more-->
1. 创建用户
   
    adduser superman

2. 用户启动脚本中嵌入限制脚本
    
    把`init.sh`脚本嵌入到`~/.bashrc`中 
    比如：`. /home/superman/init.sh`

3. 账号登录
    
    当superman账号登录linux系统时，会提示用户选择相应操作。

> `init.sh` 脚本账号demo

```shell
#!/bin/bash

trap 'onCtrlC' INT
function onCtrlC () {
    echo 'Ctrl+C is captured'
}

cfirst=1
while :
do
	#c=getchar();
	#if(c==EOF)
	#	exit(0);

    if [ $cfirst -eq 1 ];then
    	python /opt/script/help.py
    fi
    cfirst=0
    read -p"请输入：" name
    case $name in
        "help")
	    python /opt/script/help.py
		;;
        "showip")
           ip addr
            ;;
        "telnet")
	    python /opt/script/telnet.py
            ;;
	 "logout")
		logout
		 ;;
	 "exit")
		exit
		 ;;
        *)
            echo "输入错误，请重新输入"
    esac
done
```

