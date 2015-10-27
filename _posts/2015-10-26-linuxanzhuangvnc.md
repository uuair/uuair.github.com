---
layout: post
keywords: linux,vnc
description: linux安装vnc
title: "linux安装vnc"
categories: [linux,vnc]
tags: [vnc,linux]
group: archive
icon: file-alt
---
{% include site/setup %}
 
###安装vnc：  

    apt-get install tightvncserver  

    tightvncserver  

#####设置密码后，显示  

    New 'X' desktop is kali:1  

注意后面的:1，启动vnc客户端：下载地址(http://www.realvnc.com)   

输入：`ip:1`来连接   

#####关闭vnc输入：  

    tightvncserver -kill :1  

raspberry用户还多了一个选择，realvnc专门针对树莓派也有了vnc server:下载地址(http://www.realvnc.com/products/vnc/raspberrypi/)  

#####修改vnc密码：  

    vncpasswd  

#####查看vnc端口：  

    netstat -nutlp  

-n ：列出数字形式的连接地址  
-u ：列出 UDP 的连接  
-t ：列出 TCP 的连接  
-l ：正在进行 Listen (监听)的服务网络状态  
-p ：列出 PID 与 Program 的名称  

或者ps命令来查看：  

    ps aux | grep vnc  

-a ：不和終端機 (terminal) 有關的所有程序  
-u ：所有有效使用者 (effective user) 的程序  
-x ：與 a 這個參數一起使用可列出完整資訊  
-| grep vnc 表示只列出有包含 vnc 關鍵字的程序  

#####修改vnc启动的桌面为默认的LXDE:   

    vi ~/.vnc/xstartup  

进入后可以添加最后一行，注释掉其他：  

    xrdb $HOME/.Xresources
    xsetroot -solid grey
    x-terminal-emulator -geometry 80x24+10+10 -ls -title "$VNCDESKTOP Desktop" &
    #x-window-manager &
    # Fix to make GNOME work
    #export XKL_XMODMAP_DISABLE=1
    #/etc/X11/Xsession
    /usr/bin/startlxde &    



#####开机启动vnc:  

在 /etc/init.d/ 下建立一个控制的脚本 (script)， 例如取名为tightvncserver  


```
#!/bin/sh
### BEGIN INIT INFO
# Provides:          tightvncserver
# Required-Start:    $local_fs
# Required-Stop:     $local_fs
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Short-Description: Start/stop tightvncserver
### END INIT INFO
 
# More details see:
# http://www.penguintutor.com/linux/tightvnc
 
### Customize this entry
# Set the USER variable to the name of the user to start tightvncserver under
export USER='root'
### End customization required
 
eval cd ~$USER
 
case "$1" in
  start)
    # 启动命令行。此处自定义分辨率、控制台号码或其它参数。
    su $USER -c '/usr/bin/tightvncserver :1'
    echo "Starting TightVNC server for $USER "
    ;;
  stop)
    # 终止命令行。此处控制台号码与启动一致。
    su $USER -c '/usr/bin/tightvncserver -kill :1'
    echo "Tightvncserver stopped"
    ;;
  *)
    echo "Usage: /etc/init.d/tightvncserver {start|stop}"
    exit 1
    ;;
esac
exit 0
```  

注意这里的`export USER='root'`,需要修改成自己要登陆的用户，kali默认单用户，只有root，如果是respberry的话，默认应该是`pi`用户  

#####修改脚本权限：  

    sudo chmod 755 /etc/init.d/tightvncserver  

#####将脚本加入启动项：  

    sudo update-rc.d tightvncserver defaults    

#####修改vnc默认端口：  

    /usr/bin/tightvncserver  
    $vncPort = 5900 + $displayNumber;  

修改5900为8888，则连接`:1`的地址变为`ip:8889`  

#####取消开机启动：  

    sudo update-rc.d -f tightvncserver remove 