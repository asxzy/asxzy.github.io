---
layout: post
title: windows7下访问samba密码错误解决方法
date: '2011-6-30'
comments: true
---
用windows上访问linux的共享目录
回到windows，打开“网络”（我用的是win7以前这个东西叫网上邻居），在地址栏输入\\\\linux ip 比如，\\\\192.168.100.13 ，根本找不到?!
有搜索了老半天，好在这个问题还是很普遍的，关闭linux的防火墙：#service iptables stop。
终于可以找到linux了……
可是更纠结的问题出现了，总提示用户名和密码总是不对。用户名应该是上面再samba图像配置里面的设置的windows用户，密码也是那里设置的密码。可是就是不对。
有时一阵狂搜，终于找到了问题的所在。
下面可以解决的方法：

单击[开始]——[运行] 输入 “secpol.msc”打开管理工具，展开“本地策略”；
然后，单击“安全选项”。 双击“网络安全：LAN Manager 身份验证级别”；
最后，单击列表中：发送LM和NTLMv2，如果已协商，则使用NTLMv2协议。


链接网址：[](http://blog.chinaunix.net/u3/94191/showart_2228653.html)。出现这个问题的原因这篇文章里也给出了答案。
