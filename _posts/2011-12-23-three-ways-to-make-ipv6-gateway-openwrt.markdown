---
layout: post
title: "单一IPV6地址做网关的三种方法之OpenWrt篇"
date: '2011-12-23'
comments: true
---
方案一：NAT

NAPT66已经做得很好了，就不多介绍了。
NAPT66：http://code.google.com/p/napt66/

方案二：IPv4 NAT + IPv6 bridge
openwrt的trunk版提供了6scripts包可以使用该方法实现ipv6。
操作
```
opkg update
opkg install ebtables 6scripts
```
编辑配置文件/etc/config/6bridge
```
vi /etc/config/6bridge
```
修改配置文件
```
config 6bridge
option bridge 'bripv6' # 将bripv6修改为你的bridge设备名，通过brctl show查看
```
启用脚本
```
/etc/init.d/6bridge start
```
设置开机自启动
```
/etc/init.d/6bridge enable
```
但实际上，在某些环境下，这种方法还是有缺陷的。比如需要IPv4通过交换机验证的环境中，由于客户端没有通过联网验证，上端路由器不会相应来自客户端的任何请求，故本方案只是用于IPv6无需认证的网络环境使用。

<strong>NOTE:</strong> 6script依赖ebtables包，<del>该软件包只有trunk版提供，backfire版无ebtables</del>，12.09之后，非trunk版也提供ebtables与6script.

方案三：proxy_ndp

<del datetime="2013-04-19T20:20:51+00:00">npd6 <http://code.google.com/p/npd6/>
npd6是一款可以自动配置npd proxy的软件，短小精悍，配置简洁，老少皆宜。。</del>
npd6可以使用ndppd代替，该包已经被openwrt官方trunk版收录

开始openwrt下的配置吧
安装radvd，给客户端分配合法ip
```
opkg update
opkg install radvd
```
编辑配置文件/etc/config/radvd
前两个配置项的ignore去掉，prefix项中的list prefix填写正确的prefix即可：
```
vi /etc/config/radvd
```
```
config interface
option interface 'lan'
option AdvSendAdvert 1
option AdvManagedFlag 0
option AdvOtherConfigFlag 0
list client ''

config prefix
option interface 'lan'
# If not specified, a non-link-local prefix of the interface is used
list prefix '2001:250:1006:3006::/64'
option AdvOnLink 1
option AdvAutonomous 1
option AdvRouterAddr 0
```
启动radvd
```
/etc/init.d/radvd start
```
设置开机自启动
```
/etc/init.d/radvd enable
```
<strong>此处更新（2013/4/19）</strong>
此文发布已久，现发现npd6可以使用openwrt官方trunk版的ndppd包代替，安装及配置方法如下
安装ndppd包
```
opkg install ndppd
```
配置ndppd
```
vim /etc/ndppd.conf
```
找到配置文件中的proxy标签和rule标签，设置成你的内网网段：
```
proxy eth1{
	router yes
	timeout 500
	ttl 30000

	rule2001:250:1006:3006::/64 {
	auto
	}
}
```
开启ndppd
```
/etc/init.d/ndppd start
```
设置ndppd为开机自启动
```
/etc/init.d/ndppd enable
```





NOTE：在启用<del datetime="2013-04-19T20:20:51+00:00">npd6</del>ndppd之前，要给路由器设定固定的ipv6地址，否则路由器会向上端路由发送请求自动获取ip，br-lan和wan口均会获得prefix为/64的ipv6地址，导致路由表错乱。
编辑配置/etc/config/network
```
vi /etc/config/network
```
```
config interface lan
option type bridge
option ifname eth1.0
option proto static
option ipaddr 10.0.0.1
option netmask 255.255.255.0
option ip6addr '2001:250:1006:3006::4/64'
option nat 1

config interface wan
option ifname eth1.1
option proto static
option ipaddr XXX.XXX.XXX.XXX #你的ipv4地址
option netmask 255.255.255.0
option gateway XXX.XXX.XXX.XXX #你的网关地址
option dns '2001:470:20::2 74.82.42.42' #dns服务器
option ip6addr '2001:250:1006:3006::3/126' #ipv6地址，注意prefix，prefix相同会导致路由表错乱
option ip6gw '2001:250:1006:3006::1 #你的ipv6网关地址
```
重启network
```
/etc/init.d/network restart
```
<del datetime="2013-04-19T20:20:51+00:00">之后启动npd6</del>

子网客户端上用浏览器开ipv6.google.com，可以打开就说明ok了。

注意事项：
lan口wan口必须设定ipv6地址，且不能使用同一prefix，否则会导致路由表错乱。<!--:--><!--:en-->方案一：NAT

