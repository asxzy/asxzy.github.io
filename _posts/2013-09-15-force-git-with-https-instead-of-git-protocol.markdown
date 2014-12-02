---
layout: post
title: "git中强制使用https取代git协议"
date: 2013-09-15 12:47
comments: true
categories: 
---

实验室电脑在一个诡异的防火墙及代理网关之后，导致使用git时经常无法连接git协议。但https访问却正常。git设计的时候已经考虑到了这些问题，在实际使用过程中，可以将https配置为默认协议。命令很简单：

```bash
git config--global url."https://".inseadOf git://
```

命令输入之后，你的.gitconfig文件里就会多出以下两行
```
[url "https://"]
    insteadOf = git:
```

这样在某些无法访问git协议的环境中也可以正常的clone了。
