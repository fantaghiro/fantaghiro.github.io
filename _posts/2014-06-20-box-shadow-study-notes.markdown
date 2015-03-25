---
layout: post
title: box-shadow学习笔记
category: study
description: 仔细学习了CSS中box-shadow的用法。
tags:
- CSS
- 前端
- 笔记
---
  
昨天练习着看别人写的代码，是关于页面效果的。对于阅读结果的预期不如一开始所想的。原本已经看过的知识已经显得生疏。虽然最终磕磕绊绊地把代码看下来了，但是对自己还是很不满意。于是决定把里面生疏的一些地方拿出来好好再看一下。于是有了这样第一篇文章，关于CSS中box-shadow样式的学习总结。

box-shadow的语法是这样的：
  
```
Formal syntax: none | [inset? && [ <offset-x> <offset-y> <blur-radius>? <spread-radius>? <color>? ] ]#
```
  
  
- 这里是一个目录
{:toc}
  
##各项设置说明##
  
###inset###
  
在没有设置inset的情况下，阴影部分默认方向是在box之外，向右向下延伸的（就好像box是在内容之上）。
  
一旦设置了inset，阴影部分就出现在box里面（就好像里面的内容在box里面被压了下去）。inset的阴影是在边框里面绘制的（即使边框是透明的也没关系），同时inset阴影位于背景之上，内容之下。
  
###&lt;offset-x>&lt;offset-y>###
  
这是两个长度值，用于指定阴影偏移的距离。&lt;offset-x>用于指定横向偏移距离。如果设为负值，就会将阴影置于元素左侧。&lt;offset-y>设定的是纵向的偏移，负值会将阴影置于元素的上方。
  
如果这两个数值都设为0，那么阴影是位于元素后面（而且如果设置了&lt;blur-radius>和/或&lt;spread-radius>的话，可能会产生一个模糊的效果）。
  
###&lt;blur-radius>###
  
这是第三个长度值。该值越大，模糊范围就越大，阴影就会随之_变大_变浅。该值不允许设为负值。如果没有设置该值，那么默认为0（也就是说阴影边缘是锋利的）。
  
###&lt;spread-radius>###
  
这是第四个长度值。正值会导致阴影扩张变大；负值会导致阴影缩小。如果没有具体设置数值，那么默认为0（也就是说阴影的大小与元素大小相当）。
  
###&lt;color>###
  
设置阴影的颜色。如果没有具体设置的话，阴影颜色要取决于浏览器——通常情况下会采用color的值，但是需要注意的是，Safari浏览器目前碰到这种情况，会绘制一个透明的阴影。
  
##具体实例##
  
<p data-height="518" data-theme-id="2146" data-slug-hash="tLxpc" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/fantaghiro/pen/tLxpc/'>box-shadow-test</a> by Pei (<a href='http://codepen.io/fantaghiro'>@fantaghiro</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>
  
###实例说明###

> 从第1、2个box可以看出，设置了blur-radius会使阴影周围出现模糊。但是虽然设置了blur-radius，但是由于box2的offset-x和offset-y与box1相同，整个可视阴影范围也大致相当。据称，设置了blur-radius的阴影范围实际上是大于原范围的，但是由于边缘模糊，真正的可视范围的大小并不会有太大改变。

> box3中，由于将blur-radius设置为负值，导致任何阴影都没有出现，对box-shadow的样式设置无效。

> box4中，针对不同方向上的阴影可以设置不同颜色以及blur-radius值。设置了blur-radius的绿色阴影就比红色阴影模糊。

> box5中，由于没有设置offset-y值，因此阴影仅在横向上发生偏移。但是看box1—4，由于设置了offset-y值，都在纵向上发生了便宜。对于box-shadow，我之前错误的认为，阴影是添加上去的，其实不然。在没有添加spread-radius的情况下，阴影是与元素大小相同，如果没有设置inset，阴影是位于元素下方。出现阴影是由于阴影相对于元素的位置发生偏移造成的。因此，将阴影添加到元素上的东西是认识错误，将阴影与元素视为叠着的两层，出现x和y 的偏移时，两层的相对位置就被错开了一点，这样更有助于理解。

> box6与box5对比看，box6比5多了1em的blur-radius，即使在纵向上没有发生偏移，box6在纵向上仍然呈现出有阴影的摸样。这说明blur-radius确实让阴影范围变大了，但是变大的并不是很多。

> box7增加了spread-radius的设置，阴影范围明显增大。可以看出，spread-radius是在原阴影四周都增加了长度。

> box8—12对比来看，能够清晰看出blur-radius对模糊的作用和spread-radius对于阴影大小的作用。值得注意的是spread-radius可以设为负值，见box12。

> 从box13—15看来，blur-radius也作用于添加的spread-radius上。

> box16、17是关于inset的演示。如果设置了inset，那么offset-x如果设置为正值，阴影会在元素内部的左侧出现；设置为负值，会在元素右侧出现。offset-y如果设置了正值，阴影会在元素内部的上侧出现；设为负值，会在元素内部的下侧出现。

> box18说明，针对内、外阴影，可以有不同的设置。

> box19说明，如果针对同一位置有不同的阴影设置，那么先设置的值位于后设置的值上方。box19中的黄色阴影位于黑色阴影之上。

> box20说明，如果有两层阴影叠加，并且前面一层阴影有blur-radius设置，后面一层阴影就会透出来一些。可以看到box20的设置了blur-radius的黄色阴影就没有box19的黄色阴影那么亮。

> box21说明，阴影的形状是跟随元素形状改变的。元素变为圆角，阴影就自动变为圆角。

> box22—24对比来看，对于阴影的颜色可以设置一定的透明度。如果将两个有透明度的同色的阴影叠加，则颜色会变深，可以看到box23是box22同样的阴影叠加了两边，颜色就比box22明显要深。但是box23两个阴影叠加起来还是没有box24的实色颜色深。

> box25说明，对于阴影的不同设置，用逗号分隔，可以加很多条，组合起来会造成十分复杂的效果。

##相关文章收集##

1. [这里](http://blog.codeschool.com/post/89758324803/designing-characters-with-box-shadow)有一位牛人，用box-shadow做像素动画！
