---
layout: post
title: VirtualBox中的主宿机虚拟机互通
date: '2010-11-19'
comments: true
---
近期想在本地配置一个睿思服务器的生产环境，由于DT的校园网，环境只能在虚拟机中配置。

配置目的：
1.主宿机虚拟机可以相互访问。
2.虚拟机可以上网。

我是这样一个思路去配置的。
利用VirtualBox的Host-Only模式实现主宿机和虚拟机的互通
通过共享主宿机的物理网卡实现虚拟机上网。

配置过程：
1.主宿机中安装VirtualBox Host-Only Network虚拟网卡（安装VirtualBox的时候默认会安装一个）。
打开VirtualBox->管理->全局设定->网络->添加Host-Only网络

![](/uploads/2010/11/01.jpg "添加host-only网卡")

2.共享主宿机的网卡。
右键桌面上的管理->更改适配器设置->右键"本地连接"->共享->选中"允许其他……"->网卡选中VirtualBox Host-Only Network
确定之后有个对话框，点确定

![](/uploads/2010/11/1.jpg "共享网络")

3.关闭VirtualBox中的DHCP服务器。
打开VirtualBox->管理->全局设定->网络->编辑网络->DHCP服务器->关闭“启用服务器”。

![](/uploads/2010/11/2.jpg "关闭VirtualBox中的DHCP服务器")

4.设置虚拟机为Host-Only Network。

![](/uploads/2010/11/3.jpg "更改虚拟机网络为Host-Only")


之后进入虚拟机设置虚拟机网卡为DHCP自动获取即可。



至此，大功告成
