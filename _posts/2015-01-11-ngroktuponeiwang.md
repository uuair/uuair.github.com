---
layout: post
keywords: Centos,ngrok,代理,内网
description: 使用ngrok突破内网
title: "ngrok代理，使外网可以访问内网"
categories: [Centos]
tags: [Centos,ngrok,网络]
group: archive
icon: file-alt
---
{% include site/setup %}

无奈的使用了宽带通这个运营商，经常断，网速不稳定，还没有公网IP，办理的时候说有，但其实是个伪地址，通过v2ex.com上面的询问，确定了俺没有公网IP这个事实了。  

如果想通过外网访问自己的电脑，我尝试了花生壳收费服务，内网可以突破的服务，可惜我没有windows的机器，花生壳绑定到路由器上依然无法使用内网服务，所以退款了（还在审核中，两天了）。  

然后v2ex的高手给我推荐了几个程序，我没有一一尝试，因为我是计算机小白啊，太高深了肯定搞不定。比如“localtunnel"，好像不符合我的要求，我想访问ssh。  

直到有人推荐给我**ngrok**,第一，我看得懂说明啊，第二，简单功能可以实现，还有高级功能，虽然我现在不懂，但起码是个希望不是坑啊。  

下面来开始介绍我学习ngrok的过程：  

首先是官网[ngrok](http://www.ngrok.com)  

其实官方的介绍很详细了，但我还是简单说一下吧。

如果想马上运行期ngrok来，只要下载ngrok到电脑中（我使用的是centos）然后运行  
`ngrok 80`  
会出现下面的界面：  

    ngrok

    Tunnel Status                 online
    Version                       1.3/1.3
    Forwarding                    http://3a4bfceb.ngrok.com -> 127.0.0.1:80
    Forwarding                    https://3a4bfceb.ngrok.com -> 127.0.0.1:80
    Web Interface                 http://127.0.0.1:4040
    # Conn                        0
    Avg Conn Time                 0.00ms

这里显示的就是使用**http://3a4bfceb.ngrok.com**这个域名，可以访问到本机的80端口。域名是ngrok随机给的，如果不退出ngrok，则这个域名可以一直使用，当然也可以自定义域名，不过这需要先在ngrok网站上注册账号，注册后登陆，马上会看到一段命令，这段命令需要在本地运行，并写入.ngrok文件中，比如我的：  

`ngrok -authtoken /EIIALciaoiu4iJjkdoIUWO 80`  

当然了，这段命令是我伪造的，不过意思差不多，真输入了是没效果的，第一次需要输入，以后就不用了。当输入完成后，可以使用自定义域名访问本机http服务的办法了。  

`ngrok -subdomain=xxx 80`  

xxx这里可以输入任意字符，会生成xxx.ngrok.com的域名，输入后会提示：  

    ngrok

    ...
    Forwarding                    https://xxx.ngrok.com -> 127.0.0.1:80  
    ...  

接下来就是我自己用到的ssh服务以及各种端口转发了  

简单版：  

`ngrok -proto=tcp22`  

    ngrok

    ...
    Forwarding                    tcp://ngrok.com:50612 -> 127.0.0.1:22
    ...  

这时候，就可以使用ngrok.com:50612来访问本机的22端口了。其中50612这个端口是随机的，每次使用也都不相同。

进阶版：

如果想跟我一样，端口转发多个，就需要将配置写入.ngrok文件中，当然这个文件还可以实现同时运行http访问等ngrok可以提供的所有功能。  

*我这里必须使用root权限才可以修改此文件，但必须退出root权限才可以运行！*  

    vi .ngrok
    
    tunnels:
       ssh:
        remote_port: 50019
        proto:
          tcp: 22
       ssh1:
        remote_port: 50029
        proto:
          tcp: 9999
       xxx.com
        remote_port: 50039
        proto:
          http: 9090  

这个文件可以一直写下去，**tunnels**是必须写的，**remote_port**这里自定义了在ngrok.com后面的端口号，如果不写则为随机显示。后面的ssh、ssh1、xxx.com这些都是运行的名字，可以自定义，运行的时候输入  
`./ngrok start ssh ssh1 xxx.com`   

    ngrok

    Tunnel Status                 online
    Version                       1.3/1.3
    Forwarding                    tcp://ngrok.com:44764 -> 127.0.0.1:22
    Forwarding                    tcp://ngrok.com:48973 -> 127.0.0.1:999
    Forwarding                    https://xxx.ngrok.com -> 127.0.0.1:9090
    
到目前为止，程序已经正常运行了，端口转发很happy。但我担心如果端口都绑定到ngrok这个网站，会不安全。所以我想自己架设ngrok服务器，并且由于ngrok服务器在境外，访问速度并不快，所以如果有一台境内服务器就更方便了。好在ngrok也提供了这样的服务,需要一个ssl的证书，我还没搞定这事，下次接着写吧。