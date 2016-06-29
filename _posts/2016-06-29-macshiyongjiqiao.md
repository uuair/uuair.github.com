---
layout: post
keywords: Mac
description: Mac tips
title: "Mac使用技巧"
categories: [linux,mac]
tags: [linux,mac]
group: archive
icon: file-alt
---
{% include site/setup %}

###Mac终端命令  

重启Macos: `shutdown -r now`  
关闭MacOS:  `shutdown now`  
获取电池管理设置信息: `pmset -g`  
设置显示器无活动15分钟后关闭: `sudo pmset displaysleep 15`  
计算机无活动30分钟休眠: `sudo pmset sleep 30`  

强制Finder程序显示隐藏文件: `defaults write com.apple.finder AppleShowAllFiles TRUE`  
强制Finder程序不显示隐藏文件: `defaults write com.apple.finder AppleShowAllFiles FALSE`  

ping某个主机： `ping -o www.baidu.com`  
诊断到某个主机的路由节点: `traceroute baidu.com`  
检查主机HTTP服务或网络是否可用: `curl -I www.baidu.com |head -n 1`  
管理windows网络: `man net`  
诊断域名： `dig www.baidu.com a dig www.baidu.com MX`  
查看谁正在登录到Mac机器上: `w`  
显示系统路由表： `netstat -r`  
显示活动网络连接： `netstat -s `  
显示网络统计： `netstat -s` 

统计剪切板中文本的行数： `pbpaste |wc -l`  
统计剪切板中的单词数： `pbpaste | wc -w`  
移除剪切板中重复的文本，然后重新写回剪切版: `pbpaste | sort | unip | pbcopy`  
显示剪切版中文本的前5行： `pbpaste | head -n 5`  
显示剪切板中文本的后5行： `pbpaste | tail -n 5`  

显示终端输入历史： `history`  
将文件转成HTML，支持格式包括Text,RTF,DOC: `textutil -convert html file.extension`  
Nano是一个比vim弱的文本编辑器，但是很方便，其中ctrl+o来保存，ctrl+x为退出。  
清除终端显示内容： `clear`  

###Mac使用技巧  

`control＋command＋space` 可以输入emoji，图片字符，特殊符号（使用率较高）  
输入不认识的字的各个部分，然后按`shift＋空格`  
把鼠标移到dock栏的一个图标上,然后在magic mouse上用一个手指轻触两下，就会显示这个程序正在运行的窗口～(全屏运行和最小化的除外）  
去格式粘贴：`cmd+option+shift+v`  
显示文件信息： `MDLS+文件名`  `File+文件名`  
截屏：`shift+cmd+3` 截全屏 `shift+cmd+4` 截鼠标选择  `shift+ctrl+cmd+3` `shift+ctrl+cmd+4` 保存到剪切板中  
检查文件md5: `md5 文件名`  
看网页或者文本的时候按一下方向键，指针就消失了。按 Tab 键也能变相实现。  
“打印”选项（CMD+P）可以把网页、文本、图片等存储为 PDF 格式  
『1/4进度调整音量和亮度』按F10/F11或者F1/F2的时候同时按住CMD+Shift。  
不想用第三方下载器下载东西，那就 CMD+C 链接，在 Safari 下载窗口里CMD+V。  
Option+点击Dock上的图标，可打开此程序或文件夹所在的目录。  
想快速找到当前 Finder 窗口下的某个文件，直接键盘打它首字母即可，想更精确？快速打前几个字母，甚至是支持汉字的，用中文输入法的可以试下。  
“移到废纸篓”的快捷键是 CMD+Del ，那在“废纸篓”里“放回原处”的快捷键是什么呢？还是 CMD+Del 。  
光标在地址栏的前提下，CMD+Del 可直接清空地址栏，我之前一直用的 CMD+L ，再 Del 的。  
OS X 的第二套剪切/粘贴的快捷键』Control+K，Control+Y 。它其实是命令行快捷键，它不会改写剪切板中已经存在的内容，而且剪切走的内容只能粘贴出纯文本，不附加多余的样式。多用于 Markdown 编辑软件，比如Mou，VIM等，OS X内置的“文本编辑”和“终端”也可用这套快捷键，不支持 Pages，Word。  
『移动文件』CMD+C 复制文件，在目标目录 CMD+Option+V，就把原文件移动过来了，相当于剪切粘贴。  
不同磁盘间拖动文件，Finder 会默认复制一份过去，按住 CMD+拖动，可实现不复制直接移动。  
按住 CMD+ Option+拖到文件，可快速“制作替身”。  
按住Option+拖到文件，可快速复制一份原文件。  
在预览里选择导出格式时候，按 Option 点开会出现更多格式。  
两个同名文件夹，按住 Option 拖动才会出现“合并”选项，否则只能“替换”。  
『如何打出带声调的字母』在“美国英文”输入法下面，一直按下键盘上部分单个英文字母即可。  
Option+双击文件夹，强制本窗口打开文件夹。  
CMD+双击文件夹，强制新窗口打开文件夹。   
Mac下的反向Tab：Option+Shift+Tab。  
CMD+Tab和CMD+\`可正向反向切换后台，同时按 CMD+Q 或者 CMD+H 可配合关闭、隐藏应用程序。  
预览中按“\`”(1左边那个)可调出放大镜。   
Option+右键文件可快速更改默认打开方式。  
Photo Booth 自拍，按住Option不读秒。  
Finder的“前往”菜单里，按住 Option 才会显示用户名的资源库。  
iTunes下，按住 Option 点加号按钮是最大化，非全屏，重复操作，恢复大小。  
Control+左键点击相当于右键。  
在系统偏好设置-显示器的面板下，按住 Option 可出现“检测显示器”的选项。  
一直按着 Option+CMD 启动系统偏好设置（如果之前已经启动，请关掉再试），然后进显示器面板，会多了“旋转”选项。  
『把iMac当外界显示器』CMD+F2，进入/离开 iMac 的 Target Display 即外界显示器模式。实测 21、27均可，而不是官方宣称的只有27才支持。  
在“桌面与屏幕保护程序”面板下，可以直接把当前壁纸拖出来。  
Mac键盘没有Home、End、PgUp、PgDn等按钮，有时候要跳转到行开始或结尾一下下按很麻烦，可以使用command+左右上下方向键来实现，选取内容可以使用command+shift+左右上下方向键实现。   
command+option+v 粘贴并移动复制的内容，按住command +delete 可以删除一整行。  
optiion+F11打开声音设置，option+F1打开显示设置等等等...  
通过Command＋Tab键调出切换窗口，选中应用后不要松开Command，按Option，再松开所有键，即可将最小化的应用程序窗口也显示出来。  
只显示当前窗口，隐藏其他窗口：`command+option+H`  
在截屏的时候，按一下空格键，可以只截屏幕上的某一个窗口。  
Mac下面观看图片的时候，不能像win下面一样选择下一张图片的时候，先`command+A`选择全部的图片，再按enter键就可以一张一张观看了。  
按住Finder对话框顶部或者是Finder里任意的文件夹图标，拖动到Terminal终端命令行窗口，可以直接粘贴目录路径。  
Terminal终端命令行窗口输入 `open .`，用Finder打开当前目录。  
在终端里输入`syslog | grep -i "Wake reason"`  查看休眠时做了什么。    
查看多个文件占用的容量 `ctrl + command + i`。  
把多个文件归类到一个文件夹中：选中你想要的文件 按`control＋command＋n`  




   

  




