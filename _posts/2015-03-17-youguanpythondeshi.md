---
layout: post
keywords: python
description: Mac下安装python
title: "有关Python的事"
categories: [Python]
tags: [Mac,Python]
group: archive
icon: file-alt
---
{% include site/setup %}

我是一个非计算机专业人士，从事着关于梦想的投资，以实现别人的梦想为己任，而我自己的梦想，就是带着全家环游世界，并且凭借一台笔记本电脑，就可以养活自己，无论在哪里。投资、代码，我挺想结合这两点的。凭借我对计算机微薄的了解，我给自己规划的顺序是python–>java–>c\c++，python相当于以前的vb，入门容易，并且超越vb的地方是，用途广泛，就拿他下手吧。  

我的系统环境为MAC系统，OSX10.10，本机内置的python的版本为2.7.6,查看python.org的地址得知，python2的版本为2.7.8，python3的版本为3.4.2，搜索了一下python2与python3的区别，好像是说各有利弊，现在讲python3的教程还少，开发的东西也以python2为主，所以我还是两个都装吧，自然引申出pyenv这个版本管理器以及他的插件等等。  

*不管三七二十一，先装上brew再说*  

    $ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  

>安装pyenv有两种办法，一种是利用brew，一种是作者的另外一个项目，pyenv-installer，全自动安装，顺便安装了三个插件，这三个插件是……我忘记了，反正有一个是virtualenv。这里我就使用pyenv-installer来安装。关于pyenv-installer的说明，可以看[这里](https://github.com/yyuu/pyenv-installer)  

    $ curl -L https://raw.githubusercontent.com/yyuu/pyenv-installer/master/bin/pyenv-installer | bash

*然后将*  

    export PATH="$HOME/.pyenv/bin:$PATH"
    eval "$(pyenv init -)"
    eval "$(pyenv virtualenv-init -)"  

*放到`~/.bash_profile`里面*  
*随后运行*  
    $ exec bash --login  

下面是安装可以切换的python  

    $ pyenv install -l  
*查看可安装的版本*  
    
    $ pyenv install 2.7.8  
在osx中执行这步的时候出现错误提示：*ERROR: The Python zlib extension was not compiled. Missing the zlib?*  
解决办法是将命令改为`$ CFLAGS="-I$(xcrun --show-sdk-path)/usr/include" pyenv install -v 2.7.8`  

关于pyenv的命令：  
*删除pyenv的方法是运行`rm -fr ~/.pyenv`*  

    pyenv versions  
    //查看安装的python的版本   
    pyenv local 2.7.8  
    //指定当前目录下的python版本，local还可以用global和shell分别表示全局及当前终端    
    pyenv install -l  
    //查看可安装的python版本    
    pyenv uninstall 2.7.8  
    //卸载python  

以下开始建立virtualenv  

*创建虚拟环境*  

    $pyenv virtualenv 3.4.2 project_name   
    //如果不指定3.4.2的版本号，则默认按照local指定的版本创建虚拟环境   
    $pyenv virtualenv  
    //虚拟机列表  
*指定当前目录适用某虚拟环境*  

    $ pyenv local project_name  
    $ pyenv activate <name>  
    $ pyenv deactivate  

*取消设置*  

    $ pyenv local project_name  --unset
    $ pyenv local 3.4.2 --unset  

*删除版本或者虚拟环境*  

    $ pyenv uninstall 3.4.2  
    $ pyenv uninstall project_name  


    

