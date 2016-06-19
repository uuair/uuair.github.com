---
layout: post  
keywords: DNS  
description: 关于域名劫持  
title: "查看114.114.114.114是否被劫持"  
categories: [Centos]  
tags: [Centos,DNS]  
group: archive  
icon: file-alt  
---
{% include site/setup %}  

##<center>查看114.114.114.114是否被劫持</center>

运行这个命令：  

`nslookup whether.114.dns.com 114.114.114.114`  

如果返回的是127.0.0.1，则说明你的网络DNS劫持，你的运营商劫持了114DNS的请求。  
目前114.114.115.115还没有被劫持（北京宽带通）。  

    nslookup whether.114dns.com 114.114.115.115
    Server:		114.114.114.114
    Address:	114.114.114.114#53

    Non-authoritative answer:
    Name:	whether.114dns.com
    Address: 127.0.0.1

    nslookup whether.114dns.com 114.114.115.115
    Server:		114.114.115.115
    Address:	114.114.115.115#53

    Non-authoritative answer:
    Name:	whether.114dns.com
    Address: 60.215.138.225

