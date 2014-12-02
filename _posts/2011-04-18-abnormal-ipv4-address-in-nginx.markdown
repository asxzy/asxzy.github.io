---
layout: post
title: nginx中获取客户端IPV4地址异常
date: '2011-4-18'
comments: true
---
之前配置好了 nginx 和 IPv6 ，并让 nginx 同时监听 IPv4 和 IPv6 地址，今天突然发现 PHP 的 getenv("REMOTE_ADDR"); 甚至 nginx 日志在获取使用 IPv4 的访客 IP 时有些问题，一概显示成了类似于 ::ffff:111.222.111.222 这种 IPv6 格式。到 nginx 的 wiki 搜索后发现了问题所在：原来 Linux 默认情况下所有的 IPv6 TCP socket 都可以通过将 IPv4 地址转换为 IPv6 地址的格式从而处理来自于 IPv4 的连接，这也就是为什么 Linux 下面的 nginx 写一个 listen [::]:80 即可 4/6 通吃的原因，但是这样就造成了客户的 IPv4 地址被翻译成了 IPv6 的格式，从而造成 php 以及其他程序无法获取客户的 IPv4 地址。这样显然问题多多，如果某个程序保存客户 IP 地址这个字段不够长的话很容易出现问题。

解决办法是在 etc/sysctl.conf 中加入一行

```
net.ipv6.bindv6only=1
```
之后
```
sysctl -p
```
即可关闭 Linux 的这一 bug feature，之后记得修改 nginx 的配置文件，加入 IPv4 的监听配置

PS：FreeBSD 默认 IPv4 和 IPv6 就是分开处理的，需要分别 listen。
