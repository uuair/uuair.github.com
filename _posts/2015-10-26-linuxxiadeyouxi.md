---
layout: post
keywords: game,linux
description: linux terminal game
title: "Linux下的彩蛋及terminal游戏"
categories: [linux]
tags: [game,linux,centos,emacs]
group: archive
icon: file-alt
---
{% include site/setup %}

###Linux下的彩蛋及terminal游戏


###Emacs篇：

查看emacs中内置的游戏可以进入：

    ls /usr/share/emacs/**/lisp/play

例如我这里显示的是：

```
/usr/share/emacs/22.1/lisp/play
├── 5x5.el.gz
├── 5x5.elc
├── animate.el.gz
├── animate.elc
├── blackbox.el.gz
├── blackbox.elc
├── bruce.el
├── cookie1.el.gz
├── cookie1.elc
├── decipher.el.gz
├── decipher.elc
├── dissociate.el.gz
├── dissociate.elc
├── doctor.el.gz
├── doctor.elc
├── dunnet.el.gz
├── dunnet.elc
├── fortune.el.gz
├── fortune.elc
├── gamegrid.el.gz
├── gamegrid.elc
├── gametree.el.gz
├── gametree.elc
├── gomoku.el.gz
├── gomoku.elc
├── handwrite.el.gz
├── handwrite.elc
├── hanoi.el.gz
├── hanoi.elc
├── landmark.el.gz
├── landmark.elc
├── life.el.gz
├── life.elc
├── meese.el.gz
├── meese.elc
├── morse.el.gz
├── morse.elc
├── mpuz.el.gz
├── mpuz.elc
├── pong.el.gz
├── pong.elc
├── snake.el.gz
├── snake.elc
├── solitaire.el.gz
├── solitaire.elc
├── spook.el.gz
├── spook.elc
├── studly.el.gz
├── studly.elc
├── tetris.el.gz
├── tetris.elc
├── yow.el.gz
├── yow.elc
├── zone.el.gz
└── zone.elc
```
  
想要运行这些游戏，需要进入emacs

    emacs  

![](http://uuair.qiniudn.com/image/2/d0/9f8e63b6637d1173b16bfdaa887ce.png)

输入Enter后会看到密密麻麻的文字：

![](http://uuair.qiniudn.com/image/3/c6/0cf64560150bd0560b55925b4f480.png)

随便按一下方向键或者Enter跳过  

![](http://uuair.qiniudn.com/image/e/51/1d4adbde2afbe62f77998047020c5.png)

出现这个画面后同时按下Esc键和x（执行），然后输入你想玩的游戏的名字
  
![](http://uuair.qiniudn.com/image/0/22/d0d21dc9e5fca89f302b9cca375d9.png)
![](http://uuair.qiniudn.com/image/e/71/c5e8e246cc0ca1507abd902babcaa.png)  
![](http://uuair.qiniudn.com/image/f/12/b30aab42e8d42ac004bdc68378d54.png)  

俄罗斯方块:输入tetris  

![](http://uuair.qiniudn.com/image/8/69/12d60887ebafd29a11af70068e5cd.png)  

贪吃蛇:输入snake  

![](http://uuair.qiniudn.com/image/4/b1/a41e1ef9c7d2328a845ea039a56c4.png)

五子棋:输入gomoku  

![](http://uuair.qiniudn.com/image/a/a0/22d77db439d15fcf1fbff14a3ce60.png)

乒乓球:输入pong  