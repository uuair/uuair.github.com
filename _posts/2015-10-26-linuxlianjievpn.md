---
layout: post
keywords: vpn,pptp,
description: linux连接vpn
title: "linux连接vpn(pptp)"
categories: [linux,rasberry,network]
tags: [rapberry,linux,vpn]
group: archive
icon: file-alt
---
{% include site/setup %}
 
环境：raspbian(基于debian)

###安装pptp客户端    
为了正常访问一些国外的源，需要使用vpn的方式。  

    sudo apt-get install pptp-linux  

    sudo pptpsetup --create myvpn --server xxx.xxx.xxx.xxx --username xx1 --password xx2 --encrypt --start  

其中encrypt是加密的意思  

/etc/ppp/peers/myvpn 保存了服务器设置  
/etc/ppp/chap-secrets 保存了用户名和密码   

修改route：  

    sudo ip route del default  
    sudo ip route add default dev ppp0  

停止vpn：  

    sudo poff myvpn  

开始vpn：  

    sudo pon myvpn  

修改route后，断开vpn，会出现无法上网的错误，这时候恢复route：  

    sudo ip route add default via 192.168.1.1  

配置自动route：  

    sudo vi /etc/ppp/ip-up.d/route-traffic

    #!/bin/bash
     /sbin/ip route add <vpn server ip> via <client gateway>
     /sbin/ip route del default
     /sbin/ip route add default dev ppp0

`chmod +x /etc/ppp/ip-up.d/route-traffic`

    sudo vi /etc/ppp/ip-down.d/disableroute

     #!/bin/bash
     /sbin/ip route add default via  <client gateway>

`chmod +x /etc/ppp/ip-down.d/disableroute`