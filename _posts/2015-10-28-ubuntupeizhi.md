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


###Ubuntu14/15配置： 

**新建用户**:  

    adduser uuair
    sudo vi /etc/sudoers
    
**添加sudo权限** 

    name ALL=(ALL:ALL) ALL  

**升级系统**  

    apt-get update & apt-get upgrade  
    
**设置ssh**  
ssh需要设置两方面，修改默认端口以及keys登陆方式：  

    vi /etc/ssh/sshd_config  
    
*修改一下几个地方：*  

    Port 22  #这里可以修改成任意端口号  
    PermitRootLogin yes 改为no  #禁止root登录  
    
*ssh服务命令:*  

    sudo /etc/init.d/ssh stop  
    sudo /etc/init.d/ssh start  
    sudo /etc/init.d/ssh restart  
    
*设置证书登录:*     
在服务器上执行：  

    ssh-keygen  
    
一路回车后来到客户机上执行：  

    cd ~/.ssh  
    scp id_rsa.pub name@xxx.xxx.xxx.xx~/.ssh/id_rsa.pub1  
    cat id_rsa.pub1 >> authorized_keys  
    chmod 700 authorized_keys  
    
后面再登录，就可以不用输入密码了。如果禁止密码登录，则修改`/etc/ssh/sshd_config`这里的：  

    PasswordAuthentication 更改为no  
最后重启ssh。


    
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

`ssserver -c /etc/shadowsocks.json -d start`   #运行   
`ssserver -c /etc/shadowsocks.json -d stop`    #停止      

或者直接运行：  

`ssserver -c /etc/shadowsocks.json`  

设置开机启动：  

    whereis ssserver  
    
我的显示文件在`/usr/local/bin/ssserver`这里，编辑`/etc/rc.local`文件  

    sudo vi /etc/rc.local   #编辑rc.local文件  
    # 在exit前面加入下面一行  
    # /usr/local/bin/ssserver -c /etc/shadowsocks.json -d start  
    
保存重启搞定！

**搭建ghost博客**  

    wget http://dl.ghostchina.com/Ghost-0.7.0-zh-full.zip    
    unzip -uo Ghost-0.7.0-zh-full.zip -d ghost
    sudo apt-get install curl -y  
    curl -sL https://deb.nodesource.com/setup_0.12 | sudo -E bash -   
    sudo apt-get install nodejs -y 
    sudo apt-get install nodejs-legacy #如果出现path问题，比如/usr/bin/env找不到，就安装这个 
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
    
    server {
        listen 80;
        server_name example.com;

    location / {
        proxy_set_header   X-Real-IP $remote_addr;
        proxy_set_header   Host      $http_host;
        proxy_pass         http://127.0.0.1:2368;


修改`server-name`为自己的域名  

软连接到sites-enabled目录下：  

    sudo ln -s /etc/nginx/sites-available/ghost.conf /etc/nginx/sites-enabled/ghost.conf  
    sudo service nginx restart  
    sudo systemctl enable nginx.service #ubuntu15
    sudo systemctl restart nginx.service #ubuntu15
    
安装mysql  

    sudo apt-get install mysql-server mysql-client  
    sudo mysql_secure_installation  
    mysql -uroot -p -e 'create database ghost;'   
    
**安装pptp**  

    sudo apt-get update  
    sudo apt-get install pptp   
    
 *编辑pptp.conf文件*  
 
     sudo vi /etc/pptpd.conf  
     
 *在当前文件写入以下配置:*  
 
     option /etc/ppp/options.pptpd
     logwtmp
     localip 192.168.2.1
     remoteip 192.168.2.10-100
     END
 
 **注：如果出现vpn连接错误`Plugin /usr/lib/pptpd/pptpd-logwtmp.so is for pppd version 2.4.5, this is 2.4.6`，可以注释掉`logwtmp`参数，就可以解决。**  
 **注2:如果无法访问网络，还可以尝试将`localip`这里的参数，写上外网的参数**   
 
 *编辑pptpd-option文件*  
 
```
name pptpd
refuse-pap
refuse-chap
refuse-mschap
require-mschap-v2
require-mppe-128
ms-dns 8.8.8.8
ms-dns 8.8.4.4
proxyarp
lock
nobsdcomp 
novj
novjccomp
nologfd
END
```  

*增加路由转发*  

    vi /etc/sysctl.conf  
    #添加如下参数：  
    net.ipv4.ip_forward=1  
    #退出保存后立即生效  
    sysctl -p  
    
*修改iptables NAT转发：*  

    iptables -t nat -A POSTROUTING -s 192.168.2.0/24 -o eth0 -j MASQUERADE  
    
*设置MTU*:  

    iptables -I FORWARD -s 192.168.2.0/24 -p tcp --syn -i ppp+ -j TCPMSS --set-mss 1300  
    
*保存iptables的设置：*
   
    iptables-save > /etc/iptables/iptables.rules 

*iptables设置开机加载到网卡配置中*        
    
    vi /etc/network/interfaces    
    pre-up iptables-restore < /etc/iptables.rules   
    
*增加vpn用户名*  

    vi /etc/ppp/chap-secrets  
    
    test * password *  
    
中间用tab隔开，test是用户名，password是密码，中间两个*号。  

    systemctl restart pptpd  
    
**设置完毕**  



    

    
    


