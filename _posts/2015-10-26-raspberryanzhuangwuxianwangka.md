---
layout: post
keywords: raspberry
description: 安装无线网卡
title: "raspberry安装无线网卡"
categories: [linux,rasberry]
tags: [rapberry,linux]
group: archive
icon: file-alt
---
{% include site/setup %}
 
#####访问无线网：  

我购买的是无驱的无线网卡:  
![](http://uuair.qiniudn.com/image/3/87/412ed7205dd2b94c30f6859e43f6d.jpg)  

1.查看网卡：  

```
pi@raspberrypi ~ $ lsusb
Bus 001 Device 002: ID 0424:9514 Standard Microsystems Corp. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 003: ID 0424:ec00 Standard Microsystems Corp. 
Bus 001 Device 004: ID 0bda:8176 Realtek Semiconductor Corp. RTL8188CUS 802.11n WLAN Adapter
```

2.查看网络，一开始没有连接，所以显示的是`unassociated`    

```
pi@raspberrypi ~ $  iwconfig wlan0
wlan0     unassociated  Nickname:""
          Mode:Managed  Frequency=2.412 GHz  Access Point: Not-Associated   
          Sensitivity:0/0  
          Retry:off   RTS thr:off   Fragment thr:off
          Power Management:off
          Link Quality:0  Signal level:0  Noise level:0
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:0   Missed beacon:0
``` 

3.扫描网络：  

```
pi@raspberrypi ~ $ sudo iwlist wlan0 scan
wlan0     Scan completed :
          Cell 03 - Address: 40:4A:03:92:BA:4B
                    ESSID:"foo"
                    Protocol:IEEE 802.11bgn
                    Mode:Master
                    Frequency:2.462 GHz (Channel 11)
                    Encryption key:on
                    Bit Rates:144 Mb/s
                    Extra:rsn_ie=30140100000fac040100000fac040100000fac020c00
                    IE: IEEE 802.11i/WPA2 Version 1
                        Group Cipher : CCMP
                        Pairwise Ciphers (1) : CCMP
                        Authentication Suites (1) : PSK
                    Quality=88/100  Signal level=42/100  
```  

4.修改`/etc/wpa_supplicant/wpa_supplicant.conf`  

`pi@raspberrypi:~$ sudo vi /etc/wpa_supplicant/wpa_supplicant.conf`  

对应的文档修改为：  

```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
        ssid="foo"
        psk="1234567890123"
        proto=RSN
        key_mgmt=WPA-PSK
        pairwise=CCMP
        auth_alg=OPEN
}
```

######扫描结果与对应栏目介绍：  

`IE: IEEE 802.11i/WPA2 Version 1`  

表示加密结果为WPA2,对应的项目为proto。  
`RSN`:WPA(2)  
`WPA`:WPA(1)  

```
Group Cipher : CCMP 
Pairwise Ciphers (1) : CCMP
```
表示WPA2使用AES加密方式，对应的项目为pairwise。  
`CCMP`:AES cipher, WPA(2)  
`TKIP`:TKIP cipher, WPA(1)  

`Authentication Suites (1) :PSK`  
表示使用pre-shared key做鉴定，对应的项目为key_mgmt。  
`WPA-PSK`:Authentication via pre-shared key  
`WPA-EAP`:Authentication via enterprise authentication server  

5.重启网卡：  

    sudo ifdown wlan0  
    sudo ifup wlan0  

有一些显示的信息，是可以忽略的：  

```
ioctl[SIOCSIWAP]: Operation not permitted
ioctl[SIOCSIWENCODEEXT]: Invalid argument
ioctl[SIOCSIWENCODEEXT]: Invalid argument
```  

6.通过DHCP获得ip地址：

    sudo dhclient wlan0  

如果显示如下信息，可以忽略掉：  

```
rfkill: Cannot open RFKILL control device
ioctl[SIOCSIWAP]: Operation not permitted
ioctl[SIOCSIWENCODEEXT]: Invalid argument
ioctl[SIOCSIWENCODEEXT]: Invalid argument
```  

或者：

    RTNETLINK answers: File exists  

10.成功获得ip地址  

```
pi@raspberrypi ~ $ ifconfig wlan0
wlan0     Link encap:Ethernet  HWaddr 74:da:38:05:68:4c  
          inet addr:192.168.1.117  Bcast:192.168.1.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:1158 errors:0 dropped:79 overruns:0 frame:0
          TX packets:53 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:109024 (106.4 KiB)  TX bytes:6214 (6.0 KiB)
```
