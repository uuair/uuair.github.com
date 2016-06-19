---
layout: post
keywords: Cnetos,samba
description: Centos6安装samba共享
title: "Centos6安装samba并共享"
categories: [Centos]
tags: [Centos,samba,共享]
group: archive
icon: file-alt
---
{% include site/setup %}

####Centos6.6下安装samba，实现共享。这个教程是我综合了网上n多文章来的，应该是很全很全了，因为大部分教程，都有缺陷，对照着做，不一定可以访问共享。

1.关闭SELinux:  

`vi /etc/selinux/config`  
`SELINUX=enforcing`    //注释掉    
`SELINUXTYPE=targeted`    //注释掉  
`SELINUX=disabled`    //增加这句  
`:wq`  
`shutdown -r now`    //重启系统  
通过以上步骤，关闭了SELinux，虽然不关闭也可以实现samba的访问，但设置起来比较麻烦。  

2.下载samba:  
`yum install samba samba-client samba-swat -y`    

3.设置samba:  
`sudo service smb start/stop`   //利用此命令启动/关闭samba  
`sudo service smb status`    //查案服务启动情况  
`sudo chkconfig --level 35 smb on`    //在3、5级别上自动运行samba服务  
`sudo vi /etc/samba/smb.conf`    //配置samba服务的文件  
samba的配置文件分为Global Settings和Share Definitions两部分。  

*Global Settings*    
`workgroup = WORKGROUP`    //一般windows设置的工作组名就是workgroup  
`server string = Samba Server Version %v` //可以不修改，显示Samba版本号  
`netbios name = smbserver`  //NetBIOS的名称.  
`security = user`
//Samba的验证方式，一共有四种:  
a.share:用户访问Samba不需要提供用户名和口令  
b.user:Samba共享目录只能被授权的用户访问，账号和密码在Samba中建立  
c.server: 依靠其他Windows NT/2000或Samba来验证账号密码，是一种代理验证。此种安全模式下，系统管理员可以把所有的Windows用户和口令集中到一个NT系统上，使用Windows NT进行Samba认证  
d.domain:域安全级别，使用主域控制器(PDC)来完成认证  
`passdb backend = tdbsam`  
//用户后台，目前有三种：smbpasswd、tdbsam和ldapsam。  
a.smbpasswd：该方式是使用smb自己的工具smbpasswd来给系统用户设置一个Samba密码，客户端使用这个密码访问Samba的资源。默认文件在/etc/samba目录下，如果没有则需要手工建立。  
b.tdbsam:该方式使用一个数据库文件建立用户数据库，数据库文件叫passdb.tdb，默认在/etc/samba目录下，可以使用pdbedit命令建立Samba账户，不过Samba用户必须是系统用户。pdbedit的主要命令有：  

    pdbedit -a username: 新建Samba账户  
    pdbedit -x username: 删除Samba账户  
    pdbedit -L: 列出Samba用户列表,读取passdb.tdb数据库文件  
    pdbedit -Lv: 列出Samba用户列表的详细信息  
    pdbedit -c "[D]" -u username: 暂停该Samba用户的账号  
    pdbedit -c "[]" -u username: 恢复该Samba用户的账号  

c.ldapsam:该方式是基于LDAP的账户管理方式验证，过程略。  

*Share Definitions*  
[共享名]  
comment =  任意字符串  //对该共享的描述  
path = 共享目录路径  
//path用来指定共享目录的路径。可以用%u、%m这样的宏来代替路径里的unix用户和客户机的Netbios名。  
browseable = yes/no //该共享是否可以浏览  
writable = yes/no //该共享是否可写  
available = yes/no //该共享是否可用  
admin users = 该共享的管理者  
//admin users用来指定该共享的管理员（对该共享具有完全控制权限）。在Samba3.0中，如果用户验证方式设置成“security=share”时，此项无效。  
例如: admin users = david, sandy（多个用户中间用逗号隔开）  
valid users = 允许访问该共享的用户  
//valid users用来指定允许访问该共享资源的用户  
例如：valid users = david, @dave, @tech（多个用户或组中间用逗号隔开，如果要加入一个组就用“@组名”表示）  
invalid users = 禁止访问该共享的用户  
//invalid users用来指定不允许访问该共享的用户  
例如：invalid users = root, @bob（多个用户或组中间用逗号隔开）
write list = 允许写入该共享的用户  
//write list = david, @dave  
public = yes/no  //是否允许guest账户访问  
guest ok = yes/no //同“public”  

Samba安装好后，使用testparm命令可以测试smb.conf配置是否正确，使用testparm -v命令可以详细列出配置  

----------------
我自己的例子：  
共享一个叫movie的盘，给一个movie组的ffaa用户，该目录只能是ffaa和movie组浏览：  
a.添加ffaa用户  
`groupadd movie`  
`useradd -g movie ffaa`  
`passwd ffaa`  
//建立用户的同时加入到相应的组中的方式：useradd -g 组名 用户名  

b.在根目录下建立/movie文件夹  
`cd /`  
`mkdir movie`  

c.将刚才建立的账户添加到Samba中：  
`pdbedit -a ffaa`  //输入两边密码后建立成功  

d.修改主配置文件如下:

    [global]
    workgroup = WORKGROUP  
    server string = David Samba Server Version %v  
    netbios name = DavidSamba  
    log file = /var/log/samba/log.%m  
    security = user  //用户级别，由Samba检查账户密码  
    ===Share Definitions==  
    [homes]                                 //设置用户宿主目录
    comment = Home Directories
    browseable = no
    writable = yes
    ;    valid users = %S
    ;    valid users = MYDOMAIN\%S  
    [public]
    comment = Public Stuff
    path = /share
    public = yes  
    [movie]									//movie组目录，只允许movie组成员访问
    comment = movie
    path = /movie
    valid users = @movie  
    
4.设置完服务器后，重新启动smb服务：  
`sudo service smb restart`    
如果跟我一样，还是无法访问smb服务，则需要修改防火墙（并非关闭）  
`sudo vi /etc/sysconfig/iptables`  
增加如下内容：  
    
    -A INPUT -m state --state NEW -m tcp -p tcp --dport 139 -j ACCEPT
    -A INPUT -m state --state NEW -m tcp -p tcp --dport 445 -j ACCEPT
    -A INPUT -m state --state NEW -m udp -p udp --dport 137 -j ACCEPT
    -A INPUT -m state --state NEW -m udp -p udp --dport 138 -j ACCEPT
    
`sudo service iptables restart`  重启防火墙后生效。  