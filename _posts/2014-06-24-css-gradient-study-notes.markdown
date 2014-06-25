---
layout: post
title: CSS3 gradient 学习笔记
category: study
tags:
- CSS
- 前端
- 笔记
---

##总述

CSS中的&lt;gradient>指的是一种image，可以看到&lt;gradient>通常设置到background或者background-image上。但是这种image没有大小，会随着被应用的对象大小而改变。gradient一次在英文是坡度的意思，也含有逐渐改变的意思。在CSS中表示的就是两个或多个颜色的渐进过渡。
<!--more-->

- 这里是一个目录
{:toc}

CSS中的过渡gradient包含有四种形式：linear-gradient、radial-gradient、repeating-linear-gradient、repeating-radial-gradient。这四种类型下面各举一例：

<p data-height="268" data-theme-id="2146" data-slug-hash="JbECi" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/fantaghiro/pen/JbECi/'>JbECi</a> by Pei (<a href='http://codepen.io/fantaghiro'>@fantaghiro</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

##linear-gradient

###定义

linear-gradient是线性过渡。它是由一个轴——过渡线(gradient line)——定义的。在gradient line上的每一个点颜色都不同。垂直于gradient line的每一条线上的颜色都相同，都是该垂直线与gradient line相交的焦点的颜色。如下图所示：

<img src="http://pic.yupoo.com/fantaghiro_v/DR7CkQuj/j12bE.png">

gradient line是通过box中点并有一定倾角的轴线。过渡色是由不同点来定义的，包括起始点（starting point）、终止点（ending point）以及中间可选的停色点（stop-color points）。

起始点是gradient line上颜色开始的位置。该位置是gradient line与通过同一象限元素一角且与gradient line垂直的线的交点处。同理可得终止点。更简单的说法是：终止点是与起始点对称的位置。

除了起始点与终止点以外，还可以定义额外的位于gradient line之上的color-stop points。这样可以设置多色的渐变效果。

linear-gradient不允许设置重复的渐变，但是通过灵活运用color-stop points，可以实现同样的效果。如果要实现真正的重复渐变，可以使用repeating-linear-gradient。

如果没有指定color-stop point，那么它就默认位于前一个点与后一个点的正中间。当然color-stop point也可以明显地通过使用长度和百分比来进行设置。

> 需要注意的是，要将gradient line与视觉上亮色的模糊分界线区分开来。双色渐变经常可以用肉眼辨识出一条亮色的分界线，这条线并不是gradient line，而是与gradient line垂直的一根线。

###语法

{% highlight css %}
linear-gradient(  [ &lt;angle> | to &lt;side-or-corner> ,]? &lt;color-stop> [, &lt;color-stop>]+ )
{% endhighlight %}

以上语法中：

- <code> [&lt;angle> | to &lt;side-or-color>,] </code>这一部分用于定义gradient line
    - 其中 <code>&lt;side-or-color></code> = <code>[left | right] || [top | bottom]</code> 
- <code>&lt;color-stop> [, &lt;color-stop>]+</code> 用于定义color-stop point列表
    - 其中 <code>&lt;color-stop></code> =<code> &lt;color> [ &lt;percentage> | &lt;length> ]?</code>

下面是具体说明。

####&lt;side-or-corner>

该属性设置的是gradient line上的starting-point。它包括两个关键词：第一个关键词是水平方向上的：left或right；第二个是垂直方向上的top或bottom。按照什么顺序写都可以，而且这些关键词都是可选的。

如果设置了to top, to bottom, to left或to right，其实可以视为设置angle为 0deg、180deg、270deg、90deg。应当可以这样理解。当gradient line穿过元素中心，并且是自下而上的垂直方向时，可视为0deg，由于gradient line是自下向上的，因此是to top，starting-point是在下面；当gradient从0deg顺时针旋转180度后，方向变成自上而下，这时是to bottom，起始点在上方；然后gradient line继续顺时针方向旋转90度，也就是从0deg顺时针旋转270度时，gradient是水平的，方向是自右向左，因此是to left，起始点在右边；to right同理可得。如果设置为这四个值以外的值，比如to top right、to left bottom等，在定义这些角的时候，starting-point与所述角是在同一个象限内，同时该starting-point与该角构成的直线与gradient line垂直。这样可以确保后续设置&lt;color-stop>的时候，这个颜色刚好是那个角上那个点的颜色。

    315deg    0deg   45deg
               ^
               |
    270deg <---+---> 90deg
               |
               v
    225deg   180deg  135deg
    
<hr>
    
    top-left     top      top-right
                  ^
                  |
    left      <---+--->       right
                  |
                  v
    bottom-left bottom bottom-right


