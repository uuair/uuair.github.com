---
layout: post
keywords: raspbian
description: raspbian设置
title: "raspbian设置"
categories: [linux,raspberry]
tags: [rapbian,raspberry]
group: archive
icon: file-alt
---
{% include site/setup %}

新入手一个树莓派2，准备上kali……  

安装系统：  

    diskutil list
    diskutil umount /dev/disk2s1    
    sudo dd bs=2m if=kali-2.0.1-rpi2.img of=/dev/disk2    

(CTRL+T)可以查看dd的过程，MAC下使用control+T  

我的系统是osx，所以通过以上四步，可以把kali安装到sd卡里面。  

###rpi的默认账号：  

    pi/raspberry  

###添加用户：  

    adduser name   

#####给予sudo权限:    

    sudo vi /etc/soduers

添加 
    
    name ALL=(ALL:ALL) ALL  
    sudo reboot  

###升级系统：  

    apt-get update & apt-get upgrade   

###安装字体：  

    dpkg-reconfigure locales  

选择字符编码：en\_US.UTF-8、zh\_CN.GBK、zh\_CN.UTF-8    
选择字符：zh\_CN.UTF-8     
设置完后reboot    

###修复vi方向键变英文:  

先删除系统自带的tiny版的vim：  

    sudo apt-get remove vim-common     

重新安装：  

    sudo apt-get install vim  