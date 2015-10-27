---
layout: post
keywords: raspberry
description: 通过串口访问raspbian
title: "raspberry通过串口访问"
categories: [linux,rasberry]
tags: [rapberry,linux]
group: archive
icon: file-alt
---
{% include site/setup %}
 
###raspberry通过串口访问：    

#####串线的安装方法：

串线总共有四根，分别为红、绿、白、黑，其中红色的用不到。  
黑线接地线（下图中的ground），白色的接TXD（下图中的GPIO 14），绿色接RXD（下图中的GPIO 15）。  

![](http://uuair.qiniudn.com/image/2/d2/77d5a24c7e88bbc210421da34c356.jpg)
    
此图与下图面板方向一致：  

![](http://uuair.qiniudn.com/image/a/dd/639b7755add8d59a184a423706e0e.jpg)  

#####Mac系统访问raspbian:  

######首先安装驱动：[官网地址](http://www.prolific.com.tw/US/ShowProduct.aspx?p_id=229&pcid=41)  

安装以后，可以使用`ls /dev/tty.usb*`命令查看，如果没有显示，则驱动不对或没安装，正确的应显示:  

![](http://uuair.qiniudn.com/image/f/52/5338b09c2ef55383d41304a59771f.png)  

其中tty.usbserial就是树莓派  

>以上树莓派安装串口，转载自[hyice](http://blog.163.com/hy_ice719/blog/static/876628182013234917251/)，感谢作者。  

######Mac上安装screen:  

screen是个在shell中的好东西，它可以创建一个线程的分身，好比说在vps中通过ssh连接，运行apt-get update的时候，如果通过screen创建线程，那么你就可以关闭整个界面去做其他事情而不担心断线。  

`sudo brew install screen`  

安装完毕后执行`screen /dev/tty.usbserial 115200`  
运行后按回车键，就可以看到登陆符了。  

关闭raspbian后想重新访问，需要拔下串口线后重新连接，如果有其他的连接问题，则需要kill进程：  

    ps -x |grep tty  
    kill 进程号  

