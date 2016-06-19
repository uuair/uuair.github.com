---
layout: post
keywords: Centos,ssh
description: ssh安全
title: "centos下的ssh安全"
categories: [shadowsocks]
tags: [centos,ssh,安全]
group: archive
icon: file-alt
---
{% include site/setup %}

闲来无事，查看了一下centos的日志，尼玛，一堆尝试ssh登陆的信息，哎，真是无聊啊。开始改吧。  

*查看日志*  

    $ cd /var/log  
    $ less secure  

>可以配合grep参数显示要显示的内容  

*禁止root登陆ssh*  

    $ vi /etc/ssh/sshd_config  

PermitRootLogin no //修改为此值  
PermitEmptyPasswords no //禁止空密码登录  

*修改ssh端口*  

    Prot 3333
 

*修改防火墙*  

    $ vi /etc/sysconfig/iptables  

*修改登录错误的时间*    

    $ vi /etc/pam.d/login  

在PAM-1.0下面添加：  
>auth required pam_tally2.so deny=5 unlock_time=1800  
//登录错误5次锁定1800秒
