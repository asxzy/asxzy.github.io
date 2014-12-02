---
layout: post
title: "ipv6的proxy_ndp自动部署脚本"
date: '2011-12-2'
comments: true
---

思路：
在路由器上获取arp表中的客户端网卡mac地址，并将mac地址计算为ipv6地址，分别添加路由和邻居发现代理

依赖：
Linux > 2.6.19
ip，grep，sed，awk，radvd（用于分配ipv6地址）

实现：

```bash
# This script auto configure ipv6_proxy_ndp
#
# @author: asxzy<asxzy@asxzy.net>
#                                            -> yes -> maintan ->
# config -> get arp list -> get neigh list -|                    |-> add new client to the neigh
#                                            --------> no ----- >

# config
PREFIX='2001:250:1006:3006'
ROUTER='2001:250:1006:3006::1'
WAN='eth1'
LAN='br-lan'

# get the client list
ARP=$(cat /proc/net/arp | grep 'br-lan' | awk '{print $4}' | sed -e "s/://g" | awk 'BEGIN{FS=""}{if($1>0){print $1}if($2==8){print "a"}else if($2==9){print "b"}else if($2==12){print "e"}else if($2==13){print "f"}else if($2==14){print "c"}else if($2==15){print "d"}else if($2==2||$2==3||$2==6||$2==7||$2==10||$2==11){print $2-2}else{print $2+2}}' | sed -e "s/^/${PREFIX}:/")

# check the pid and ipv6 route
COUNT=0
NEW=''
if [ ! -f /tmp/ipv6.pid || $(ip -6 route | grep ${ROUTER} -c) -ne 0 ]
then
        # add the default route
        ip -6 route add default via ${ROUTER} dev ${WAN}
        # add new client to the neigh & route list
        for i in ${ARP}
        do
                ip -6 neigh add proxy $i dev ${WAN}
                ip -6 route add $i dev ${LAN}
        done
else
        # check list
        for i in ${ARP}
        do
                if [ $(cat /tmp/ipv6.pid | grep ${i} -c) -ne 0 ]
                then
                        # add new client to the neigh & route list
                        ip -6 neigh add proxy $i dev ${WAN}
                        ip -6 route add $i dev ${LAN}
                else
                        # make a disconnected-client list
                        sed -i "/$i/d" /tmp/ipv6.pid
                fi
        done
        # del discontected-client from the list
        for i in `cat /tmp/ipv6.pid`
        do
                ip -6 neigh del proxy $i dev ${WAN}
                ip -6 route del $i dev ${LAN}
        done
fi

# write client list into pid
echo ${ARP} > /tmp/ipv6.pid
```


测试阶段，<del>windows有待验证。</del>，由于添加的ipv6地址为mac计算所得，windows NT6以上必须关闭随机ipv6地址生成功能才能使用该脚本
