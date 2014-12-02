---
layout: post
title: windows 7下关闭IPV6隧道
date: '2010-12-20'
comments: true
---
Windows 7下关闭IPV6隧道

IPv6隧道是将IPv6报文封装在IPv4报文中，让IPv6数据包穿过IPv4网络进行通信。对于采用隧道技术的设备来说，在隧道的入口处，将IPv6的数据报封装进IPv4，IPv4报文的源地址和目的地址分别是隧道入口和隧道出口的IPv4地址。

若想还原IPv6隧道则用以下命令:

```bash
netsh interface teredo set state default
netsh interface 6to4 set state default
netsh interface isatap set state default
```
我是有原生IPV6的人，更多情况下，我希望关闭IPv6隧道。
```bash
netsh interface teredo set state disable
netsh interface 6to4 set state disabled
netsh interface isatap set state disabled
```
