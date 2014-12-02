---
layout: post
title: "关闭windows nt6.0以上内核的ipv6自动配置随机接口功能"
date: '2011-12-6'
comments: true
---

实验室需要使用npd代理实现ipv6路由，由于windows自动配置使用的地址是随机生成，导致无法正常获取windows下ipv6地址。临时ipv6地址也会对网络形成一定干扰。于是在cmd中输入以下命令即可关闭随机接口和临时IPv6，使用EUI-64标准地址。
```bash
netsh interface ipv6 set global randomizeidentifiers=disabled
netsh interface ipv6 set privacy state=disable
```

