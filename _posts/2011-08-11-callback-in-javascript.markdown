---
layout: post
title: 理解JavaScript的回调函数（callback）
date: '2011-8-11'
comments: true
---
用过jQuery的人都对其callback的使用印象深刻，惭愧的是，用了两年jQuery，我至今都不知回调是如何实现的，于是乎，各种代码。

1.什么是回调函数（callback）
回调函数，就是由你自己写的。你需要调用另外一个函数，而这个函数的其中一个参数，就是你的这个回调函数名。这样，系统在必要的时候，就会调用你写的回调函数，这样你就可以在回调函数里完成你要做的事。
回调函数是一个很有用，也很重要的概念。当发生某种事件时，系统或其他函数将会自动调用你定义的一段函数。

这样说，也许会晕。

用代码看看。
jQuery中getJSON的官方样例

	$.getJSON("http://api.flickr.com/services/feeds/photos_public.gne?tags=cat&tagmode=any&format=json&jsoncallback=?",
		function(data){
		$.each(data.items, function(i,item){
			$("</pre>
	<img alt="" />
	<pre>").attr("src", item.media.m).appendTo("#images");
			if ( i == 3 ) return false;
		});
	});

getJSON的定义是loadJSON(url,callback);
其实现的功能是，发送GET请求到url，发送完毕之后，调用callback函数，一般用于处理url所获取的内容。

为什么要这样做的，因为JavaScript是异步处理数据的。何为异步处理？读者<a href="//?p=196">猛点这里</a>

2.回调函数的实现
知道了什么是回调函数，就要考虑它的实现方法了。看个最简单的样例。

	a = function(f){
		data = 1;
		console.log(data++);
		f();
	};

	a(function(){
		console.log(data);
	});

运行结果
1
2

定义一个函数a，参数为一个函数f，这个f和一般传入的变量一样，只是一个变量名，并不代表有一个函数实体f。
a函数体内，给这个f指定一个要传入的参数，一般都写在最后，回调函数的意义就是在于在某个函数内满足一定条件或接收数据之后进行回调。

最后调用函数a，并传入一个函数实体function(){};一个最简单的回调函数就完成了。

其实回调函数的定义，总结为一句话，将函数作为变量传入需要进行回调的函数内。


2011.8.11@淘宝
