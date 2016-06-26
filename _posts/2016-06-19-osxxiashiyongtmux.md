---
layout: post
keywords: tmux+powerline
description: osx10.11下使用tmux+powerline
title: "osx下使用tmux+powerline（一）"
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

####Session相关操作 

**操作**
<div class="level2">
<table>
<p>
类似各种平铺式窗口管理器，tmux使用键盘操作，常用快捷键包括：
</p>
<div class="table sectionedit5"><table class="inline">
	<tr class="row0">
		<td class="col0 centeralign" colspan="2">  Ctrl+b  </td><td class="col2">激活控制台；此时以下按键生效</td>
	</tr>
	<tr class="row1">
		<td class="col0" rowspan="9">系统操作</td><td class="col1 centeralign">  ?  </td><td class="col2">列出所有快捷键；按q返回</td>
	</tr>
	<tr class="row2">
		<td class="col0 centeralign">  d  </td><td class="col1">脱离当前会话；这样可以暂时返回Shell界面，输入tmux attach能够重新进入之前的会话</td>
	</tr>
	<tr class="row3">
		<td class="col0 centeralign">  D  </td><td class="col1">选择要脱离的会话；在同时开启了多个会话时使用</td>
	</tr>
	<tr class="row4">
		<td class="col0 centeralign">  Ctrl+z  </td><td class="col1">挂起当前会话</td>
	</tr>
	<tr class="row5">
		<td class="col0 centeralign">  r  </td><td class="col1">强制重绘未脱离的会话</td>
	</tr>
	<tr class="row6">
		<td class="col0 centeralign">  s  </td><td class="col1">选择并切换会话；在同时开启了多个会话时使用</td>
	</tr>
	<tr class="row7">
		<td class="col0 centeralign">  :  </td><td class="col1">进入命令行模式；此时可以输入支持的命令，例如kill-server可以关闭服务器</td>
	</tr>
	<tr class="row8">
		<td class="col0 centeralign">  [  </td><td class="col1">进入复制模式；此时的操作与vi/emacs相同，按q/Esc退出</td>
	</tr>
	<tr class="row9">
		<td class="col0 centeralign">  ~  </td><td class="col1">列出提示信息缓存；其中包含了之前tmux返回的各种提示信息</td>
	</tr>
	<tr class="row10">
		<td class="col0" rowspan="10">窗口操作</td><td class="col1 centeralign">  c  </td><td class="col2">创建新窗口</td>
	</tr>
	<tr class="row11">
		<td class="col0 centeralign">  &amp;  </td><td class="col1">关闭当前窗口</td>
	</tr>
	<tr class="row12">
		<td class="col0 centeralign">  数字键  </td><td class="col1">切换至指定窗口</td>
	</tr>
	<tr class="row13">
		<td class="col0 centeralign">  p  </td><td class="col1">切换至上一窗口</td>
	</tr>
	<tr class="row14">
		<td class="col0 centeralign">  n  </td><td class="col1">切换至下一窗口</td>
	</tr>
	<tr class="row15">
		<td class="col0 centeralign">  l  </td><td class="col1">在前后两个窗口间互相切换</td>
	</tr>
	<tr class="row16">
		<td class="col0 centeralign">  w  </td><td class="col1">通过窗口列表切换窗口</td>
	</tr>
	<tr class="row17">
		<td class="col0 centeralign">  ,  </td><td class="col1">重命名当前窗口；这样便于识别</td>
	</tr>
	<tr class="row18">
		<td class="col0 centeralign">  .  </td><td class="col1">修改当前窗口编号；相当于窗口重新排序</td>
	</tr>
	<tr class="row19">
		<td class="col0 centeralign">  f  </td><td class="col1">在所有窗口中查找指定文本</td>
	</tr>
	<tr class="row20">
		<td class="col0" rowspan="14">面板操作</td><td class="col1 centeralign">  “  </td><td class="col2">将当前面板平分为上下两块</td>
	</tr>
	<tr class="row21">
		<td class="col0 centeralign">  %  </td><td class="col1">将当前面板平分为左右两块</td>
	</tr>
	<tr class="row22">
		<td class="col0 centeralign">  x  </td><td class="col1">关闭当前面板</td>
	</tr>
	<tr class="row23">
		<td class="col0 centeralign">  !  </td><td class="col1">将当前面板置于新窗口；即新建一个窗口，其中仅包含当前面板</td>
	</tr>
	<tr class="row24">
		<td class="col0 centeralign">  Ctrl+方向键  </td><td class="col1">以1个单元格为单位移动边缘以调整当前面板大小</td>
	</tr>
	<tr class="row25">
		<td class="col0 centeralign">  Alt+方向键  </td><td class="col1">以5个单元格为单位移动边缘以调整当前面板大小</td>
	</tr>
	<tr class="row26">
		<td class="col0 centeralign">  Space  </td><td class="col1">在预置的面板布局中循环切换；依次包括even-horizontal、even-vertical、main-horizontal、main-vertical、tiled</td>
	</tr>
	<tr class="row27">
		<td class="col0 centeralign">  q  </td><td class="col1">显示面板编号</td>
	</tr>
	<tr class="row28">
		<td class="col0 centeralign">  o  </td><td class="col1">在当前窗口中选择下一面板</td>
	</tr>
	<tr class="row29">
		<td class="col0 centeralign">  方向键  </td><td class="col1">移动光标以选择面板</td>
	</tr>
	<tr class="row30">
		<td class="col0 centeralign">  {  </td><td class="col1">向前置换当前面板</td>
	</tr>
	<tr class="row31">
		<td class="col0 centeralign">  }  </td><td class="col1">向后置换当前面板</td>
	</tr>
	<tr class="row32">
		<td class="col0 centeralign">  Alt+o  </td><td class="col1">逆时针旋转当前窗口的面板</td>
	</tr>
	<tr class="row33">
		<td class="col0 centeralign">  Ctrl+o  </td><td class="col1">顺时针旋转当前窗口的面板</td>
	</tr>
</table></div>

