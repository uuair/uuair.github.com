---
layout: post
keywords: shadowsocks,cow
description: shadowsocks
title: "用cow及shadowsocks穿越互联网(网上没有的原创内容)"
categories: [shadowsocks]
tags: [centos,shadowsocks,cow]
group: archive
icon: file-alt
---
{% include site/setup %}

我用了好多天的时间来研究，到底如何干净的访问互联网，在网络中搜索了很多遍，始终无法得到我想要的答案，作者主页也好久没动静了，问了也白问，索性一边问，一边自己思考，现在弄的差不多了，或许还要修改，但已经正常了。  

##用cow连接shadowsocks服务器，并利用pac访问互联网  

我要说的是，以下的过程，是为了留给我自己记录的，因为这些东西，我搜遍了互联网，都没找到答案，或许是我太小白了，也许一些常识，我根本不知道所以才会犯错。  

第一步，配置shadowsocks服务器。这个网上有很多的教程，我用的是python安装的版本，就不多说了，以前我也写过。  

第二步，安装cow。cow是一个二级代理，作者主页上有着详细的安装方法，主页地址是:[https://github.com/cyfdecyf/cow](https://github.com/cyfdecyf/cow)  

以下引用自作者主页  

>curl -L git.io/cow | bash  
>编辑 ~/.cow/rc (Linux) 或 rc.txt (Windows)，简单的配置例子如下  

    #开头的行是注释，会被忽略
    # 本地 HTTP 代理地址
    # 配置 HTTP 和 HTTPS 代理时请填入该地址
    # 或者在自动代理配置中填入 http://127.0.0.1:7777/pac
    listen = http://127.0.0.1:7777

    # SOCKS5 二级代理
    proxy = socks5://127.0.0.1:1080
    # HTTP 二级代理
    proxy = http://127.0.0.1:8080
    proxy = http://user:password@127.0.0.1:8080
    # shadowsocks 二级代理
    proxy = ss://aes-128-cfb:password@1.2.3.4:8388
    # cow 二级代理
    proxy = cow://aes-128-cfb:password@1.2.3.4:8388  

>Unix 系统在命令行上执行 cow & (若 COW 不在 PATH 所在目录，请执行 ./cow &)  

要说明的是，cow支持好几种协议的连接方式，一种是cow服务器连接ss服务器，一种是cow服务器连接cow服务器，另外的一种cow连接ssh不太推荐，因为容易被封。  

要说的是，如果是cow服务器连接cow服务器，那么在境外的cow服务器上的配置，只需要配置listen这行就可以了，将`listen = cow://aes-128-cfb:password@0.0.0.0:8888`这句写上，下面全部标上#就ok。

另外，我碰到的问题是，安装完cow后，运行命令`vi rc`后，看到的是一个html文件，这个内容不用管，要么把rc删了，下载作者主页上的rc，要么把内容清空，复制主页上的rc内容过来，都没问题。  

啰嗦一下说一下我的环境：  
主机a在国外的vps上，配置了shadowsocks，主机b在国内，配置了cow。这两台机器都是公网的，主机c是本机，准备利用pac访问互联网。  

那么问题来了：  

1.dns污染的问题：我使用了google的dns，居然还是被污染了（youtube.com），更别说各个isp的了，所以最后我换了opendns的dns，起码现在正常了。如果你也碰到youtube无法访问的情况，请尝试opendns的dns。

2.cow服务器的listen要设置成0.0.0.0的形式，否则无法在公网上访问到。

3.cow服务器的rc文件中，有一个认证部分，我打开了，在osx系统的http代理以及https代理中，可以输入用户名和密码。

4.本机的正确设置方式：（osx系统）  

网络设置中设置：  

**自动代理配置：http://ip(b):7777/pac** 

或者使用下面的配置:  
 
**web（http）代理:ip(b) 端口7777 下面输入账号密码**  
**安全web代理(https):ip(b) 端口7777 下面输入账号密码**  
  
我就是在这里出事的，google什么的都无法访问，最后才发现，youtube、google、facebook等网站，在我这里都是https访问。如果用第一种pac访问的办法，目前我还没办法访问到https的网站，第二种显然就是可以的了。但是第二种是所有的流量都走shadowsocks服务器了，对vps的流量有比较大的影响，而第一种，国内服务器的带宽决定了访问速度，如果可以国内走本机流量，国外走vps就好了，《曲径》的服务就是这样的，但我还没搞明白。  

那么现在既然使用了pac，访问墙内的网站，显示的是b服务器的地址，访问墙外的网站，就是服务器a的地址了。  

下一步，我将用iphone试试如何连接服务器。  

iphone的连接办法，在网络设置中，自动哪里输入pac的地址，或者手动哪里输入http的代理服务器地址就ok了。只不过同样的，无法访问https，国内全部走国内服务器。我还在寻找另外的方案解决这个问题中。

