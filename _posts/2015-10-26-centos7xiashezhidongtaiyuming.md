---
layout: post
keywords: 动态域名,ddns
description: linux下设置3322动态域名
title: "Centos7下设置动态域名"
categories: [linux]
tags: [ddns,linux,centos,network]
group: archive
icon: file-alt
---
{% include site/setup %}

我使用了3322.org的动态域名(ddns)服务，在centos7上的设置方法如下：  

首先安装需要的软件：

    yum install lynx vixie-cron crontabs -y

lynv是一个在shell中的浏览器，vixie-cron是cron的主程序,crontabs是用来安装、卸载、列举驱动cron守护进程表格的程序。
cron程序可能在linux中已经内置了，这是一个定时程序，可以定时执行任务。  

在3322的官网上的说明：linux下更新动态域名的方法为：  

    lynx -mime_header -auth=用户名:密码 “http://members.3322.net/dyndns/update?system=dyndns&hostname=域名”

安装完上述程序后可以测试一下：  

    lynx -mime_header -auth=用户名:密码 "http://members.3322.net/dyndns/update?system=dyndns&hostname=域名"

其中用户名、密码、域名这里输入自己的，如果没问题，则会提示更新成功。  

接下来设置cron：  

    systemctl start/stop/restart crond.service  
//这是启动、停止、重启命令   

    systemctl enable crond.service  
//加入到开机启动中  
 
或者执行命令`:ntsysv`，加入开机启动  

crontab命令：  

-e 编辑该用户的计时器设置   
-l 列出该用户的计时器设置   
-r 删除该用户的计时器设置   
-u<用户名称> 指定要设定计时器的用户名称  

例如5分钟更新一次动态域名检测，命令为：

    #crontab -e

在打开的窗口中输入：(vi格式，输入i后输入，输入结束按esc后输入”:wq”推出)

    */5 * * * * lynx -mime_header -auth=用户名:密码 "http://www.3322.org/dyndns/update?system=dyndns&hostname=域名" &

使用crontab -l可以查看。

设置crontab后，系统会每5分钟进行一次提示，使用的是sendmail的方法，关闭提示的方法为:

    echo "unset MAILCHECK" >> /etc/profile 
    source /etc/profile

下面列出crontab的格式：

基本格式 :  
* *　 *　 *　 *　　command  
分　时　日　月　周　 命令

第1列表示分钟1～59 每分钟用*或者 */1表示  
第2列表示小时1～23（0表示0点）  
第3列表示日期1～31  
第4列表示月份1～1  
第5列标识号星期0～6（0表示星期天）  
第6列要运行的命令  

例子：

    30 21 * * * /usr/local/etc/rc.d/lighttpd restart

上面的例子表示每晚21:30重启apache

    45 4 1,10,22 * * /usr/local/etc/rc.d/lighttpd restart

上面的例子表示每月1、10、22日的4 : 45重启apache。

    10 1 * * 6,0 /usr/local/etc/rc.d/lighttpd restart

上面的例子表示每周六、周日的1 : 10重启apache。

    0,30 18-23 * * * /usr/local/etc/rc.d/lighttpd restart

上面的例子表示在每天18 : 00至23 : 00之间每隔30分钟重启apache。

    0 23 * * 6 /usr/local/etc/rc.d/lighttpd restart

上面的例子表示每星期六的11 : 00 pm重启apache。

    * */1 * * * /usr/local/etc/rc.d/lighttpd restart

每一小时重启apache

    * 23-7/1 * * * /usr/local/etc/rc.d/lighttpd restart

晚上11点到早上7点之间，每隔一小时重启apache

关闭因为使用crontab而产生的mail

    crontab -e
    在最上面输入 MAILTO=""

清空mail

    cd /var/spool/mail
    echo '' >root