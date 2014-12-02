---
layout: post
title: CentOS上安装NFS
date: '2010-12-13'
comments: true
---
系统环境
192.168.137.100
192.168.137.101
192.168.137.102所有系统均为CentOS5.5

我懒...所以用yum安装了.

服务端:
```bash
yum install nfs* -y
```

安装好之后修改配置文件
vi /etc/exports/data 192.168.137.101(rw,sync,fsid=0) 192.168.137.102(rw,sync,fsid=0)
[共享的目录] [主机名1或IP1(参数1,参数2)] [主机名2或IP2(参数3,参数4)]
下面是一些NFS共享的常用参数：

ro                      只读访问
rw                      读写访问
sync                    所有数据在请求时写入共享
async                   NFS在写入数据前可以相应请求
secure                  NFS通过1024以下的安全TCP/IP端口发送
insecure                NFS通过1024以上的端口发送
wdelay                  如果多个用户要写入NFS目录，则归组写入（默认）
no_wdelay               如果多个用户要写入NFS目录，则立即写入，当使用async时，无需此设置。
hide                    在NFS共享目录中不共享其子目录
no_hide                 共享NFS目录的子目录
subtree_check           如果共享/usr/bin之类的子目录时，强制NFS检查父目录的权限（默认）
no_subtree_check        和上面相对，不检查父目录权限
all_squash              共享文件的UID和GID映射匿名用户anonymous，适合公用目录。
no_all_squash           保留共享文件的UID和GID（默认）
root_squash             root用户的所有请求映射成如anonymous用户一样的权限（默认）
no_root_squash          root用户具有根目录的完全管理访问权限
anonuid=xxx             指定NFS服务器/etc/passwd文件中匿名用户的UID
anongid=xxx             指定NFS服务器/etc/passwd文件中匿名用户的GID

然后设定开启自启动
chkconfig portmap on
chkconfig nfs on之后启动服务
service portmap start
service nfs start
之后检查一下

showmount -e 192.168.137.100显示
Export list for 192.168.137.100:
/data 192.168.137.102,192.168.137.101好了..服务端配置好了..

在客户端
yum install nfs* -y然后设定开启自启动
chkconfig portmap on之后启动服务
service portmap start之后再客户端mount一下.

mount -t nfs 192.168.137.100:/data /data随便写几个文件测试一下..收工
