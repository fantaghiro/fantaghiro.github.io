---
layout: post
title: box-shadow学习笔记
category: study
tags:
- CSS
- 前端
- 笔记
---

昨天练习着看别人写的代码，是关于页面效果的。对于阅读结果的预期不如一开始所想的。原本已经看过的知识已经显得生疏。虽然最终磕磕绊绊地把代码看下来了，但是对自己还是很不满意。于是决定把里面生疏的一些地方拿出来好好再看一下。于是有了这样第一篇文章，关于CSS中box-shadow样式的学习总结。
<!--more-->

box-shadow的语法是这样的：

···
Formal syntax: none | [inset? && [ &lt;offset-x> &lt;offset-y> &lt;blur-radius>? &lt;spread-radius>? &lt;color>? ] ]#
···

##各项设置说明##

###inset###

在没有设置inset的情况下，阴影部分默认方向是在box之外，向右向下延伸的（就好像box是在内容之上）。

一旦设置了inset，阴影部分就出现在box里面（就好像里面的内容在box里面被压了下去）。inset的阴影是在边框里面绘制的（即使边框是透明的也没关系），同时inset阴影位于背景之上，内容之下。

###&lt;offset-x>&lt;offset-y>###

这是两个长度值，用于指定阴影偏移的距离。&lt;offset-x>用于指定横向偏移距离。如果设为负值，就会将阴影置于元素左侧。&lt;offset-y>设定的是纵向的偏移，负值会将阴影置于元素的上方。

如果这两个数值都设为0，那么阴影是位于元素后面（而且如果设置了&lt;blur-radius>和/或&lt;spread-radius>的话，可能会产生一个模糊的效果）。

###&lt;blur-radius>###

这是第三个长度值。该值越大，模糊范围就越大，阴影就会随之变大变浅。该值不允许设为负值。如果没有设置该值，那么默认为0（也就是说阴影边缘是锋利的）。

###&lt;spread-radius>###

这是第四个长度值。正值会导致阴影扩张变大；负值会导致阴影缩小。如果没有具体设置数值，那么默认为0（也就是说阴影的大小与元素大小相当）。

###&lt;color>###

设置阴影的颜色。如果没有具体设置的话，阴影颜色要取决于浏览器——通常情况下会采用color的值，但是需要注意的是，Safari浏览器目前碰到这种情况，会绘制一个透明的阴影。

##具体实例##

<p data-height="518" data-theme-id="2146" data-slug-hash="tLxpc" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/fantaghiro/pen/tLxpc/'>box-shadow-test</a> by Pei (<a href='http://codepen.io/fantaghiro'>@fantaghiro</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

