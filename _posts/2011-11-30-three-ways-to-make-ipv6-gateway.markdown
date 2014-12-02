---
layout: post
title: "单一ipv6地址做网关的三种解决方案"
date: '2011-11-30'
comments: true
---
本文主要是介绍三种在只有一个IPv6地址的情况下做网关的解决方案，这些方案基于Linux，在实验室网络部署中有着一定的应用价值。

方案一：NAT

标准的IPv6是不支持NAT的，NAT本是IPv4为了解决IP池资源不足提出的方案。但IPv6已经不存在地址不足这一说，所以NAT协议并不被官方所支持。

本IPv6 的NAT方案和IPv4的NAT方案思路一致，在IPv6下划分一段“假”的IPv6地址给客户端，通过内核转发完成NAT功能。

由于本方案并非官方支持。故本文仅给出几个现成的解决方案

NAPT66：<a title="http://code.google.com/p/napt66/" href="http://code.google.com/p/napt66/">http://code.google.com/p/napt66/</a>

北邮方案，基于openwrt开发，小巧精悍。

ipv6nat Qycaitian：<a title="http://sourceforge.net/projects/ipv6nat/" href="http://sourceforge.net/projects/ipv6nat/">http://sourceforge.net/projects/ipv6nat/</a>

西电研究生作品。支持局域网ipv6自动配置、局域网端口映射、多WAN口负载均衡

&nbsp;

方案二：IPv4 NAT + IPv6 bridge

本方案思路为，IPv4路由+IPv6交换机，将wan+lan口桥接并屏蔽掉网桥上的ipv4封包，实现ipv6链路。

严格意义上来说，本方案并不是将单一地址做网关，而是给IPv6搭了一座桥出来，让IPv6的封包从路由器直接穿过。

实现起来也非常简单。

1.桥接wan口lan口。
2.屏蔽掉所有非IPv6的包。

约定：
wan口eth1
lan口eth0、wlan0、wlan1
依赖：
ebtables、birdge-utils
命令样例
```bash
brctl addbr br-lan
ifconfig br-lan up
brctl addif br-lan eth0
brctl addif br-lan eth1
brctl addif br-lan wlan0
brctl addif br-lan wlan1
ebtables -t broute -A BROUTING -p ! ipv6 -j DROP
```
但实际上，在某些环境下，这种方法还是有缺陷的。比如需要IPv4通过交换机验证的环境中，由于客户端没有通过联网验证，上端路由器不会相应来自客户端的任何请求，故本方案只是用于IPv6无需认证的网络环境使用。

&nbsp;

方案三：proxy_ndp

众所周知，IPv4中有个arp协议，他在IPv4的网络中有着非常重要的作用。但IPv6取消了ARP协议，取而代之的是NDP（Neighbor Discovery Protocol），即邻居发现协议。而Linux在2.6.19版中加入了proxy_ndp这个特性，使得linux有了代理ipv6的能力。本方案就是基于这一特性实现的。

这一方案中，网关中单一的IPv6地址可以认定为是其子网的网关，通过任意方式给子网分配与网关相同前缀的IPv6之后，将子网的IPv6地址加入网关的ndp代理之中，从而实现子网的IPv6。

过程也是非常简单。

1.在网关上打开ipv6 forwarding和proxy_ndp。
2.用任意方式给网关wan口lan口设定合法IPv6地址，所谓合法，就是要能与外网相连。
3.用任意方式给子网划分与wan口相同前缀的合法IPv6地址。
4.在网关上将子网的IPv6地址加入proxy_ndp

需要注意的几点：

1.网关必须使用静态IPv6地址，否则IPv6 forwarding会出问题。
2.网关上的路由表一定要正确，最好添加静态路由，外网网关和内网子网都要注意，最好相互ping6检测一下是否路由正确。
3.网关添加neigh proxy，dev应为wan口。

约定：
wan口eth1
lan口br-lan
wan对外网关：2001:250:1006:3006::1
lan内客户端：2001:250:1006:3006:1112:2222:3333:4444
依赖：
linux >= 2.6.19、ip
命令样例
```bash
ip -6 route add default 2001:250:1006:3006::1 dev eth1
ip -6 route add 2001:250:1006:3006:1112:2222:3333:4444 dev br-lan
ip -6 neigh add proxy 2001:250:1006:3006:1112:2222:3333:4444 dev eth1
```
如果客户端是固定的，可以将命令写成脚本，加入/etc/init.d/network或/etc/sysconfig/network-script/ifup-eth1中。

总结：以上三种方案，nat的适用性最强，可以适用于各种ipv6的环境之中；bridge最简单，可以适用于即插即用的ipv6环境；ndp最优雅，既是标准协议，也可以解决无法通过认证，无端口映射等问题，可以适用于各大高校的实验室及宿舍网络中。



鸣谢：
西电开源社区 -> bigeagle_xd 提供解决思路；
西电腾讯创新俱乐部 提供实验环境
