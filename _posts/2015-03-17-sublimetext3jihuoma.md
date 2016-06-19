---
layout: post
keywords: Sublime text3
description: sublime text3
title: "Sublime text3记录"
categories: [software]
tags: [sublime,破解]
group: archive
icon: file-alt
---
{% include site/setup %}

我是菜鸟小白，高大上的东西我也不懂，摸索出的成果记录下来，方便以后看。

我的SublimeText3的配置以及插件放到这里了[Github](https://github.com/uuair/sublime)，以后也会在这里更新。

用上以后不得不感慨，这些Geek的或者是程序员随手用来的东西，太复杂了，每一种软件学习起来，都很吃力，尤其是对于我这种不经常用的，今年用完，下次再用不定什么时候呢，不好好记下来，以后还要走弯路，我是翻了多少网站才解决了诸多问题啊。  

####快捷键：  

#####选择类：  

Ctrl+D 选中光标所占的文本，继续操作则会选中下一个相同的文本。
Alt+F3 选中文本按下快捷键，即可一次性选择全部的相同文本进行同时编辑。举个栗子：快速选中并更改所有相同的变量名、函数名等。
Ctrl+L 选中整行，继续操作则继续选择下一行，效果和 Shift+↓ 效果一样。
Ctrl+Shift+L 先选中多行，再按下快捷键，会在每行行尾插入光标，即可同时编辑这些行。
Ctrl+Shift+M 选择括号内的内容（继续选择父括号）。举个栗子：快速选中删除函数中的代码，重写函数体代码或重写括号内里的内容。
Ctrl+M 光标移动至括号内结束或开始的位置。
Ctrl+Enter 在下一行插入新行。举个栗子：即使光标不在行尾，也能快速向下插入一行。
Ctrl+Shift+Enter 在上一行插入新行。举个栗子：即使光标不在行首，也能快速向上插入一行。
Ctrl+Shift+[ 选中代码，按下快捷键，折叠代码。
Ctrl+Shift+] 选中代码，按下快捷键，展开代码。
Ctrl+K+0 展开所有折叠代码。
Ctrl+← 向左单位性地移动光标，快速移动光标。
Ctrl+→ 向右单位性地移动光标，快速移动光标。
shift+↑ 向上选中多行。
shift+↓ 向下选中多行。
Shift+← 向左选中文本。
Shift+→ 向右选中文本。
Ctrl+Shift+← 向左单位性地选中文本。
Ctrl+Shift+→ 向右单位性地选中文本。
Ctrl+Shift+↑ 将光标所在行和上一行代码互换（将光标所在行插入到上一行之前）。
Ctrl+Shift+↓ 将光标所在行和下一行代码互换（将光标所在行插入到下一行之后）。
Ctrl+Alt+↑ 向上添加多行光标，可同时编辑多行。
Ctrl+Alt+↓ 向下添加多行光标，可同时编辑多行。  

#####编辑类： 

Ctrl+J 合并选中的多行代码为一行。举个栗子：将多行格式的CSS属性合并为一行。
Ctrl+Shift+D 复制光标所在整行，插入到下一行。
Tab 向右缩进。
Shift+Tab 向左缩进。
Ctrl+K+K 从光标处开始删除代码至行尾。
Ctrl+Shift+K 删除整行。
Ctrl+/ 注释单行。
Ctrl+Shift+/ 注释多行。
Ctrl+K+U 转换大写。
Ctrl+K+L 转换小写。
Ctrl+Z 撤销。
Ctrl+Y 恢复撤销。
Ctrl+U 软撤销，感觉和 Gtrl+Z 一样。
Ctrl+F2 设置书签，F2切换书签
Ctrl+T 左右字母互换。
F6 单词检测拼写   

#####搜索类:  

Ctrl+F 打开底部搜索框，查找关键字。
Ctrl+shift+F 在文件夹内查找，与普通编辑器不同的地方是sublime允许添加多个文件夹进行查找，略高端，未研究。
Ctrl+P 打开搜索框。举个栗子：1、输入当前项目中的文件名，快速搜索文件，2、输入@和关键字，查找文件中函数名，3、输入：和数字，跳转到文件中该行代码，4、输入#和关键字，查找变量名。
Ctrl+G 打开搜索框，自动带：，输入数字跳转到该行代码。举个栗子：在页面代码比较长的文件中快速定位。
Ctrl+R 打开搜索框，自动带@，输入关键字，查找文件中的函数名。举个栗子：在函数较多的页面快速查找某个函数。
Ctrl+： 打开搜索框，自动带#，输入关键字，查找文件中的变量名、属性名等。
Esc 退出光标多行选择，退出搜索框，命令框等。
Ctrl+Shift+P 打开命令框。场景例子：打开命名框，输入关键字，调用sublime text或插件的功能，例如使用package安装插件。

#####显示类:  

Ctrl+Tab 按文件浏览过的顺序，切换当前窗口的标签页。
Ctrl+PageDown 向左切换当前窗口的标签页。
Ctrl+PageUp 向右切换当前窗口的标签页。
Alt+Shift+1 窗口分屏，恢复默认1屏（非小键盘的数字）
Alt+Shift+2 左右分屏-2列
Alt+Shift+3 左右分屏-3列
Alt+Shift+4 左右分屏-4列
Alt+Shift+5 等分4屏
Alt+Shift+8 垂直分屏-2屏
Alt+Shift+9 垂直分屏-3屏
Ctrl+K+B 开启/关闭侧边栏。
F11 全屏模式
Shift+F11 免打扰模式

#####跳转:  

用 Command+P 可以快速跳转到当前项目中的任意文件，可进行关键词匹配。
用 Command+P 后 @ (或是Command+R)可以快速列出/跳转到某个函数（很爽的是在markdown当中是匹配到标题，而且还是带缩进的！）。
用 Command+P 后 # 可以在当前文件中进行搜索。
用 Command+P 后 : (或是Ctrl+G)加上数字可以跳转到相应的行。
而更酷的是你可以用 Command+P 加上一些关键词跳转到某个文件同时加上@来列出/跳转到目标文件中的某个函数，或是同时加上#来在目标文件中进行搜索，或是同时加上:和数字来跳转到目标文件中相应的行。

#####多重选择（Multi-Selection）:

按住 Command 或 Alt，然后在页面中希望中现光标的位置点击。
选择数行文本，然后按下 Shift + Command + L。
通过反复按下 Control/Command+D 即可将全文中与光标当前所在位置的词相同的词逐一加入选择，而直接按下 Alt+F3(Windows) 或是 Ctrl+Command+G(Mac) 即可一次性选择所有相同的词。
按下鼠标中键来进行垂直方向的纵列选择，也可以进入多重编辑状态。  

#####VIM模式:

如果更喜欢 Vim 的编辑模式，可以通过以下方法来激活 Vintage mode：

按下 Shift + Command + P 调出命令面板。
输入settings user调出 Preferences：Settings - User，并按下回车。
这时会打开一个 Preferences.sublime-settings 的文件，如果是第一次修改，它应该是个空文件，把以下文本粘贴进去：
{
"ignored_packages": []
}
保存这个文件，这时按下 ESC 键，再按下一些你熟悉的 Vim 命令，是不是很有亲切感？  

>以上快捷键部分引用自[https://www.zybuluo.com/king/note/47271]，感谢作者。  

###Sublime Text3 激活  

不激活也不影响使用，激活了没变化。  

在help菜单里输入以下代码：  

	—– BEGIN LICENSE —–
	Andrew Weber
	Single User License
	EA7E-855605
	813A03DD 5E4AD9E6 6C0EEB94 BC99798F
	942194A6 02396E98 E62C9979 4BB979FE
	91424C9D A45400BF F6747D88 2FB88078
	90F5CC94 1CDC92DC 8457107A F151657B
	1D22E383 A997F016 42397640 33F41CFC
	E1D0AE85 A0BBD039 0E9C8D55 E1B89D5D
	5CDB7036 E56DE1C0 EFCC0840 650CD3A6
	B98FC99C 8FAC73EE D2B95564 DF450523
	—— END LICENSE ——
