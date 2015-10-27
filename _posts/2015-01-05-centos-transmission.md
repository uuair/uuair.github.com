---
layout: post
keywords: Cnetos,transmission
description: Centos6使用yum安装transmission
title: "Centos6使用yum安装transmission"
categories: [Centos]
tags: [Centos,transmission]
group: archive
icon: file-alt
---
{% include site/setup %}
####Centos6下使用yum安装Transmission  
背景：新购买了一台HP的microserver，其实我并非IT从业人员，也不怎么懂电脑，但是我有一台QNAP的机器，以前一直在挂PT，现如今保存了我的大量照片，所以不想在跑PT了，故购买了新的电脑。    

可是新电脑的系统我却发愁了，简单的可以用windows server2003，稍微容易一点的可以使用freenas，可我偏爱ssh方式登录而非图形界面（网速慢也是一个原因），freenas使用的是bsd的系统，包括那个jail，我真的没搞定（太小白了），所以还是使用Centos6系统吧（Centos7我也装了，但不会用，教程也少）。后面我打算把Centos6的系统学习过程都写出来，今天先记录第一笔，安装Transmission。  

`yum install transmission transmission-daemon -y`  
	//安装完成后设置settings.json  

`service transmission-daemon start`  
`service transmission-daemon stop`  
//运行过transmission后，可以生成配置文件

`#find / -name settings.json`  
	//找到settings.json的位置，例如我的位置是"/var/lib/transmission/.config/transmission/settings.json"
	
设置settings.json，主要参数如下：  

	"rpc-authentication-required": true,   
    "rpc-enabled": true,  
    "rpc-password": “password”,             
    "rpc-username": “username”,  
    "rpc-whitelist-enabled": false, 
    "umask": 18,				//这里改为0，可以控制默认下载文件权限777  
    
 如果无法连接9091端口，则需要修改防火墙：  
 `vi /etc/sysconfig/iptables`  
 增加如下：  
 `-A INPUT -m state --state NEW -m tcp -p tcp --dport 9091 -j ACCEPT`  
`-A INPUT -m state --state NEW -m tcp -p tcp --dport 51413 -j ACCEPT`   
`-A INPUT -m state --state NEW -m tcp -p tcp --dport 49153:65534 -j ACCEPT`   
随手重启防火墙：  
`service iptables restart `  

----------
>遇到的问题：  
1. `"rpc-authentication-required": true,`这里无法设置true参数，重启后总是显示false。  
查看进程得到：  
`ps -ef |grep tran`  
`501       3758     1  1 19:10 ?        00:00:02 /usr/bin/transmission-daemon -T --blocklist -g /var/lib/transmission/.config/transmission`  
进一步查询参数得到：  
` -T   --no-auth `    
`-t   --auth`    
需要修改这个参数变成`-t`  

初始化脚本的位置在：  
`/etc/init.d/transmission-daemon`  
`sudo vi /etc/init.d/transmission-daemon`  

找到如下这句：  

    DAEMON_USER="transmission"    
    DAEMON_ARGS="-T --blocklist -g $TRANSMISSION_HOME/.config/transmission"  

将这里的-T修改为-t，写入文件后再次修改settings.json就可以了。修改时需要停止transmission,修改后重新启动。  
    





    

    
