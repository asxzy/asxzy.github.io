---
layout: post
title: ! '[转载][直观学习排序算法] 视觉直观感受若干常用排序算法'
date: '2012-1-9'
comments: true
---
<!--:zh--><div>
<h1><strong>1 快速排序</strong></h1>
<strong>介绍：</strong>

快速排序是由<a title="东尼·霍尔" href="http://zh.wikipedia.org/wiki/%E6%9D%B1%E5%B0%BC%C2%B7%E9%9C%8D%E7%88%BE">东尼·霍尔</a>所发展的一种<a title="排序算法" href="http://zh.wikipedia.org/wiki/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95">排序算法</a>。在平均状况下，排序 <em>n</em> 个项目要<a title="大O符号" href="http://zh.wikipedia.org/wiki/%E5%A4%A7O%E7%AC%A6%E5%8F%B7"><strong>Ο</strong></a>(<em>n</em> log <em>n</em>)次比较。在最坏状况下则需要<strong>Ο</strong>(<em>n</em><sup><span style="font-size: x-small;">2</span></sup>)次比较，但这种状况并不常见。事实上，快速排序通常明显比其他<strong>Ο</strong>(<em>n</em> log <em>n</em>) 算法更快，因为它的内部循环（inner loop）可以在大部分的架构上很有效率地被实现出来，且在大部分真实世界的数据，可以决定设计的选择，减少所需时间的二次方项之可能性。

<strong>步骤：</strong>
<ul>
	<li>从数列中挑出一个元素，称为 "基准"（pivot），</li>
	<li>重新排序数列，所有元素比基准值小的摆放在基准前面，所有元素比基准值大的摆在基准的后面（相同的数可以到任一边）。在这个分区退出之后，该基准就处于数列的中间位置。这个称为<strong>分区（partition）</strong>操作。</li>
	<li><a title="递归" href="http://zh.wikipedia.org/wiki/%E9%80%92%E5%BD%92">递归</a>地（recursive）把小于基准值元素的子数列和大于基准值元素的子数列排序。</li>
</ul>
<strong>排序效果：</strong>

