---
layout: post
keywords: raspberry
description: raspbian安装kali源
title: "raspbian安装kali源及工具"
categories: [linux,rasberry]
tags: [rapberry,linux]
group: archive
icon: file-alt
---
{% include site/setup %}
 
###安装kali源以及相应工具  

    sudo vi /etc/apt/sources.list  

添加下面：  

    deb http://http.kali.org/kali kali main non-free contrib
    deb http://security.kali.org/kali-security kali/updates main contrib non-free
    deb-src http://http.kali.org/kali kali main non-free contrib
    deb-src http://security.kali.org/kali-security kali/updates main contrib non-free  

下载公钥：  

    gpg --keyserver pgp.mit.edu --recv-key 44C6513A8E4FB3D30875F758ED444FF07D8D0BF6  

导入：  

    gpg --export --armor 7D8D0BF6 | apt-key add -  

以上两步需要在sodu su以后做  

随后则可以开始`apt-get update`    

#####Metasploit

    apt-get install metasploit 
