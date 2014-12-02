---
layout: post
title: "如何为ATI/APU用户编译编译安装XBMC，硬解播放视频"
date: '2011-12-31'
comments: true
---
本文译自：<a href="http://forum.xbmc.org/showthread.php?t=116996">http://forum.xbmc.org/showthread.php?t=116996</a>

译者：asxzy <asxzy@asxzy.net>


<span style="font-size: large;">什么是Xvba</span>

Xvba（X-Video Bitstream Acceleration）是使用A卡和FusionAPU进行硬件视频加速的类库.
如果你有兴趣的话，<a href="http://www.phoronix.com/scan.php?page=news_item&px=MTAyODU" target="_blank">这里</a>?有一些Xvba的信息

这个项目是由<strong>FernetMenta</strong>和<strong>fritsch?</strong>组织并发起的

<span style="font-size: medium;">现状</span>
<strong>你可以获得:</strong>
- 改进后的稳定的VAAPI(xvba-va-driver)，非常强大的类库，为Intel和ATI用户提供硬解码的基础.
- 高清支持，可以顺畅的解码H264, VC-1

<strong>不能工作的部分:</strong>
- H264 with Level >= 5.1 (A卡驱动fglrx限制)

<strong>已知问题:</strong>
- A卡驱动fglrx在挂起和恢复时出错（并非xbmc-xvba错误）

<strong>我们未来将要做些什么:</strong>
- 推进 MPEG-2 (如果我们能联系上AMD)
- 使用H264 5.1 (如果AMD肯告诉我们方法)
译者注：凡是出问题，都出在AMD身上。

<strong>你需要:</strong>
- deb方式安装的A卡闭源驱动fglrx(amd catalyst) >= 11.11 (>=fglrx 2:8.911)

GIT 源:
<a href="https://github.com/FernetMenta/xbmc/commits/xvba" target="_blank">https://github.com/FernetMenta/xbmc/commits/xvba</a>

PA的Ubuntu源:
<a href="https://launchpad.net/~wsnipex/+archive/xbmc-xvba" target="_blank">https://launchpad.net/~wsnipex/+archive/xbmc-xvba</a>

<strong>NOTE:</strong>?窗口界面可能和XBMC不兼容(如 compiz, gnome-shell)
如果你有这个问题，请禁用Compiz，如果你还想用unity，你可以选择unity-2d.

你也应该在XBMC中将等待垂直同步开启：
XBMC - 系统 - 设置 - 视频输出
XBMC - system - settings - system - video output - Vsync - always

<span style="font-size: large;">怎样从头安装XBMC PVR Xvba</span>

<strong>第一步:</strong>
我们使用最小化安装后的64位 Ubuntu 11.10 Oneric做演示.
译者注：译者使用普通安装的64位Ubuntu 11.10 Oneric同样成功了，其他版本理论上均可成功安装。

选择命令行安装，并且使用xbmc作为用户名
译者注：这里使用xbmc做用户名是为了后边自动登录到xbmc做准备，选用其他名称无任何影响

重启之后，安装ssh，这样你就可以从其他终端登录到linux上了。同时，为了安装ppa源，我们也需要安装一些python包。最后，将xbmc添加到video和audio用户组。如果不进行这一步，没有启动x终端的用户将无法访问gpu资源，从而无法安装。本机操作直接按Ctrl+alt+F1进入命令行。

命令:

```bash
sudo apt-get update
sudo apt-get install ssh python-software-properties udisks upower xorg alsa-utils mesa-utils git-core librtmp0 lirc libmad0 lightdm
sudo adduser xbmc video
sudo adduser xbmc audio
#译者注：如果你没有使用xbmc作为用户名，这里请将xbmc替换为你的用户名
sudo reboot # 不确定是否需要重启，保险起见，重启一下吧
```

<strong>第二步:</strong>
我们需要安装最新的AMD/ATI闭源驱动 (截至译者翻译，最新版为 11.12).

现在安装一些依赖库

命令:
```bash
sudo apt-get install -y build-essential cdbs fakeroot dh-make debhelper debconf libstdc++6 dkms libqtgui4 wget execstack libelfg0 dh-modaliases
sudo apt-get install -y ia32-libs
```

下载并安装最新的AMD闭源驱动(fglrx)

命令:
```bash
cd ~; mkdir catalyst11.12; cd catalyst11.12
wget http://www2.ati.com/drivers/linux/ati-driver-installer-11-12-x86.x86_64.run
sudo sh ati-driver-installer-11-12-x86.x86_64.run --buildandinstallpkg
#译者注，这里有人可能会失败。原因是安装驱动的时候可能需要其他依赖。这里译者推荐先编译后手动安装。
#命令如下：
sudo sh ati-driver-installer-11-12-x86.x86_64.run --buildpkg
sudo dpkg -i *.deb
sudo apt-get install -f
#如果你已经成功运行之前的
#sudo sh ati-driver-installer-11-12-x86.x86_64.run --buildandinstallpkg
#命令，并且没有报错，以上三行命令无需重复进行。
#接着更新显卡设置
sudo aticonfig --initial -f
sudo aticonfig --sync-vsync=on

```

可选设置: 禁用underscan(黑边)

命令:
```bash
sudo aticonfig --set-pcs-val=MCIL,DigitalHDTVDefaultUnderscan,0
```
译者注：这个可选设置在译者两个笔记本上均无反应

<strong>第三步:</strong>
安装 PVR+XVBA build

命令:
```bash
sudo add-apt-repository ppa:wsnipex/xbmc-xvba
#不要脸的译者又来了=.=||：国人喜欢复制粘贴代码，这一步会提示你按回车确认导入证书，喜欢粘贴的伸手党请把后面的命令单独复制粘贴吧。
sudo apt-get update
sudo apt-get install xbmc xbmc-bin

```

&nbsp;

<span style="font-size: large;">译者的话</span>

由于本人实际环境与需求和原文有些许出入（本人正常安装带有图形界面的Ubuntu且不需要xbmc自启动），故后续xbmc自动登录部分未作翻译，读者如需自动登录，请访问原文参考操作。
<a href="http://forum.xbmc.org/showthread.php?t=116996">http://forum.xbmc.org/showthread.php?t=116996</a>

本文内容真实可用，译者亲测：
ASUS M51VA：ATI mobility HD3650
Acer 522：AMD C-50 APU

大老半夜辛辛苦苦翻译，如需转载请注明原文地址及本文地址。

asxzy <asxzy@asxzy.net>
2012年1月3日
