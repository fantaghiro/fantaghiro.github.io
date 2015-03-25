---
layout: post
title: CSS3 gradient 学习笔记
category: study
description: 仔细学习了CSS中gradient的用法。
tags:
- CSS
- 前端
- 笔记
---

##总述

CSS中的&lt;gradient>指的是一种image，可以看到&lt;gradient>通常设置到background或者background-image上。但是这种image没有大小，会随着被应用的对象大小而改变。gradient一次在英文是坡度的意思，也含有逐渐改变的意思。在CSS中表示的就是两个或多个颜色的渐进过渡。

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
linear-gradient(  [ <angle> | to <side-or-corner> ,]? <color-stop> [, <color-stop>]+ )
{% endhighlight %}

以上语法中：

- <code> [<angle> | to <side-or-color>,] </code>这一部分用于定义gradient line
    - 其中 <code><side-or-color></code> = <code>[left | right] || [top | bottom]</code> 
- <code><color-stop> [, <color-stop>]+</code> 用于定义color-stop point列表
    - 其中 <code><color-stop></code> =<code> <color> [ <percentage> | <length> ]?</code>

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

##radial-gradient

###定义

radial-gradient由中心（center）、结束图形轮廓（ending shape contour）、位置（position）和color stop确定。radial-gradient包括了连续的从其中心一直到结束轮廓以及更远的位置的同心且与结束图形轮廓一致的图形。color stop定位在一条虚拟的渐变射线（virtual gradient ray）上。这个virtual gradient ray是水平从中心开始向正右方延伸。如果是用百分比表示位置的话，那么从中心到virtual gradient ray与结束图形轮廓之间的焦点这么一段线段为100%。从中心开始逐渐扩大的并且与结束轮廓形状一致的每个形状都是单色的，其颜色由它与gradient ray相交的交点的颜色决定。

**结束形状只能是正圆（circle）或椭圆（ellipse）。**

radial-gradient不允许设置重复的渐变，如果要实现重复的径向渐变，可以使用repeating-radial-gradient。

<img style="max-width: 90%;" src="http://pic.yupoo.com/fantaghiro_v/DRiOmtI9/H727n.png" >

###语法

{% highlight css %}
  radial-gradient( [[ circle               || &lt;length> ]                     [ at &lt;position> ]? , | 
                    [ ellipse              || [&lt;length> | &lt;percentage> ]{2}] [ at &lt;position> ]? , |
                    [ [ circle | ellipse ] || &lt;extent-keyword> ]             [ at &lt;position> ]? , |
                                                                               at &lt;position> ,     &lt;color-stop> [ , &lt;color-stop> ]+ )
                   \------------------------------------------------------------------------------/\--------------------------------/
                                 Definition of the contour, size and position of the ending shape         List of color stops  
    
          where &lt;extent-keyword> = closest-corner | closest-side | farthest-corner | farthest-side
            and &lt;color-stop> = &lt;color> [ &lt;percentage> | &lt;length> ]?
{% endhighlight %}

**定义ending shape**

- radial-gradient( circle, … )
等同于 radial-gradient( circle farthest-corner, …) 

- radial-gradient( ellipse, … )
等同于radial-gradient( ellipse farthest-corner, …) 

- radial-gradient( &lt;extent-keyword>, … )
会画出一个正圆

- radial-gradient( circle radius, … ) 
一个位于中心的正圆，具有固定半径。不可以用百分比。

- radial-gradient( ellipse x-axis y-axis, … ) 
给出两个椭圆半轴的长度，现是水平方向，然后是垂直方向

**定义图形的位置**

- radial-gradient(... at &lt;position>, ...)

**定义color stop**

- radial-gradient(..., &lt;color-stop>)
- radial-gradient(..., &lt;color-stop>, &lt;color-stop>)

下面是具体说明。

####&lt;position>

该属性的意义与&lt;background-position>或&lt;transform-origin>相同。如果没有设置该属性，则默认为中心center。

####&lt;shape>

定义的是渐变的形状。可以是circle（正圆）；或者是ellipse（椭圆）。默认值为ellipse。

####&lt;size>

渐变的大小。

####&lt;color-stop>

确定某个固定点的颜色。该值包含一个颜色值，后面跟一个可选的stop position（用百分比或长度表示）。0%或长度0代表渐变的中心。100%代表虚拟的gradient ray与ending shape的交点。在0%和100%之间的百分比值，是线性分布在gradient ray上的。

####&lt;extent-keywrod>

也就是描述ending shape有多大的关键词。可用的关键词如下表：

<table>
    <thead>
        <td>Constant</td>
        <td>Description</td>
    </thead>
    <tbody>
        <tr>
            <td>closest-side</td>
            <td>如果是正圆，那么渐变的ending shape与box最接近center的一边相切；如果是椭圆，那么ending shape与最接近中心的水平边与垂直边相切。</td>
        </tr>
        <tr>
            <td>closest-corner</td>
            <td>渐变的ending shape与最接近中心的box的一角相遇。</td>
        </tr>
        <tr>
            <td>farthest-side</td>
            <td>与closest-side相似，只不过把“最接近”改为“最远离”。</td>
        </tr>
        <tr>
            <td>farthest-corner</td>
            <td>与closest-corner相似，只不过把“最接近”改为“最远离”。</td>
        </tr>
    </tbody>
</table>

###radial-gradient实例

<p data-height="331" data-theme-id="2146" data-slug-hash="dJGvj" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/fantaghiro/pen/dJGvj/'>dJGvj</a> by Pei (<a href='http://codepen.io/fantaghiro'>@fantaghiro</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

###radial-gradient灵活使用

<p data-height="307" data-theme-id="2146" data-slug-hash="sCpeJ" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/fantaghiro/pen/sCpeJ/'>sCpeJ</a> by Pei (<a href='http://codepen.io/fantaghiro'>@fantaghiro</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

从上述例子可以看出，radial-gradient可以作为图片来看待，可以定位；radial-gradient可以叠加，可以为radial-gradient添加底色。

##repeating-linear-gradient、repeating-radial-gradient

简而言之，repeating-linear-gradient就是可以无限重复的linear-gradient。见下例：

<p data-height="268" data-theme-id="2146" data-slug-hash="CHeAi" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/fantaghiro/pen/CHeAi/'>CHeAi</a> by Pei (<a href='http://codepen.io/fantaghiro'>@fantaghiro</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

需要注意的是：在设置repeating-linear-gradient时，与linear-gradient不同的是，不要给repeating-linear-gradient设置明确的end color。如果设置了，那么也就repeat不起来了。最后一个颜色一定要设置一定长度或百分比才行。

同理，一下是两个repeating-radial-gradient的例子：

<p data-height="578" data-theme-id="2146" data-slug-hash="EAFeB" data-default-tab="result" class='codepen'>See the Pen <a href='http://codepen.io/fantaghiro/pen/EAFeB/'>EAFeB</a> by Pei (<a href='http://codepen.io/fantaghiro'>@fantaghiro</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

##五彩斑斓的由gradient制作的图案

通过各种技术组合，可以通过gradient的设置制作出各种精美的图案。在[这里](http://lea.verou.me/css3patterns/)能看到很多神奇的Pattern。

