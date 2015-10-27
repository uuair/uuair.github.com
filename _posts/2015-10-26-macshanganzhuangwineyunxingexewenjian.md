---
layout: post
keywords: wine,Mac
description: Mac下运行exe文件
title: "在Mac上安装wine运行exe文件"
categories: [Mac]
tags: [Mac,linux,windows]
group: archive
icon: file-alt
---
{% include site/setup %}

环境:

*Yosemite 10.10*  
*Terminal*  

一、用于安装homebrew

- 打开Terminal.app;

- 输入：  

        ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

- 回车键执行…

二、homebrew自检

- 输入：  

        brew doctor

- 回车键执行…

三、使用homebrew安装wine

- 输入：  

        brew install wine

- 回车键执行…

四、安装缺失组件

- 浏览器访问[https://xquartz.macosforge.org/landing]()

- 下载安装Xquartz

五、重试：使用homebrew安装wine  

- 输入：  

        brew install wine

- 回车键执行…

六、检查wine安装状态  

    wine --version

使用wine打开exe程序  

    wine filename.exe