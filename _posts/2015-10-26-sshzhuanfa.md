---
layout: post
keywords: ssh
description: ssh转发、隧道
title: "SSH转发设置"
categories: [linux]
tags: [ssh,centos,it,linux,network]
group: archive
icon: file-alt
---
{% include site/setup %}

##ssh隧道记录

一直头疼的问题就是我一直处在一个大局域网里，有一个伪公网ip，所以从外面一直无法访问自己。  

尝试过ngrok服务，最大的问题还是安全，因为要在ngrok.com上开一个端口，还经常断，自己建服务器需要ssl，咱也没钱买啊，所以看上了ssh隧道转发，特此记录。

先说说原理，一共三种转发方法：

- 动态端口转发（Socks代理)

- 本地端口转发

- 远端端口转发

假设a为内网机器，b为外网机器，c为在外网使用的计算机，三者都有ssh服务，a可以访问b，b跟c可以互相访问。

###动态端口转发

动态端口转发会配置本地端口，将此端口的所有数据转发到远端地址上，并通过Socks协议与本地端口通讯，此时ssh充当Socks代理服务器的角色。在a主机上执行：

    ssh -D localhost:8080 b'sip

这样在主机a上，可以通过

    SOCKS5 localhost:8080

访问外网服务，或者是在浏览器的代理服务器上的socks5里面，写上127.0.0.1，端口8080，然后就可以翻墙了。

###本地端口转发

内网a无法访问外网c，可以通过b进行跳转，将c的端口映射到a自己机器上。在a上执行：

a将要访问c的5900的vnc端口

    ssh -L 5901:*:5900 b'sip

然后在a上，可以通过下面的命令，连接c的5900端口：

    open vnc://localhost:5901

本地端口转发实现了内网无法访问外网某一电脑，通过可以连接的另一台外网电脑实现转发的功能。

###远端端口转发

外网c无法访问内网a，外网b也无法访问内网a，但是内网a可以访问b，所以通过转发端口，使得c访问b的某一端口，来实现访问a的功能，也就是将a的端口，映射到b上，然后c访问b来解决。在a上执行：

c将要访问a的5900端口，在b上开一个5901的端口做转发

    ssh -R 5901:*:5900 b'sip

然后c通过连接b的5901，访问a的5900端口：

    open vnc://b’ip:5901

ip地址中*是代表绑定的ip，可以是127.0.0.1，也可以是localhost，*则代表了谁都可以访问，不绑定地址。

>以上说明参考了http://codelife.me/blog/2012/12/09/three-types-of-ssh-turneling，感谢作者。

接下来研究持续的ssh隧道建立

因为ssh是无法持续连接的，比如网络故障或者时间长了会断，所以需要autossh来保持持续连接。

    yum install autossh -y

替换ssh的命令：

    autossh -M 5678 -NR 5901:*:5900 b'sip

> autossh部分参考http://www.cnblogs.com/eshizhan/archive/2012/07/16/2592902.html，感谢作者。

补充内容：

1 我需要转发多个ssh端口，这样的命令是：

        autossh -M 5678 -NR 5901:*:5900 -NR 5903:*:5902 b'sip

以上命令是转发本机的5900到5901端口，5902到5903端口。访问c的5901跟5903就可以了。  

2 如果远程计算机c的端口不是22，那么需要加上-p参数：(9999为端口号）  

    autossh -M 5678 -NR 5901:*:5900 -NR 5903:*:5902 b'sip -p 9999