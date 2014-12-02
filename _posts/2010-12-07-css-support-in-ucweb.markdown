---
layout: post
title: 【转】UCWEB对css样式的支持(S60 V3 V7.1.0.42)
date: '2010-12-7'
comments: true
---
最近手头的项目就是WAP的改版，之前的版本也对UCWEB进行过专门的适配，为了适应UCWEB，有些效果进行了调整。最新UCWEB的版本更新到V7.1.0.42,所以有些样式又不支持了。但是用andriod平台下的ucweb，这个解析就相当好，大家有条件的话可以作自行测试。下面例举一些日常工作中碰到的问题，希望对大家有用：

1、传统的TAB做法会换行，如像koubei网的。
![](/uploads/2010/12/111-300x165.jpg)

代码如下：

<div id=”nav”>
<p>
<a href=”/store.do?m=index&sid=9b4a753e-90ab-49fb-9418-3ebe990913d7″>美食娱乐</a>
<a href=”/bar.do?m=index&sid=9b4a753e-90ab-49fb-9418-3ebe990913d7″>点评吧</a>
<a href=”/info.do?m=index&sid=9b4a753e-90ab-49fb-9418-3ebe990913d7″>生活资讯</a>
</p>
</div>

解决方法：用table td将每个A定位<td><a>美食</a></td>要解决换行，虽然效果不是很好，但是只能这样，效果可以参考图2，至少不会换行，又解决了当然选项卡的定位。

2、网上有文章说UCWEB不支持粗体<strong>font-weight:bold;</strong>的样式，在此版本中是支持的，大家可以看上图中的<strong>首页</strong>两字就是粗体的。

3、图片左右排会比较麻烦，有时候正常，有时候却不正常，好像无法解析width，见下面图文左右排的样式，右边的文字明显向右靠了。大家请参考淘宝的列表页面，好像是解析错误，不知是不是淘宝进行了特殊处理，我曾经把淘宝的源码复制传到我空间里去，但解析出来的就是显示不正常，苦恼。
![](/uploads/2010/12/2222-300x165.jpg)

4、UCWEB支持<strong>text-align:center</strong>的CSS样式，但是不支持<strong>text-align:right;</strong>因些想把更多放在标题的右侧就要换个办法了，还是只能用TABLE。

5、UCWEB对于<strong>padding</strong>，<strong>margin</strong>都不支持，如果想弄个间距什么的，就要另想办法好了。

6、关于INPUT强制一行的解析，这个是相当痛苦的事情，大家可以参考淘宝的WAP站的做法，在UC下的解析还是比较满意的，至少我做的时候，都是如网上文章所述都是强制占一行的，因此还特意更改了了分页的形式，把输入页码跳转的功能去掉了。
![](/uploads/2010/12/taobao-300x165.jpg)

7、UCWEB支付<strong>border</strong>的样式，特别是对<strong>.cate td{border:1px solid #ddd}</strong>这样的样式定义也支持不错。

8、对普通按钮的处理：UC中对<strong><a href=”#” style=”color:#fff; background:#FF0000″>这是测试效果</a></strong>这样的解析也是默认一行的，解决的方案:

第一种方法:用<strong>form</strong>,把按钮作成<strong>submit</strong>，把链接放在action里，但是UCWEB不支持自定义<strong>button</strong>,系统会调用UCWEB自带的button样式。此方法不是很好。

第二种方法就是用图片。但是一图片尺寸大，二是不利于后期维护，修改文字、样式的时候需要修改图片。

以上只是工作上遇到的一些问题，我会不断完善，上面的问题仅限S60 V3 V7.1.0.42，我们希望UCWEB对CSS的支持越来越好，以减少我们的痛苦。也希望大家共同探讨更好的解决方案。
