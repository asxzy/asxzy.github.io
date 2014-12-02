---
layout: post
title: 完美解决Linux（Ubuntu）下chromium（chrome）中文显示问题
date: '2012-1-4'
comments: true
---
通过一天的摸索，终于知道了字体在Linux下的运行机制。通过一定的技巧，可以打造和几乎和windows下一模一样的显示效果。如图（点击打开大图）

![](/uploads/2012/01/windows.png)

![](/uploads/2012/01/ubuntu.png)

图一为windows下的显示效果，默认字体为宋体。
图二为ubuntu下的显示效果，默认字体为微软雅黑。

还看的过去吧。

Linux下Chromium（chrome）的显示一直是个饱受诟病的问题，大家各种方法工具一起上，现在网上提供的主要方法为：
1.删楷体+改系统字体
2.设置里改字体。
3.启动器的命令里加上"-disable-tabbed-options"，在任意输入框右键拼写检查选项-。。。。。。。。。。。（真的很佩服能找到这种方法的人）。

以上方法均能使chromium（chrome）显示用户指定的字体，但问题来了。用户只能指定一个字体作为网页显示的字体，这样有悖设计师初衷，比如有的设计师需要使用大于17px的中文作标题，宋体显然不能满足需求，设计师将其指定为楷体或其他矢量字体，以便提高显示效果。在这种情况下，以上方法均会使网页变形。

反观firefox，firefox可以使用系统默认字体作为渲染网页的字体，这是为什么呢，我们来看看firefox的配置吧。

![](/uploads/2012/01/Screenshot-2012-01-04-184249.png "firefox下字体设置" )

在语言编码栏选中简体中文后，firefox的默认配置：
比例字体默认为无衬线字体，继承第三个选项
衬线字体为serif
无衬线字体为sans-serif
等宽字体为monospace

这里普及一个知识，以上三种字体中的选项并非是一种特定的字体，而是通用字体。何为通用字体，这个解释起来就很麻烦了，要回归W3C标准才能知道，简短的介绍在这里：<a href="http://www.w3school.com.cn/css/css_font-family.asp">http://www.w3school.com.cn/css/css_font-family.asp</a>

再简单点说，以上三种字体，均代表系统默认字体。即

衬线字体选择serif，使用系统默认的衬线字体。
无衬线字体选择sans-serif，使用系统默认的无衬线字体。
等宽字体选择monospace， 使用系统默认的等宽字体。

又有童鞋问了，衬线、无衬线和等宽，这三个有什么区别，这个要到印刷学去查明原因了。

serif，衬线字：字体末端带着小小勾，主要应用于印刷物，如报纸。其特点是字号小（印刷省钱），远处看还是为一条直线，因为带勾，阅读时不会因为字体过小而串行。
sans-serif，无衬线字：字体末端不带勾，比衬衫字大，适合屏幕显示。
monospace，等宽字体：字体宽度相等，主要用于显示代码和对齐排版。

言归正传，回到firefox的配置文件上来。

通过察看配置，一切真相大白。原来firefox并没有设置字体，而是老老实实的继承了系统字体设置。

&nbsp;

chromium（chrome）就不一样了，Linux下的chromium（chrome）默认字体并不继承系统字体。

又有童鞋说了，和firefox一样，在配置文件中改成继承系统字体呗，于是乎大家开始找，好不容易在字体的下拉菜单中找到了一个Sans，找到了个Monospace，选之。。。

悲剧就是从这里开始的，你应该记得，Linux是区分大小写的吧，事实上，Sans和Monospace是两中特定的字体，并非通用字体选项。

有的读者这时候会叫，搞毛线啊，转了一圈还是不能设置？
等我说完嘛。

配置项里虽然无法选择通用字体，但是，他的配置总会保存在某一处吧。找到他，暴力改之。这个文件位于~/.config/chromium/Default/Preferences（这个是chromium的目录，chrome理论上把chromium改为chrome即可，没条件验证，有的朋友帮忙看下是不是这个文件）

首先，关闭所有正在运行的chromium（chrome）。之后用你最喜欢的编辑器打开配置文件，编辑之。我这里用vim

```bash
vim ~/.config/chromium/Default/Preferences
```
按shift+g转到文件末尾处
你会看到这些东西
```
"webkit": {
"webprefs": {
"global": {
"fixed_font_family": "monospace",
"sansserif_font_family": "scans",
"serif_font_family": "scans-serif",
"standard_font_family": "scans"
},
"uses_universal_detector": true
}
}
```
font_family，常写css的童鞋是不是感觉很亲切呢。这里就是字体设置了，把他改的和我上边内容一样就行了。如图
![](/uploads/2012/01/Screenshot-2012-01-04-190845.png)

好了，现在启动chromium（chrome），随便打开一个网页，难看的楷体消失了。

&nbsp;

