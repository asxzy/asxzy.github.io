---
layout: post
title: 压缩vdi虚拟硬盘的集中方法(转)
date: '2010-11-19'
comments: true
---
http://osnaile.osdn.cn/?p=124

用 Sun VirtualBox 软件虚拟出来的硬盘文件是 VDI 文件，这个文件会随着使用而变大，因为磁盘碎片的产生，这个文件里也有很多的没用的空闲空间，为了节省空间，就需要对 VDI 文件进行压缩。

压缩分三步，1.在虚拟系统中进行碎片整理；2.在虚拟系统中把空闲空间标记为 0；3.在宿主系统中收缩 VDI 文件。

第一步，碎片整理可以用系统自带的，也可以使用第三方软件。

第二步，使用 “sdelete” 把空闲空间标记为 0，下载地址：http://technet.microsoft.com/en-us/sysinternals/bb897443.aspx

第三步，收缩

收缩有两个办法，一个是使用 VirtualBox 自带的 VBoxManage.exe，命令格式是：
```
VBoxManage modifyhd VDI文件名 compact
```
不过，我在使用这个命令时出错了，错误信息是：“Shrink hard disk operation is not implemented!”

我在网上也查了这个错误，有不少人也遇到了同样的问题。

有高人写了一段小代码，实现了这个功能，PackVDI，下载地址：http://jerome.hode.free.fr/opensource/PackVDI.zip

执行 PackVDI 文件名即可。

注：本文内容只在 WINDOWS 环境下测试过，VirtualBox 版本：2.1.4

http://www.hooto.com/home/rui/blog/archives/5144.html

指导思想

1. 虚拟机: 清理系统，卸载、删除系统垃圾文件

2. 虚拟机: 将磁盘数据靠“前”移动，并将剩余磁盘空间写“零”

3. 物理主机: 清除“零”字节空间，使用 VBoxManage modifyhd 工具压缩 VDI 磁盘镜像文件

Windows 虚拟机

1. 虚拟机: 删除系统垃圾文件，运行磁盘整理程序...

2. 虚拟机: 用 SDelete 工具写"零"，下载地址 http://technet.microsoft.com/en-us/sysinternals/bb897443.aspx，在命令行下执行 "sdelete -c"... 关机...

3. 物理主机: 执行 "VBoxManage modifyhd /the-path-of-VDI.vdi --compact"

1、要想复制一个VDI再次使用，必须通过VboxManager命令实现，语法是
```
   vboxmanager clonevdi <source_vdi> <destination_vdi>
```
2、VirtualBox并没有提供这个功能的GUI方式，另外，VboxManager命令有不少增强功能，可以参考UserGuide。

   查看VDI文件信息 vboxmanager showvdiinfo <vdi_file>
   压缩VDI文件体积 vboxmanager modifyvdi <uuid | vdi_file> compact
