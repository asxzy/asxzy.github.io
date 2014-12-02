---
layout: post
title: 简易整合ThinkPHP2.0和CKEditor
date: '2010-10-22'
comments: true
---
之前看过一些文章，也是关于ThinkPHP2.0和CKEdior/FCKEditor的，不过大多数是Ctrl+C/Ctrl+V草草了事，没有亲手实践，或多或少都给读者留有问题。

自己动手丰衣足食，现在把我将ThinkPHP2.0和CKEditor的整合过程写下来，原理是ThinkPHP2.0的第三方类库导入机制，如有不周，还请看客批评指正。

首先在CKEditor官网下载最新版本的CKEditor，解压到/Pulibc/ckeditor。

将ckeditor中的ckeditor_php5.php复制到/ThinkPHP/Vendor/ckeditor/ckeditor.php

接下来，打开复制过去的ckeditor.php，修改以下两处：
```
1.38行
public $basePath;改为
public $basePath='__PUBLIC__/ckeditor/';目的是让CKEditor找到正确的引用目录。

2.69行
把public $returnOutput = true;改为
public $returnOutput = false;目的是不直接输出生成结果，便于分配到模板。
```
以上两处修改好之后，CKEditor就可以在TP中调用了。
如果没有特殊需求，项目中最简单调用方法为：
```
vendor("ckeditor.ckeditor");
$CKEditor= new CKEditor();
$this-&gt;assign('CKeditor',$CKEditor-&gt;editor("content","text here"));
```
其中content为textaera的name，text here为textaera中的文字。

在模板中直接使用{$CKeditor}就将CKeditor调用出来了。

上传部分现在还没有使用，等到使用起来再更新吧。