NAPT66已经做得很好了，就不多介绍了。
NAPT66：http://code.google.com/p/napt66/

方案二：IPv4 NAT + IPv6 bridge
openwrt的trunk版提供了6scripts包可以使用该方法实现ipv6。
操作
```
opkg update
opkg install ebtables 6scripts
```
编辑配置文件/etc/config/6bridge
```
vi /etc/config/6bridge
```
修改配置文件
```
config 6bridge
option bridge 'bripv6' # 将bripv6修改为你的bridge设备名，通过brctl show查看
```
启用脚本
```
/etc/init.d/6bridge start
```
设置开机自启动
```
/etc/init.d/6bridge enable
```
但实际上，在某些环境下，这种方法还是有缺陷的。比如需要IPv4通过交换机验证的环境中，由于客户端没有通过联网验证，上端路由器不会相应来自客户端的任何请求，故本方案只是用于IPv6无需认证的网络环境使用。

NOTE:6script依赖ebtables包，该软件包只有trunk版提供，backfire版无ebtables

方案三：proxy_ndp

npd6 <http://code.google.com/p/npd6/>
npd6是一款可以自动配置npd proxy的软件，短小精悍，配置简洁，老少皆宜。。

开始openwrt下的配置吧
安装radvd，给客户端分配合法ip
```
opkg update
opkg install radvd
```
编辑配置文件/etc/config/radvd
前两个配置项的ignore去掉，prefix项中的list prefix填写正确的prefix即可：
```
vi /etc/config/radvd
```
```
config interface
option interface 'lan'
option AdvSendAdvert 1
option AdvManagedFlag 0
option AdvOtherConfigFlag 0
list client ''

config prefix
option interface 'lan'
# If not specified, a non-link-local prefix of the interface is used
list prefix '2001:250:1006:3006::/64'
option AdvOnLink 1
option AdvAutonomous 1
option AdvRouterAddr 0
```
启动radvd
```
/etc/init.d/radvd start
```
设置开机自启动
```
/etc/init.d/radvd enable
```
<strong>此处更新（2013/4/19）</strong>
此文发布已久，现发现npd6可以使用openwrt官方trunk版的ndppd包代替，安装及配置方法如下
安装ndppd包
```
opkg install ndppd
```
配置ndppd
```
vim /etc/ndppd.conf
```
找到配置文件中的proxy标签和rule标签，设置成你的内网网段：
```
proxy eth1{
router yes
timeout 500
ttl 30000

rule2001:250:1006:3006::/64 {
auto
}
}
```
开启ndppd
```
/etc/init.d/ndppd start
```
设置ndppd为开机自启动
```
/etc/init.d/ndppd enable
```
<del datetime="2013-04-19T20:11:58+00:00">安装对应路由器的npd6，通过简单的配置即可。
软件包请自行在我的服务器上找
http://openwrt.asxzy.net
以brcm为例（有这个芯片的基友们太多了 -。-！）
```
opkg install http://openwrt.asxzy.net/backfire/10.03.1/brcm63xx/packages/npd6_0.4.4-1_brcm63xx.ipk
```
编辑配置文件/etc/npd6.conf
```
vi /etc/npd6.conf
```
```
prefix = 2001:250:1006:3006:
interface = eth1 #这里要写WAN网卡，我的是eth1，具体可以ifconfig或者cat /etc/config/network查看
```</del>




NOTE：在启用npd6之前，要给路由器设定固定的ipv6地址，否则路由器会向上端路由发送请求自动获取ip，br-lan和wan口均会获得prefix为/64的ipv6地址，导致路由表错乱。
编辑配置/etc/config/network
```
vi /etc/config/network
```
```
config interface lan
option type bridge
option ifname eth1.0
option proto static
option ipaddr 10.0.0.1
option netmask 255.255.255.0
option ip6addr '2001:250:1006:3006::4/64'
option nat 1

config interface wan
option ifname eth1.1
option proto static
option ipaddr XXX.XXX.XXX.XXX #你的ipv4地址
option netmask 255.255.255.0
option gateway XXX.XXX.XXX.XXX #你的网关地址
option dns '2001:470:20::2 74.82.42.42' #dns服务器
option ip6addr '2001:250:1006:3006::3/126' #ipv6地址，注意prefix，prefix相同会导致路由表错乱
option ip6gw '2001:250:1006:3006::1 #你的ipv6网关地址
```
重启network
```
/etc/init.d/network restart
```
之后启动npd6
```
npd6
```
子网客户端上用浏览器开ipv6.google.com，可以打开就说明ok了。

注意事项：
lan口wan口必须设定ipv6地址，且不能使用同一prefix，否则会导致路由表错乱。
