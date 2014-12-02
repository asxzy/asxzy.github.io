---
layout: post
title: LAMP\LNMP\LNAMP性能大比拼
date: '2011-6-1'
comments: true
---
测试结果出来了。。

先上个大概结论

单纯从php上来说
phpcgi解析速度和apache基本持平。
但是apache远比phpcgi稳定。

php-cgi在170并发下第一次出错，400并发就狂报错

apache在450鬓发下第一次出错，且出错概率万分之一。之后再出错过。

370以上php-cgi全崩溃
500以上apache全崩溃

内存上暂时没有详细的统计数据，不过从零散的统计上来看，apache比phpcgi要多用200m左右。 


并发上。。纯html，nginx，12000，apache8000.nginx一次报错都没有。apache4000以上开始报错。。 



个人感觉lnamp平台可行。 
稳定的多 


更加详尽的数据等过两天整理好了做图对比。
