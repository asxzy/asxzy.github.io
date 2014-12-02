---
layout: post
title: 最大流算法之一——福特富尔克森方法
date: '2013-4-20'
comments: true
---
最近在复习Dr. Tsin的03-060554 Advance Algorithm，其中最大流的算法一直迷迷糊糊，索性边学边写，记录下来。

问题：
在图论中，网络流 (Network Flow) 是指在一个每条边都有容量 (Capacity) 的有向图分配流，使一条边的流量不会超过它的容量。（边有附带容量的图称为网络。）一道流必须符合一个结点的进出的流量相同的限制，除非这是一个源点 (Source) ──有较多向外的流，或是一个汇点 (Sink) ──有较多向内的流。一个网络可以用来模拟道路系统的交通量、管中的液体、电路中的电流或类似一些东西在一个结点 (Node) 的网络中游动的任何事物。

最大流问题即在该网络汇总，流量从A到B，如何选择路径、分配经过路径的流量可以达到总流量最大的要求。

计算最大流最基本的方法是福特富尔克森方法（The Ford-Fulkerson method）、埃德蒙兹卡普算法（The Edmonds-Karp algorithm）

福特富尔克森方法（The Ford-Fulkerson method）:
Ford-Fulkerson方法依赖于三种重要思想：残留网络，增广路径和割。
Ford-Fulkerson方法是一种迭代的方法。开始时，对所有的u，v∈V有f(u,v)=0，即初始状态时流的值为0。
在每次迭代中，可通过寻找一条“增广路径”来增加流值。增广路径可以看成是从源点s到汇点t之间的一条路径，沿该路径可以压入更多的流，从而增加流的值。
反复进行这一过程，直至增广路径都被找出来，根据最大流最小割定理，当不包含增广路径时，f是G中的一个最大流。
在算法导论中给出的Ford-Fulkerson实现代码如下：

FORD_FULKERSON(G,s,t)
```
for each edge(u,v)∈E[G]
     do f[u,v] <— 0
         f[v,u] <— 0
while there exists a path p from s to t in the residual network Gf
     do cf(p) <— min{ cf(u,v) : (u,v) is in p }
     for each edge(u,v) in p
         do f[u,v] <— f[u,v]+cf(p)         //对于在增广路径上的正向的边，加上增加的流
             f[v,u] <— -f[u,v]                //对于反向的边，根据反对称性求
```
相比于代码，我更喜欢用数据流来表示和理解一个算法。

![](/uploads/2013/04/1.png)
![](/uploads/2013/04/2.png)
![](/uploads/2013/04/3.png)
![](/uploads/2013/04/4.png)
![](/uploads/2013/04/5.png)
![](/uploads/2013/04/6.png)
![](/uploads/2013/04/7.png)
![](/uploads/2013/04/8.png)
![](/uploads/2013/04/9.png)
![](/uploads/2013/04/10.png)
![](/uploads/2013/04/11.png)
![](/uploads/2013/04/12.png)
![](/uploads/2013/04/13.png)
![](/uploads/2013/04/14.png)
![](/uploads/2013/04/15.png)

伪码及配图来自于互联网。