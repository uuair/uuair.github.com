---
layout: post
keywords: tmux+powerline
description: osx10.11下使用tmux+powerline
title: "osx下使用tmux+powerline"
categories: [linux]
tags: [linux,mac]
group: archive
icon: file-alt
---
{% include site/setup %}

##Tmux的安装配置：  

**osx下安装**:  

	brew install tmux  
	
**关于tmux的说明：**  

tumx能支持的功能非常强大，类似screen的保持连接功能，分割多个窗口使用多个shell等等，太复杂的我也搞不定，貌似这个配置不太难吧。  

tmux的三个元素分别为:  

* Session 一组窗口的集合，通常用来概括同一个任务。session可以有自己的名字便于任务之间的切换。  
* Window 单个可见窗口。Windows有自己的编号，也可以认为和ITerm2中的Tab类似。  
* Pane 窗格，被划分成小块的窗口，类似于Vim中 C-w +v 后的效果。  

<img src="http://cenalulu.github.io/images/linux/tmux/concept.jpg" width="400" height="400"/>

tumx的前缀快捷键默认为`ctrl+b`，也就是说所有的快捷功能，都需要先按下`ctrl+b`，然后再按相应的键，好像翻译过来叫前置快捷键吧，英文是`<prefix>`。  

**安装powerline:**:  

安装之前有个提示，让我升级了pip，因为这玩意是python写的，所以起嘛升级python2到最新版本吧。  

	pip install --upgrade pip  
	// 升级pip  
	
	pip install --user powerline-status  
	
官方的powerline说明文档在[这里](http://powerline.readthedocs.io/en/latest/installation/osx.html)   
   

###tmux的基本操作  

`Prefix-Command`前置操作：所有下面介绍的快捷键，都必须以前置操作开始。tmux默认的前置操作是`Ctrl+b`。例如，想新建一个窗体，就需要先在键盘上按下`Ctrl+b`，松开后再按下`n`键。  

下面所有的`prefix`均代表`ctrl+b`    

**Session相关操作**  

操作              | 快捷键 
-----------------| ------
查看/切换session  | prefix s
离开Session       | prefix d
重命名当前Session  | prefix \$  

**Windows相关操作**    

操作              | 快捷键 
-----------------| ------
新建窗口          | prefix c
切换到上一个活动的窗口 | prefix space
关闭一个窗口       | prefix  \&
使用窗口号切换     | prefix 窗口号  

**Pane相关操作**  

操作              | 快捷键 
-----------------| ------
切换到下一个窗格    |  prefix o
查看所有窗格的编号  |  prefix q
垂直拆分出一个新的窗格 | prefix \"
水平拆分出一个新窗格   | prefix %
暂时把一个窗体放到最大  | prefix z    


###tmux的一些个性化定制  

做一些美化和个性配置，可以使用[gpakosz的tmux配置](https://github.com/gpakosz/.tmux)。  


	$ cd  
	$ rm -rf .tmux  
	$ git clone https://github.com/gpakosz/.tmux.git  
	$ ln -s .tmux/.tmux.conf  
	$ cp .tmux/.tmux.conf.local .    
  
安装完成以后的效果：  

<img scr="http://cenalulu.github.io/images/linux/tmux/tmux_screenshot.png" width="400" height="400" />

###为Bash配置powerline  

通过`pip show powerline-status`命令，获得powerline的安装位置，比如我的：`/Users/root/Library/Python/2.7/lib/python/site-packages/powerline/bindings/bash/powerline.sh`    

将以下配置保存到~/.bash_profile中：  

	if [ -d "$HOME/Library/Python/2.7/bin" ]; then
    PATH="$HOME/Library/Python/2.7/bin:$PATH"
	fi  
	export PATH="$HOME/.local/bin:$PATH"
	export POWERLINE_COMMAND=powerline
	export POWERLINE_CONFIG_COMMAND=powerline-config
	powerline-daemon -q
	POWERLINE_BASH_CONTINUATION=1
	POWERLINE_BASH_SELECT=1
	. /Users/root/Library/Python/2.7/lib/python/site-packages/powerline/bindings/bash/powerline.sh 

为Mac OS X的ls弄上颜色，最简单的办法是在`~/.bash_profile`中添加一行代码：`export CLICOLOR=1`  

以上配置我参考了很多网上的答案，因为我的机器默认情况下由于path问题无法正常运行，加上上面的配置就ok了，特此记录下来。   

*Teriminal字体配置*  

配置好以后在bash中中文会出现错误的符号，这时候需要安装字体：  

	git clone https://github.com/powerline/fonts.git  
	cd fonts  
	./install.sh  
	
安装完成后可以在Terminal中的字体选项看到安装的字体了`xxx for powerline`  


	 




 




    



    

    
    