好了，搞定了，就这么简单。说了这么多，完全是为了抛砖引玉，单纯的贴代码没啥意思，代码是思想的体现。有思想的程序猿才能进化嘛。就这样啦。。<!--:--><!--:en-->通过一天的摸索，终于知道了字体在Linux下的运行机制。通过一定的技巧，可以打造和几乎和windows下一模一样的显示效果。如图（点击打开大图）

![](/uploads/2012/01/windows.png)

![](/uploads/2012/01/ubuntu.png)

图一为windows下的显示效果，默认字体为宋体。
图二为ubuntu下的显示效果，默认字体为微软雅黑。

还看的过去吧。

Linux下Chromium（chrome）的显示一直是个饱受诟病的问题，大家各种方法工具一起上，现在网上提供的主要方法为：
1.删楷体+改系统字体
2.设置里改字体。
3.启动器的命令里加上"-disable-tabbed-options"，在任意输入框右键拼写检查选项-。。。。。。。。。。。（真的很佩服能找到这种方法的人）。

以上方法均能使chromium（chrome）显示用户指定的字体，但问题来了。用户只能指定一个字体作为网页显示的字体，这样有悖设计师初衷，比如有的设计师需要使用大于17px的中文作标题，宋体显然不能满足需求，设计师将其指定为楷体或其他矢量字体，以便提高显示效果。在这种情况下，以上方法均会使网页变形。

反观firefox，firefox可以使用系统默认字体作为渲染网页的字体，这是为什么呢，我们来看看firefox的配置吧。

![](/uploads/2012/01/Screenshot-2012-01-04-184249.png "firefox下字体设置")

在语言编码栏选中简体中文后，firefox的默认配置：
比例字体默认为无衬线字体，继承第三个选项
衬线字体为serif
无衬线字体为sans-serif
等宽字体为monospace

这里普及一个知识，以上三种字体中的选项并非是一种特定的字体，而是通用字体。何为通用字体，这个解释起来就很麻烦了，要回归W3C标准才能知道，简短的介绍在这里：<a href="http://www.w3school.com.cn/css/css_font-family.asp">http://www.w3school.com.cn/css/css_font-family.asp</a>

再简单点说，以上三种字体，均代表系统默认字体。即

衬线字体选择serif，使用系统默认的衬线字体。
无衬线字体选择sans-serif，使用系统默认的无衬线字体。
等宽字体选择monospace， 使用系统默认的等宽字体。

又有童鞋问了，衬线、无衬线和等宽，这三个有什么区别，这个要到印刷学去查明原因了。

serif，衬线字：字体末端带着小小勾，主要应用于印刷物，如报纸。其特点是字号小（印刷省钱），远处看还是为一条直线，因为带勾，阅读时不会因为字体过小而串行。
sans-serif，无衬线字：字体末端不带勾，比衬衫字大，适合屏幕显示。
monospace，等宽字体：字体宽度相等，主要用于显示代码和对齐排版。

言归正传，回到firefox的配置文件上来。

通过察看配置，一切真相大白。原来firefox并没有设置字体，而是老老实实的继承了系统字体设置。

&nbsp;

chromium（chrome）就不一样了，Linux下的chromium（chrome）默认字体并不继承系统字体。

又有童鞋说了，和firefox一样，在配置文件中改成继承系统字体呗，于是乎大家开始找，好不容易在字体的下拉菜单中找到了一个Sans，找到了个Monospace，选之。。。

悲剧就是从这里开始的，你应该记得，Linux是区分大小写的吧，事实上，Sans和Monospace是两中特定的字体，并非通用字体选项。

有的读者这时候会叫，搞毛线啊，转了一圈还是不能设置？
等我说完嘛。

配置项里虽然无法选择通用字体，但是，他的配置总会保存在某一处吧。找到他，暴力改之。这个文件位于~/.config/chromium/Default/Preferences（这个是chromium的目录，chrome理论上把chromium改为chrome即可，没条件验证，有的朋友帮忙看下是不是这个文件）

首先，关闭所有正在运行的chromium（chrome）。之后用你最喜欢的编辑器打开配置文件，编辑之。我这里用vim

```bash
vim ~/.config/chromium/Default/Preferences
```
按shift+g转到文件末尾处
你会看到这些东西
```
"webkit": {
"webprefs": {
"global": {
"fixed_font_family": "monospace",
"sansserif_font_family": "scans",
"serif_font_family": "scans-serif",
"standard_font_family": "scans"
},
"uses_universal_detector": true
}
}
```
font_family，常写css的童鞋是不是感觉很亲切呢。这里就是字体设置了，把他改的和我上边内容一样就行了。如图
![](/uploads/2012/01/Screenshot-2012-01-04-190845.png)

好了，现在启动chromium（chrome），随便打开一个网页，难看的楷体消失了。

&nbsp;

好了，搞定了，就这么简单。说了这么多，完全是为了抛砖引玉，单纯的贴代码没啥意思，代码是思想的体现。有思想的程序猿才能进化嘛。就这样啦。。