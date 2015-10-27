---
layout: post
keywords: firewall
description: Centos7下的防火墙说明
title: "Centos7的frewall防火墙说明"
categories: [centos,linux,network,it]
tags: [firewall,centos]
group: archive
icon: file-alt
---
{% include site/setup %}

####关于firewalld

firewallD是一个动态防火墙，设置后无需重启服务。  

* 查看firewalld的状态:  

        firewall-cmd --state  

    其结果显示的是:  

        running  

    则表示运行中  

* 重新载入:    

        firewall-cmd --reload

        –complete-reload则会清空所有设置

* firewalld可以针对不同网络环境，应用不同的zone来设置防火墙，查看本机有什么zone，输入：

        firewall-cmd --get-zones

* 列出firewalld所能识别的服务：

        firewall-cmd --get-services

* 列出firewall所有支持的icmptypes种类:

        firewall-cmd --get-icmptypes

* 列出所有的zone以及设置：  

        firewall-cmd --list-all-zones

* 列出目前使用的zone：

        firewall-cmd --get-default-zone

* 设置使用某个zone:

        firewall-cmd --set-default-zone=<zone>

* 查看zone的详细信息：

        firewall-cmd --zone=<zone> --list-all

* 获取激活的zone:

		firewall-cmd --get-active-zones

* 打开panic模式，关闭和打开络连接：

		firewall-cmd --enable-panic
		firewall-cmd --disenable-panic

* 启用区域中的一种服务：

		firewall-cmd [zone=<zone>] --add-service=<service> [--timeout=<seconds>]

* 如果不指定区域，则使用默认区域，如果设置了时间，则服务只启动特定秒数

    例如：启动默认区域中的http服务：

		firewall-cmd zone=home --add-service=http --timeout=60

* 启用http服务60秒

	禁用服务：

		frewall-cmd [--zone=<zone>] --remove-service

* 启用区域端口和协议组合：

		firewall-cmd [--zone=<zone>] --add-port=<port>[-<port>]/<protocol> [--timeout=<seconds>]

    端口可以是单独的 ，也可以是范围 – ，协议可以是tcp或udp。

* 禁用端口和协议组合：

		firewall-cmd [--zone=<zone>] --remove-port=<port>[-<port>]/<protocol>

* ip伪装开启，关闭，查询：

		firewall-cmd [--zone<zone>] --add-masquerade 
		firewall-cmd [--zone<zone>] --remove-masquerade 
		firewall-cmd [--zone<zone>] --query-masquerade

* 区域的icmp阻塞开启，关闭，查询：

		firewall-cmd [--zone=<zone>] --add-icmp-block=<icmptype> 
		firewall-cmd [--zone=<zone>] --remove-icmp-block=<icmptype> 
		firewall-cmd [--zone=<zone>] --query-icmp-block=<icmptype>

* 阻塞区域的响应应答报文：  

		firewall-cmd --zone=public --add-icmp-block=echo-reply

* 在区域中启用端口转发：

		firewall-cmd [--zone=<zone>] --add-forward-port=port=<port>[-<port>]:proto=<protocol> { :toport=<port>-[<port>]} | :toaddr=<address> | :toport=<port>[-<port>]:toaddr=<address> }

端口可以映射到另一台主机的同一端，也可以是同一主机或另一主机的不同端口。端口可以是单独的 也可以是端口范围 – ,协议可以是tcp或udp，目标端口可以是端口 也可以是端口范围 –

* 例：将区域home的ssh转发到127.0.0.2  

		firewall-cmd –zone=home –add-forward-port=port=22:proto=tcp:toaddr=127.0.0.2

永久区域，需要重载或者重启服务后生效：

将参数 –permanent作为第一个设置参数

直接选项，重载或重启服务后失效：

将参数 –direct作为第一个设置参数

centos firewall 防火墙