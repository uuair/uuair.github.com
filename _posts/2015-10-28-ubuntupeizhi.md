---
layout: post
keywords: Ubuntu
description: ubuntu14的个人配置
title: "Ubuntu设置"
categories: [linux]
tags: [linux,ubuntu]
group: archive
icon: file-alt
---
{% include site/setup %}


###Ubuntu14配置： 

**新建用户**:  

    adduser uuair
    sudo vi /etc/sudoers
    
**添加sudo权限** 

    name ALL=(ALL:ALL) ALL  

**升级系统**  

    apt-get update & apt-get upgrade  
    
**设置防火墙**    

<font color="red">whereis iptables</font>  		*#查看系统是否安装了防火墙*
  
    apt-get install iptables 		#如果没有安装  
    iptables -L 		#查看防火墙配置信息  
    
<font color="red">vi /etc/iptables.rules</font>    
添加以下内容：  

```
*filter
:INPUT DROP [0:0]
:FORWARD ACCEPT [0:0]  
:OUTPUT ACCEPT [0:0]
:syn-flood - [0:0]
-A INPUT -i lo -j ACCEPT
-A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
-A INPUT -p tcp -m state --state NEW -m tcp --dport 22 -j ACCEPT
-A INPUT -p tcp -m state --state NEW -m tcp --dport 80 -j ACCEPT
-A INPUT -p tcp -m state --state NEW -m tcp --dport 443 -j ACCEPT
-A INPUT -p icmp -m limit --limit 100/sec --limit-burst 100 -j ACCEPT
-A INPUT -p icmp -m limit --limit 1/s --limit-burst 10 -j ACCEPT
-A INPUT -p tcp -m tcp --tcp-flags FIN,SYN,RST,ACK SYN -j syn-flood
-A INPUT -j REJECT --reject-with icmp-host-prohibited
-A syn-flood -p tcp -m limit --limit 3/sec --limit-burst 6 -j RETURN
-A syn-flood -j REJECT --reject-with icmp-port-unreachable
COMMIT
```

<font color="red">iptables-restore < /etc/iptables.rules</font>   *#使防火墙规则生效*  
<font color="red">vi /etc/network/if-pre-up.d/iptables</font>    *#创建文件，添加以下内容:  

```
#!bin/bash  
iptables-restore < /etc/iptables.rules  
```  
<font color="red">chmod +x /etc/network/if-pre-up.d/iptables</font> *#添加执行权限  

`iptables -L -n`  查看规则是否生效  

**关闭icmp请求：**   
临时关闭  

    sysctl -w net.ipv4.icmp_echo_ignore_all=1
    sysctl -p  
    
临时开启：  
    
    sysctl -w net.ipv4.icmp_echo_ignore_all=0
    sysctl -p  
    
永久保留：  
<font color="red">vi /etc/sysctl.conf</font>  

    net.ipv4.icmp_echo_ignore_all=1  
    
**安装shadowsocks**  

    apt-get install python-setuptools && easy_install pip
    pip install shadowsocks  
    vi /etc/shadowsocks.json
    
创建以下文件内容：  

```
{ 
"server":"101.102.103.104",   
"server_port":3288,   
"local_address": "101.102.103.104",   
"local_port":3289,   
"password":"fuckthegfw",   
"timeout":600,   
"method":"aes-256-cfb",   
"fast_open": false,   
"pid-file":"/var/run/shadowsocks_s.pid"   
}
```    

后台运行命令：  

`ssserver -c -d /etc/shadowsocks.json start`   *#运行* 
`ssserver -c -d /etc/shadowsocks.json stop`    *#停止*  

开机启动:  

`vi /etc/init.d/shadowsocks`  

输入以下内容:   
   

```  
#!/bin/sh

start(){
       ssserver -c /etc/shadowsocks.json -d start
}

stop(){
        ssserver -c /etc/shadowsocks.json -d stop
}

case "$1" in  
start)  
        start   
        ;;  
stop)  
        stop  
        ;;  
reload)  
        stop  
        start  
        ;;  
*)  
        echo "Usage: $0 {start|reload|stop}"  
        exit 1  
        ;;  
esac    
```

给执行权限  
`chmod +x /etc/init.d/shadowsocks`  
`update-rc.d shadowsocks defaults`  

这样在shell中可以直接运行`sudo service shadowsocks {start|reload|stop}来控制了  

----没成功  

**搭建ghost博客**  

    wget http://dl.ghostchina.com/Ghost-0.7.0-zh-full.zip    
    unzip -uo Ghost-0.7.0-zh-full.zip -d ghost
    sudo apt-get crul -y  
    curl -sL https://deb.nodesource.com/setup_0.12 | sudo -E bash -   
    sudo apt-get install nodejs -y  
    cd ghost  
    npm install --production  
    
上面一系列的命令，安装了nodejs以及ghost。  

    sudo npm install forever -g  

通过forever让ghost在后台一直运行，其中forever的控制命令有：  

    NODE_ENV=production forever start index.js  
    forever stop index.js  
    forver list  
    
然后通过nginx发布网站：  

    sudo apt-get install nginx -y  

*以下的配置跟centos不同*  
配置nginx:  

    sudo vi /etc/nginx/sites-available/ghost.conf  
    
```
server {
    listen 80;
    server_name example.com;

    location / {
        proxy_set_header   X-Real-IP $remote_addr;
        proxy_set_header   Host      $http_host;
        proxy_pass         http://127.0.0.1:2368;
```  

修改`server-name`为自己的域名  

软连接到sites-enabled目录下：  

    sudo ln -s /etc/nginx/sites-available/ghost.conf /etc/nginx/sites-enabled/ghost.conf  
    sudo service nginx restart  
    
安装mysql  

    sudo apt-get install mysql-server mysql-client  
    sudo mysql_secure_installation  
    mysql -uroot -p -e 'create database ghost;'   
    
    



    

    
    


