---
layout: post
keywords: tmux+powerline
description: osx10.11下使用tmux+powerline
title: "osx下使用tmux+powerline（二）"
categories: [linux]
tags: [linux,mac]
group: archive
icon: file-alt
---
{% include site/setup %}

###tmux的一些个性化定制  

做一些美化和个性配置，可以使用[gpakosz的tmux配置](https://github.com/gpakosz/.tmux)。  

```bash
	$ cd  
	$ rm -rf .tmux  
	$ git clone https://github.com/gpakosz/.tmux.git  
	$ ln -s .tmux/.tmux.conf  
	$ cp .tmux/.tmux.conf.local .    
```
  
安装完成以后的效果：  

<img src="http://cenalulu.github.io/images/linux/tmux/tmux_screenshot.png" width="400" height="400" />  

关于这个配置文件改变的东西：  

```bash
	bind -r h select-pane -L  # move left
	bind -r j select-pane -D  # move down
	bind -r k select-pane -U  # move up
	bind -r l select-pane -R  # move right
	//窗口的左下上右绑定为hjkl  
	
	bind -r H resize-pane -L 2
	bind -r J resize-pane -D 2
	bind -r K resize-pane -U 2
	bind -r L resize-pane -R 2
	//窗口的移动左下上右绑定为大写的HJKL
```
###为Bash配置powerline  

通过`pip show powerline-status`命令，获得powerline的安装位置，比如我的：`/Users/root/Library/Python/2.7/lib/python/site-packages/powerline/bindings/bash/powerline.sh`    

将以下配置保存到~/.bash_profile中：  

```bash
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
```

为Mac OS X的ls弄上颜色，最简单的办法是在`~/.bash_profile`中添加一行代码：`export CLICOLOR=1`  

以上配置我参考了很多网上的答案，因为我的机器默认情况下由于path问题无法正常运行，加上上面的配置就ok了，特此记录下来。   

*Teriminal字体配置*  

配置好以后在bash中中文会出现错误的符号，这时候需要安装字体：  

```bash
	git clone https://github.com/powerline/fonts.git  
	cd fonts  
	./install.sh  
```
	
安装完成后可以在Terminal中的字体选项看到安装的字体了`xxx for powerline`  

###tmux基本配置  

**tmux动态载入配置**  

编辑根目录的 .tmux.conf文件，添加：  

	bind r source-file ~/.tmux.conf \; display-message "Config reloaded"  
	//绑定prefix r为刷新tmux配置  
	
**鼠标切换窗格** (暂时没成功） 

```
setw -g mode-mouse on
set -g mouse-select-pane on
set -g mouse-resize-pane on
set -g mouse-select-window on
```

###常用

tmux     | 开启tmux
-------- | -------
tmux ls  | 列出会话 (tmux list-session)
tmux attach | Tmux重新连接之前的窗口可使用
tmux attach -t session | 进入某个会话
tmux -r   | 连接上次断开的session
tmux kill-session | 关闭上次tmux打开的窗口
tmux kill-server  | 关闭所有tmux打开的窗口  

###tmux常用配置说明：  

vi .tmux.conf  

```bash
#此类配置可以在命令行模式中输入show-options -g查询
set-option -g base-index 1                        #窗口的初始序号；默认为0，这里设置为1
set-option -g display-time 5000                   #提示信息的持续时间；设置足够的时间以避免看不清提示，单位为毫秒
set-option -g repeat-time 1000                    #控制台激活后的持续时间；设置合适的时间以避免每次操作都要先激活控制台，单位为毫秒
set-option -g status-keys vi                      #操作状态栏时的默认键盘布局；可以设置为vi或emacs
set-option -g status-right "#(date +%H:%M' ')"    #状态栏右方的内容；这里的设置将得到类似23:59的显示
set-option -g status-right-length 10              #状态栏右方的内容长度；建议把更多的空间留给状态栏左方（用于列出当前窗口）
set-option -g status-utf8 on                      开启状态栏的UTF-8支持
 
#此类设置可以在命令行模式中输入show-window-options -g查询
set-window-option -g mode-keys vi    #复制模式中的默认键盘布局；可以设置为vi或emacs
set-window-option -g utf8 on         #开启窗口的UTF-8支持
 
#将激活控制台的快捷键由Ctrl+b修改为Ctrl+a
set-option -g prefix C-a
unbind-key C-b
bind-key C-a send-prefix
 
#添加自定义快捷键
bind-key z kill-session                     #按z结束当前会话；相当于进入命令行模式后输入kill-session
bind-key h select-layout even-horizontal    #按h将当前面板布局切换为even-horizontal；相当于进入命令行模式后输入select-layout even-horizontal
bind-key v select-layout even-vertical      #按v将当前面板布局切换为even-vertical；相当于进入命令行模式后输入select-layout even-vertical1
```



	

	 




 




    



    

    
    