![](http://upload.wikimedia.org/wikipedia/commons/6/6a/Sorting_quicksort_anim.gif)

<strong>详细过程：</strong>

&nbsp;

&nbsp;
# 2 归并排序
<strong>介绍：</strong>

归并排序（Merge sort，台湾译作：合并排序）是建立在归并操作上的一种有效的<a title="排序" href="http://zh.wikipedia.org/wiki/%E6%8E%92%E5%BA%8F">排序</a><a title="算法" href="http://zh.wikipedia.org/wiki/%E7%AE%97%E6%B3%95">算法</a>。该算法是采用<a title="分治法" href="http://zh.wikipedia.org/wiki/%E5%88%86%E6%B2%BB%E6%B3%95">分治法</a>（Divide and Conquer）的一个非常典型的应用

<strong>步骤：</strong>
<ul>
	<li>申请空间，使其大小为两个已经排序序列之和，该空间用来存放合并后的序列</li>
	<li>设定两个指针，最初位置分别为两个已经排序序列的起始位置</li>
	<li>比较两个指针所指向的元素，选择相对小的元素放入到合并空间，并移动指针到下一位置</li>
	<li>重复步骤3直到某一指针达到序列尾</li>
	<li>将另一序列剩下的所有元素直接复制到合并序列尾</li>
</ul>
<strong>排序效果：</strong>

![](http://upload.wikimedia.org/wikipedia/commons/c/c5/Merge_sort_animation2.gif)

<strong>详细过程：</strong>

&nbsp;

&nbsp;
# 3 堆排序
<strong>介绍：</strong>

堆积排序（Heapsort）是指利用<a title="堆 (数据结构)" href="http://zh.wikipedia.org/wiki/%E5%A0%86_%28%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%29">堆</a>这种数据结构所设计的一种排序算法。堆是一个近似<a title="完全二叉树" href="http://zh.wikipedia.org/wiki/%E5%AE%8C%E5%85%A8%E4%BA%8C%E5%8F%89%E6%A0%91">完全二叉树</a>的结构，并同时满足<em>堆性质</em>：即子结点的键值或索引总是小于（或者大于）它的父节点。

<strong>步骤：</strong>

（比较复杂，自己上网查吧）

<strong>排序效果：</strong>

![](http://upload.wikimedia.org/wikipedia/commons/1/1b/Sorting_heapsort_anim.gif)

<strong>详细过程：</strong>

（暂无）
# 4 选择排序
<strong>介绍：</strong>

选择排序(Selection sort)是一种简单直观的<a title="排序算法" href="http://zh.wikipedia.org/wiki/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95">排序算法</a>。它的工作原理如下。首先在未排序序列中找到最小元素，存放到排序序列的起始位置，然后，再从剩余未排序元素中继续寻找最小元素，然后放到排序序列末尾。以此类推，直到所有元素均排序完毕。

<strong>排序效果：</strong>

![](http://upload.wikimedia.org/wikipedia/commons/b/b0/Selection_sort_animation.gif)

<strong>详细过程：</strong>

&nbsp;

&nbsp;
# 5 冒泡排序
<strong>介绍：</strong>

冒泡排序（Bubble Sort，台湾译为：泡沫排序或气泡排序）是一种简单的<a title="排序算法" href="http://zh.wikipedia.org/wiki/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95">排序算法</a>。它重复地走访过要排序的数列，一次比较两个元素，如果他们的顺序错误就把他们交换过来。走访数列的工作是重复地进行直到没有再需要交换，也就是说该数列已经排序完成。这个算法的名字由来是因为越小的元素会经由交换慢慢“浮”到数列的顶端。

<strong>步骤：</strong>
<ol>
	<li>比较相邻的元素。如果第一个比第二个大，就交换他们两个。</li>
	<li>对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对。在这一点，最后的元素应该会是最大的数。</li>
	<li>针对所有的元素重复以上的步骤，除了最后一个。</li>
	<li>持续每次对越来越少的元素重复上面的步骤，直到没有任何一对数字需要比较。</li>
</ol>
<strong>排序效果：</strong>

![](http://upload.wikimedia.org/wikipedia/commons/3/37/Bubble_sort_animation.gif)

<strong>详细过程：</strong>

&nbsp;

&nbsp;
# 6 插入排序
<strong>介绍：</strong>

插入排序（Insertion Sort）的算法描述是一种简单直观的<a title="排序算法" href="http://zh.wikipedia.org/wiki/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95">排序算法</a>。它的工作原理是通过构建有序序列，对于未排序数据，在已排序序列中从后向前扫描，找到相应位置并插入。插入排序在实现上，通常采用in-place排序（即只需用到O(1)的额外空间的排序），因而在从后向前扫描过程中，需要反复把已排序元素逐步向后挪位，为最新元素提供插入空间。

<strong>步骤：</strong>
<ul>
	<li>从第一个元素开始，该元素可以认为已经被排序</li>
	<li>取出下一个元素，在已经排序的元素序列中从后向前扫描</li>
	<li>如果该元素（已排序）大于新元素，将该元素移到下一位置</li>
	<li>重复步骤3，直到找到已排序的元素小于或者等于新元素的位置</li>
	<li>将新元素插入到该位置中</li>
	<li>重复步骤2</li>
</ul>
<strong>排序效果：</strong>

（暂无）

<strong>详细过程：</strong>

&nbsp;

&nbsp;
# 7 希尔排序
<strong>介绍：</strong>

希尔排序，也称递减增量排序算法，是<a title="插入排序" href="http://zh.wikipedia.org/wiki/%E6%8F%92%E5%85%A5%E6%8E%92%E5%BA%8F">插入排序</a>的一种高速而稳定的改进版本。

希尔排序是基于插入排序的以下两点性质而提出改进方法的：
<ul>
	<li>插入排序在对几乎已经排好序的数据操作时， 效率高， 即可以达到<a title="线性排序" href="http://zh.wikipedia.org/w/index.php?title=%E7%BA%BF%E6%80%A7%E6%8E%92%E5%BA%8F&action=edit&redlink=1">线性排序</a>的效率</li>
	<li>但插入排序一般来说是低效的， 因为插入排序每次只能将数据移动一位</li>
</ul>
<strong>排序效果：</strong>

![](http://upload.wikimedia.org/wikipedia/commons/d/d8/Sorting_shellsort_anim.gif)

</div><!--:--><!--:en--><h1><strong>1 快速排序</strong></h1>
<strong>介绍：</strong>

快速排序是由<a title="东尼·霍尔" href="http://zh.wikipedia.org/wiki/%E6%9D%B1%E5%B0%BC%C2%B7%E9%9C%8D%E7%88%BE">东尼·霍尔</a>所发展的一种<a title="排序算法" href="http://zh.wikipedia.org/wiki/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95">排序算法</a>。在平均状况下，排序 <em>n</em> 个项目要<a title="大O符号" href="http://zh.wikipedia.org/wiki/%E5%A4%A7O%E7%AC%A6%E5%8F%B7"><strong>Ο</strong></a>(<em>n</em> log <em>n</em>)次比较。在最坏状况下则需要<strong>Ο</strong>(<em>n</em><sup>2</sup>)次比较，但这种状况并不常见。事实上，快速排序通常明显比其他<strong>Ο</strong>(<em>n</em> log <em>n</em>) 算法更快，因为它的内部循环（inner loop）可以在大部分的架构上很有效率地被实现出来，且在大部分真实世界的数据，可以决定设计的选择，减少所需时间的二次方项之可能性。

<strong>步骤：</strong>
<ul>
	<li>从数列中挑出一个元素，称为 "基准"（pivot），</li>
	<li>重新排序数列，所有元素比基准值小的摆放在基准前面，所有元素比基准值大的摆在基准的后面（相同的数可以到任一边）。在这个分区退出之后，该基准就处于数列的中间位置。这个称为<strong>分区（partition）</strong>操作。</li>
	<li><a title="递归" href="http://zh.wikipedia.org/wiki/%E9%80%92%E5%BD%92">递归</a>地（recursive）把小于基准值元素的子数列和大于基准值元素的子数列排序。</li>
</ul>
<strong>排序效果：</strong>

![](http://upload.wikimedia.org/wikipedia/commons/6/6a/Sorting_quicksort_anim.gif)

<strong>详细过程：</strong>

&nbsp;

&nbsp;
# 2 归并排序
<strong>介绍：</strong>

归并排序（Merge sort，台湾译作：合并排序）是建立在归并操作上的一种有效的<a title="排序" href="http://zh.wikipedia.org/wiki/%E6%8E%92%E5%BA%8F">排序</a><a title="算法" href="http://zh.wikipedia.org/wiki/%E7%AE%97%E6%B3%95">算法</a>。该算法是采用<a title="分治法" href="http://zh.wikipedia.org/wiki/%E5%88%86%E6%B2%BB%E6%B3%95">分治法</a>（Divide and Conquer）的一个非常典型的应用

<strong>步骤：</strong>
<ul>
	<li>申请空间，使其大小为两个已经排序序列之和，该空间用来存放合并后的序列</li>
	<li>设定两个指针，最初位置分别为两个已经排序序列的起始位置</li>
	<li>比较两个指针所指向的元素，选择相对小的元素放入到合并空间，并移动指针到下一位置</li>
	<li>重复步骤3直到某一指针达到序列尾</li>
	<li>将另一序列剩下的所有元素直接复制到合并序列尾</li>
</ul>
<strong>排序效果：</strong>

![](http://upload.wikimedia.org/wikipedia/commons/c/c5/Merge_sort_animation2.gif)

<strong>详细过程：</strong>

&nbsp;

&nbsp;
# 3 堆排序
<strong>介绍：</strong>

堆积排序（Heapsort）是指利用<a title="堆 (数据结构)" href="http://zh.wikipedia.org/wiki/%E5%A0%86_%28%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%29">堆</a>这种数据结构所设计的一种排序算法。堆是一个近似<a title="完全二叉树" href="http://zh.wikipedia.org/wiki/%E5%AE%8C%E5%85%A8%E4%BA%8C%E5%8F%89%E6%A0%91">完全二叉树</a>的结构，并同时满足<em>堆性质</em>：即子结点的键值或索引总是小于（或者大于）它的父节点。

<strong>步骤：</strong>

（比较复杂，自己上网查吧）

<strong>排序效果：</strong>

![](http://upload.wikimedia.org/wikipedia/commons/1/1b/Sorting_heapsort_anim.gif)

<strong>详细过程：</strong>

（暂无）
# 4 选择排序
<strong>介绍：</strong>

选择排序(Selection sort)是一种简单直观的<a title="排序算法" href="http://zh.wikipedia.org/wiki/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95">排序算法</a>。它的工作原理如下。首先在未排序序列中找到最小元素，存放到排序序列的起始位置，然后，再从剩余未排序元素中继续寻找最小元素，然后放到排序序列末尾。以此类推，直到所有元素均排序完毕。

<strong>排序效果：</strong>

![](http://upload.wikimedia.org/wikipedia/commons/b/b0/Selection_sort_animation.gif)

<strong>详细过程：</strong>

&nbsp;

&nbsp;
# 5 冒泡排序
<strong>介绍：</strong>

冒泡排序（Bubble Sort，台湾译为：泡沫排序或气泡排序）是一种简单的<a title="排序算法" href="http://zh.wikipedia.org/wiki/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95">排序算法</a>。它重复地走访过要排序的数列，一次比较两个元素，如果他们的顺序错误就把他们交换过来。走访数列的工作是重复地进行直到没有再需要交换，也就是说该数列已经排序完成。这个算法的名字由来是因为越小的元素会经由交换慢慢“浮”到数列的顶端。

<strong>步骤：</strong>
<ol>
	<li>比较相邻的元素。如果第一个比第二个大，就交换他们两个。</li>
	<li>对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对。在这一点，最后的元素应该会是最大的数。</li>
	<li>针对所有的元素重复以上的步骤，除了最后一个。</li>
	<li>持续每次对越来越少的元素重复上面的步骤，直到没有任何一对数字需要比较。</li>
</ol>
<strong>排序效果：</strong>

![](http://upload.wikimedia.org/wikipedia/commons/3/37/Bubble_sort_animation.gif)

<strong>详细过程：</strong>

&nbsp;

&nbsp;
# 6 插入排序
<strong>介绍：</strong>

插入排序（Insertion Sort）的算法描述是一种简单直观的<a title="排序算法" href="http://zh.wikipedia.org/wiki/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95">排序算法</a>。它的工作原理是通过构建有序序列，对于未排序数据，在已排序序列中从后向前扫描，找到相应位置并插入。插入排序在实现上，通常采用in-place排序（即只需用到O(1)的额外空间的排序），因而在从后向前扫描过程中，需要反复把已排序元素逐步向后挪位，为最新元素提供插入空间。

<strong>步骤：</strong>
<ul>
	<li>从第一个元素开始，该元素可以认为已经被排序</li>
	<li>取出下一个元素，在已经排序的元素序列中从后向前扫描</li>
	<li>如果该元素（已排序）大于新元素，将该元素移到下一位置</li>
	<li>重复步骤3，直到找到已排序的元素小于或者等于新元素的位置</li>
	<li>将新元素插入到该位置中</li>
	<li>重复步骤2</li>
</ul>
<strong>排序效果：</strong>

（暂无）

<strong>详细过程：</strong>

&nbsp;

&nbsp;
# 7 希尔排序
<strong>介绍：</strong>

希尔排序，也称递减增量排序算法，是<a title="插入排序" href="http://zh.wikipedia.org/wiki/%E6%8F%92%E5%85%A5%E6%8E%92%E5%BA%8F">插入排序</a>的一种高速而稳定的改进版本。

希尔排序是基于插入排序的以下两点性质而提出改进方法的：
<ul>
	<li>插入排序在对几乎已经排好序的数据操作时， 效率高， 即可以达到<a title="线性排序" href="http://zh.wikipedia.org/w/index.php?title=%E7%BA%BF%E6%80%A7%E6%8E%92%E5%BA%8F&action=edit&redlink=1">线性排序</a>的效率</li>
	<li>但插入排序一般来说是低效的， 因为插入排序每次只能将数据移动一位</li>
</ul>
<strong>排序效果：</strong>

![](http://upload.wikimedia.org/wikipedia/commons/d/d8/Sorting_shellsort_anim.gif)
