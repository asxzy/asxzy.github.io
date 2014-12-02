---
layout: post
title: CentOS最小化安装之后wget和setup的解决
date: '2010-12-13'
comments: true
---
通过linux text最小化安装后出现的问题是wget命令不能使用了，这时可以使用rpm命令来安装wget。

rpm -ivh http://centos.ustc.edu.cn/centos/5.5/os/i386/CentOS/wget-1.11.4-2.el5_4.1.i386.rpm

rpm -ivh ftp://linux.xidian.edu.cn/centos/5.5/os/x86_64/CentOS/wget-1.11.4-2.el5_4.1.x86_64.rpm
注：这是最新版本。
执行上面的操作以后wget就可以使用了，现在就可以修改源了。

cd /etc/yum.repos.d
mv CentOS-Base.repo CentOS-Base.repo.save西电学生可以看这里//?p=70，用西电的源。
wget http://centos.ustc.edu.cn/CentOS-Base.repo.5
mv CentOS-Base.repo.5 CentOS-Base.repo
rpm --import http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-5
yum update完成，上面每行一回车。

更新完系统后就可以安装常用的基本工具了。
yum install setuptool ntsysv system-config-network system-config-keyboard ntp crontabs wget vim-enhanced
完成。至此基本的功能已经完成了，还有一些工具可以使用此方法装，在此就不操作了。
