---
layout: post  
keywords: Cnetos,shadowsocks  
description: Shadowsocks安装教程  
title: "Shadowsocks安装教程"  
categories: [Centos]  
tags: [Centos,shadowsocks,ss]  
group: archive  
icon: file-alt  
---
{% include site/setup %}  

##<center>Shadowsocks安装教程</center>

###shadowsocks需要客户端跟服务端，先说服务端：  

##CentOS:

    yum install python-setuptools  
    easy_install pip  
    pip install shadowsocks  

服务端安装好以后，创建一个配置文件`/etc/shadowsocks.json`  

    {
        "server": "0.0.0.0",  
        "server_port" : 8888,
        "local_address" : "127.0.0.1",  
        "password" : "mypassword",  
        "timeout" : 300,
        "method" : "aes-256-cfb",  
        "fast_open" : false,
        "workers" : 1,  
    }

>如果需要在后台运行，可以参考screen教程。  

运行shadowsocks:  

	ssserver -c /etc/shadowsocks.json  


Chrome推荐使用[SwitchySharp](https://chrome.google.com/webstore/detail/proxy-switchysharp/dpplabbmogkhghncfbfdeeokoefdjegm)切换代理。  
协议： socks5  
地址： 127.0.0.1  
端口： 8888  

###客户端：

####Shadowsocks for OSX:  
下载地址  
[https://sourceforge.net/projects/shadowsocksgui/](https://sourceforge.net/projects/shadowsocksgui/)  

####Shadowsocks for IOS:  
下载地址  
[https://itunes.apple.com/us/app/shadowsocks/id665729974?ls=1&mt=8](https://itunes.apple.com/us/app/shadowsocks/id665729974?ls=1&mt=8)  

####Shadowsocks for Win:  
下载地址  
[https://sourceforge.net/projects/shadowsocksgui/files/dist/](https://sourceforge.net/projects/shadowsocksgui/files/dist/)  

本文转载自[这里](https://github.com/clowwindy/shadowsocks),原文还有很多详细的介绍  



