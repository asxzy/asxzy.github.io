---
layout: post
title: LAMP？？LNMP？？LNAMP？？
date: '2011-4-2'
comments: true
---
今天睿思各种502，引发了我对目前这种架构的稳定性的怀疑。

最早睿思是采用Linux+Lighttpd+PHP+MySQL这种传统架构，虽然说高峰期会非常非常卡，但也算是比较稳定。

一年前张宴大师的<a href="http://blog.s135.com/nginx_php_v6/">Nginx 0.8.x + PHP 5.2.13（FastCGI）搭建胜过Apache十倍的Web服务器（第6版）[原创]</a>之后，决定采用LNMP架构（Linux+Nginx+PHP（FastCGI）+MySQL），运行速度确实快了不少，但问题也接踵而至，先是大量的502，打开文件数超过了系统限制。再经历了井喷式的发展之后，这种架构的劣势也日益凸显。其最大的缺点就是不稳定，大量的php进程变成了僵尸进程，系统的wa飙升。如何在不添加服务器的情况下，提升服务器的稳定性，成了我们要解决的首要问题。

最近和聪哥交流了几次，推荐使用LNAMP架构（Linux+Nginx+Apache+PHP+MySQL），Nginx做前端均衡负载，处理静态内容，Apache处理php页面，既保留了Nginx的高并发，处理静态内容速度快等优势，也保证了php的稳定性，各自发挥其优势。。

初步确定要采用最后一种方案，但是否稳定，性能能否达标，还需进行一些测试之后才能决定。

PS：据聪哥说，可能还要做LVS，但具体情况还不是很清楚，我也得加紧看LVS方面的东西了。。