由于starting-point已经设置，那么ending-point是以元素中心为中心，与starting-point对称的那个点，因此也相应确定了。

####&lt;angle>

angle角度，定义的就是渐变的方向。当渐变方向不是垂直，水平，也无法用元素的各个角定义的话，就要祭出这个值。

####&lt;color-stop>

该值是由一个&lt;color>值，后面跟着一个可选的stop position（可以用百分比表示，也可以用长度表示，百分比和长度都是针对gradient line定义的。）CSS中的color-stop的设置规则与SVG渐变中的color-stop设置规则相同。

###linear-gradient实例

以下四个例子有助于理解gradient line以及angle的设置。注意是同to top, to top right与0deg和45deg的不同设置方式，但是却获得同样的效果。注意领会starting point的位置。注意领会“to”一词内涵的方向含义。

<p data-height="268" data-theme-id="2146" data-slug-hash="Jsyew" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/fantaghiro/pen/Jsyew/'>Jsyew</a> by Pei (<a href='http://codepen.io/fantaghiro'>@fantaghiro</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>


###linear-gradient加厂商前缀与不加厂商前缀的写法区别

由于历史问题，linear-gradient在加上厂商前缀与不加厂商前缀时，写法略有区别。这个地方十分tricky，也容易引起混淆。主要区别有如下两点：

1. 加上厂商前缀的设定方向的关键词不带“to”，代表的是渐变的起始位置，那么就真好与带to的不加厂商前缀的方向是正好相反的。例如，-webkit-linear-gradient(**top**, blue, red); 指的是元素**从上往下**，由blue向red渐变；同一个意义，如果用不带厂商前缀的标准写法来写就变成 linear-gradient(**to bottom**, blue, red);
2. 如果不使用关键词，而使用angle来进行设置的话。在没有厂商前缀时，angle是垂直向上为0deg，该轴顺时针旋转为增加deg，逆时针则为负deg；但是如果添加了厂商前缀，angle为水平向右的方向为0deg，顺时针为负deg，逆时针则为正deg。

下面是添加了厂商前缀的一些例子，可以跟上面不加厂商前缀的例子进行比较。

<p data-height="298" data-theme-id="2146" data-slug-hash="lmCnq" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/fantaghiro/pen/lmCnq/'>lmCnq</a> by Pei (<a href='http://codepen.io/fantaghiro'>@fantaghiro</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

下面是同一种渐变效果的几种不同的写法：

{% highlight css %}
.grad { 
  background-color: #F07575; /* fallback color if gradients are not supported */
  background-image: -webkit-linear-gradient(top, hsl(0, 80%, 70%), #bada55); /* For Chrome and Safari */
  background-image:    -moz-linear-gradient(top, hsl(0, 80%, 70%), #bada55); /* For old Fx (3.6 to 15) */
  background-image:     -ms-linear-gradient(top, hsl(0, 80%, 70%), #bada55); /* For pre-releases of IE 10*/
  background-image:      -o-linear-gradient(top, hsl(0, 80%, 70%), #bada55); /* For old Opera (11.1 to 12.0) */ 
  background-image:         linear-gradient(to bottom, hsl(0, 80%, 70%), #bada55); /* Standard syntax; must be last */
}
{% endhighlight %}

<p data-height="268" data-theme-id="2146" data-slug-hash="vfstA" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/fantaghiro/pen/vfstA/'>vfstA</a> by Pei (<a href='http://codepen.io/fantaghiro'>@fantaghiro</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

注意，不带厂商前缀的标准写法一定要放到最后。同时最好在一开始设置一个fallback 背景色。注意带厂商前缀和不带厂商前缀中关键词的选用正好是相反的。


###linear-gradient的灵活运用

<p data-height="268" data-theme-id="2146" data-slug-hash="rHJsb" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/fantaghiro/pen/rHJsb/'>rHJsb</a> by Pei (<a href='http://codepen.io/fantaghiro'>@fantaghiro</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

从上例中可以看出，linear-gradient可以设置多色渐变。通过巧妙设置color stop，也能够构成清晰的条纹图案。linear-gradient支持透明设置。并且可以多次设置linear-gradient效果。不同的效果会产生叠加。先设置的颜色位于上层，后设置的位于下层。如果上层的颜色设置有透明，那么下层的颜色则会透出来。

此外，还可以通过设置background-size来巧妙地实现渐变效果的重复平铺。见下面的例子：

<p data-height="624" data-theme-id="2146" data-slug-hash="KoqfE" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/fantaghiro/pen/KoqfE/'>KoqfE</a> by Pei (<a href='http://codepen.io/fantaghiro'>@fantaghiro</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>



