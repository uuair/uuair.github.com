---
layout: post
keywords: Finder
description: Mac Finder变英文
title: "Mac Finder变英文的解决办法"
categories: [System]
tags: [Mac,System]
group: archive
icon: file-alt
---
{% include site/setup %}

###桌面变英文:

`touch ~/Desktop/.localized`  
`chmod 600 ~/Desktop/.localized`

应用程序变英文：

显示隐藏文件：

`defaults write com.apple.finder AppleShowAllFiles -bool true  //显示隐藏`  

>复制.localized到Applications文件夹里  

`defaults write com.apple.finder AppleShowAllFiles -bool false //恢复隐藏`


    

