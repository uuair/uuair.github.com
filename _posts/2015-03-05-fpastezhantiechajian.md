---
layout: post
keywords: centos
description: centos
title: "fpaste粘贴插件"
categories: [centos]
tags: [centos,fpaste]
group: archive
icon: file-alt
---
{% include site/setup %}

###今天新学到一个Centos的插件fpaste，可以将shell的记录贴到网上去  

    yum install fpaste -y  
>用这个命令就可以安装了  

###使用方法  
举个例子：

    netstat -anp |fpaste  

这样会返回一个网址，记录的就是netstat -anp的信息。直接就可以发到网上啦。
      

