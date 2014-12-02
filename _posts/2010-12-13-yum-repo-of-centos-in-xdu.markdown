---
layout: post
title: 西电CentOS5.6更新源
date: '2010-12-13'
comments: true
---
```bash
# CentOS-Base.repo
#
# This file uses a new mirrorlist system developed by Lance Davis for CentOS.
# The mirror system uses the connecting IP address of the client and the
# update status of each mirror to pick mirrors that are updated to and
# geographically close to the client. You should use this for CentOS updates
# unless you are manually picking other mirrors.
#
# If the mirrorlist= does not work for you, as a fall back you can try the
# remarked out baseurl= line instead.
#
#

[base]
name=CentOS-$releasever - Base
baseurl=ftp://linux.xidian.edu.cn/centos/5.6/os/$basearch/
gpgcheck=1
gpgkey=ftp://linux.xidian.edu.cn/centos/RPM-GPG-KEY-CentOS-5

#released updates
[updates]
name=CentOS-$releasever - Updates
baseurl=ftp://linux.xidian.edu.cn/centos/5.6/updates/$basearch/
gpgcheck=1
gpgkey=ftp://linux.xidian.edu.cn/centos/RPM-GPG-KEY-CentOS-5

#packages used/produced in the build but not released
[addons]
name=CentOS-$releasever - Addons
baseurl=ftp://linux.xidian.edu.cn/centos/5.6/addons/$basearch/
gpgcheck=1
gpgkey=ftp://linux.xidian.edu.cn/centos/RPM-GPG-KEY-CentOS-5

#additional packages that may be useful
[extras]
name=CentOS-$releasever - Extras
baseurl=ftp://linux.xidian.edu.cn/centos/5.6/extras/$basearch/
gpgcheck=1
gpgkey=ftp://linux.xidian.edu.cn/centos/RPM-GPG-KEY-CentOS-5

#additional packages that extend functionality of existing packages
[centosplus]
name=CentOS-$releasever - Plus
baseurl=ftp://linux.xidian.edu.cn/centos/5.6/centosplus/$basearch/
gpgcheck=1
enabled=0
gpgkey=ftp://linux.xidian.edu.cn/centos/RPM-GPG-KEY-CentOS-5
```