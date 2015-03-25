---
layout: post
title: 妙味课堂——CSS3
category: study
tags:
- CSS3
- js
- 妙味课堂
- 前端基础
- 学习笔记
---

CSS3确实非常强大，基本规则十分简单，但是使用起来确实千变万化。而且，从动画这个角度来讲，可以省去很多js代码。利用CSS3可以做出很多非常有意思的效果。

- 目录
{:toc}

学习CSS3之前先讲几个问题：

- 浏览器支持问题
- 厂商前缀问题
- 在JS中的写法：-webkit-transition => WebkitTransition; -o-transition => OTransition; -moz-transition => MozTransition

##CSS3选择器 - 属性选择器

- E[attr]只使用属性名，但没有确定任何属性值
- E[attr="value"]指定属性名，并指定了该属性的属性值
- E[attr~="value"]指定属性名，并且具有属性值，此属性值是一个词列表，并且以空格隔开，其中词列表中包含了一个value词，而且等号前面的“~”不能不写
- E[attr^="value"]指定了属性名，并且有属性值，属性值是以value开头的
- E[attr$="value"]指定了属性名，并且有属性值，而且属性值是以value结束的
- E[attr*="value"]指定了属性名，并且有属性值，而且属值中包含了value
- E[attr|="value"]指定了属性名，并且属性值是value或者以“value-”开头的值（比如说zh-cn）
- 实例：百度文库;
- 备注：IE7以上支持

**属性选择器**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>CSS3选择器</title>
	<style>
		p {height: 30px; border: 1px solid #000;}
		/*p[miaov] {background: red;} */ /*所有四个*/
		/*p[miaov=g-xM] {background: red;}*/ /*第四个小美*/
		/*p[miaov~=old] {background: red;}*/ /*第一个leo*/
		/*p[miaov^=g] {background: pink;}*/ /*第四个小美*/
		/*p[miaov$=M] {background: #cc0;}*/ /*第三、四个：子鼠和小美*/
		/*p[miaov*=d] {background: purple;}*/ /*第一、二个：leo和杜鹏*/
		/*p[miaov|=b] {background: purple;}*/ /*第一、二、三和最后一个：leo、杜鹏和子鼠、无名氏*/
	</style>
</head>
<body>
	<p miaov="b-leo old">leo</p>
	<p miaov="b-dp">杜鹏</p>
	<p miaov="b-zM">子鼠</p>
	<p miaov="g-xM">小美</p>
	<p miaov="b">无名氏</p>
</body>
</html>
~~~

**实例：百度文库**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>百度文库</title>
	<style>
		p {height: 30px; line-height: 30px; font-size: 12px; border: 1px solid #000;}
		p a {background: url(img/w.gif) no-repeat 3px center; padding-left: 20px; display: block;}
		p a[href*=text]{background: url(img/text.gif) no-repeat 3px center;}
		p a[href*=pdf]{background: url(img/swf.gif) no-repeat 3px center;}
		p a[href*=exl]{background: url(img/x.gif) no-repeat 3px center;}
	</style>
</head>
<body>
	<p><a href="http://www.miaov.com/doc/javascript.html">妙味课堂</a></p>
	<p><a href="http://www.miaov.com/text/javascript.html">妙味课堂</a></p>
	<p><a href="http://www.miaov.com/pdf/javascript.html">妙味课堂</a></p>
	<p><a href="http://www.miaov.com/doc/javascript.html">妙味课堂</a></p>
	<p><a href="http://www.miaov.com/exl/javascript.html">妙味课堂</a></p>
</body>
</html>
~~~

##CSS3选择器 - 结构性伪类

- E:nth-child(n)  表示E父元素中的第n个字节点
	- p:nth-child(odd){background:red}/*匹配奇数行*/
	- p:nth-child(even){background:red}/*匹配偶数行*/
	- p:nth-child(2n){background:red}
- E:nth-last-child(n)  表示E父元素中的第n个字节点，从后向前计算
- E:nth-of-type(n)  表示E父元素中的第n个字节点，且类型为E
- E:nth-last-of-type(n)  表示E父元素中的第n个字节点，且类型为E,从后向前计算
- E:empty 表示E元素中没有子节点。注意：子节点包含文本节点
- E:first-child 表示E元素中的第一个子节点
- E:last-child 表示E元素中的最后一个子节点
- E:first-of-type  表示E父元素中的第一个子节点且节点类型是E的
- E:last-of-type  表示E父元素中的最后一个子节点且节点类型是E的
- E:only-child表示E元素中只有一个子节点。注意：子节点不包含文本节点
- E:only-of-type 表示E的父元素中只有一个子节点，且这个唯一的子节点的类型必须是E。注意：子节点不包含文本节点
- 支持浏览器：IE9及以上、FF3.5及以上、Opera 9.6及以上、safari 3.1及以上、chrome 1.0.x及以上
- 实例：新浪头部导航

**结构性伪类**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>结构性伪类</title>
	<style>
		p {height: 30px; border: 1px solid #000;}
		span {display: block; height: 20px;}
		/*p:nth-child(1) {background: red;} *//*注意nth-child是从1开始计数的*/
		/*p:nth-child(odd) {background: red;} *//*奇数*/
		/*p:nth-child(even) {background: blue;} *//*偶数*/
		/*p:nth-child(2n) {background: green;}*/
		/*p:nth-child(2n-1) {background: yellow;}*/
		/*p:nth-child(3n) {background: purple;}*/

		/*p:nth-child(2) : 找到p标签父级下的第二个子元素，并且这个元素还得是p标签*/

		/*body *:nth-child(2) {background: red;}*/

		/*body *:nth-last-child(2) {background: green;} */ /*:nth-last-child()代表从后往前找。:nth-child()括号中写什么，:nth-last-child()里面也可以写，都支持，只不过查找顺序变成了从后向前*/

		/*p:nth-of-type(2) {background: red;}*/ /*找到p标签的父级下的第二个p标签*/

		/*body *:nth-of-type(2) {background: brown;}*/ /*body下的第二个p标签和第二个h1标签都会被找到*/

		/*p:nth-last-of-type(2) {background: purple;}*/ /*:nth-last-of-type()与:nth-of-type()都一样，只不过顺序反过来而已*/

		/*p:first-child {background: green;}*/ /*:first-child == :nth-child(1)*/

		/*:last-child == :nth-last-child(1)*/

		/*:first-of-type == :nth-of-type(1)*/
		/*:last-of-type == :nth-last-of-type(1)*/

		/*p:empty {background: black;}*/ /*不包含子元素（子元素包括文本节点）的p标签*/
		
		/*span:only-of-type {background: gray;}*/
		
		/*p *:only-of-type {background: red;}*/

		/*p *:only-child {background: blue;}*/
	</style>
</head>
<body>
	<p>p1</p>
	<h1>h1</h1>
	<p>p2</p>
	<h1>h2</h1>
	<p>p3</p>
	<h1>h3</h1>
	<p></p>
	<p>p5<span></span></p>
	<p><span></span><a href="#">链接</a></p>
</body>
</html>
~~~

**新浪头部导航**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>新浪头部导航</title>
	<style>
		.list {margin: 0; padding: 0; list-style: none;}
		.list li {width: 150px; border-right: 1px solid #000; float: left;}
		.list li:last-of-type {border: none;}
		.list a {float: left; width: 40px; margin: 0 5px; font: 12px/30px "宋体"; text-align: center;}
		.list li a:nth-of-type(3n+1) {font-weight: bold;}
		.list li:nth-child(3) a:nth-child(2) {color: red;}
	</style>
</head>
<body>
	<ul class="list">
		<li>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
		</li>
		<li>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
		</li>
		<li>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
		</li>
		<li>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
		</li>
		<li>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
		</li>
		<li>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
		</li>
		<li>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
			<a href="#">妙味</a>
		</li>
	</ul>
</body>
</html>
~~~

##CSS3选择器 - 伪类和伪元素

- E:target 表示当前的URL片段的元素类型，这个元素必须是E
- E:disabled 表示不可点击的表单控件
- E:enabled 表示可点击的表单控件
- E:checked 表示已选中的checkbox或radio
- E:first-line 表示E元素中的第一行
- E:first-letter 表示E元素中的第一个字符
- E::selection表示E元素在用户选中文字时
- E::before 生成内容在E元素前
- E::after 生成内容在E元素后
- E:not(s) 表示E元素不被匹配
- E~F表示E元素毗邻的F元素
- Content 属性

**:target伪类**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>伪类和伪元素</title>
	<style>
		div {width: 300px; height: 200px; background: #000; font: 50px/200px "微软雅黑"; color: #fff; text-align: center; display: none;}
		div:target {display: block;}
		/* :target哈希值对应的东西，点击第一个a标签，第一个div就会显示出来，因为相当于给#div1设置了display: block;的样式，点击后面两个a标签同理 */
	</style>
</head>
<body>
	<a href="#div1">div1</a>
	<a href="#div2">div2</a>
	<a href="#div3">div3</a>
	<div id="div1">div1</div>
	<div id="div2">div2</div>
	<div id="div3">div3</div>
</body>
</html>
~~~

**:disabled与:enabled**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>伪类和伪元素</title>
	<style>
		input {width: 100px; height: 30px; color: #000;}
		input:enabled {color: red;}
		input:disabled {background: gray;}
	</style>
</head>
<body>
	<input type="text" value="请输入" disabled>
</body>
</html>
~~~

**:checked**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>伪类和伪元素</title>
	<style>
		input:checked {width: 100px; height: 100px;}
	</style>
</head>
<body>
	<input type="checkbox" />
</body>
</html>
~~~

**E~F**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>伪类和伪元素</title>
	<style>
		p~h1 {background: red;}
	</style>
</head>
<body>
	<h1>h1</h1>
	<p>p</p>
	<h1>h1</h1>
	<h1>h1</h1>
</body>
</html>
~~~

**模拟单选框**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>模拟单选框</title>
	<style>
		label {float: left; margin: 0 5px; overflow: hidden; position: relative;}
		label input {position: absolute; left: -50px; top: -50px;}
		span {float: left; width: 50px; height: 50px; border: 3px solid #000;}
		input:checked~span {background: red;}
	</style>
</head>
<body>
	<label>
		<input type="radio" name="tab">
		<span></span>
	</label>
	<label>
		<input type="radio" name="tab">
		<span></span>
	</label>
	<label>
		<input type="radio" name="tab">
		<span></span>
	</label>
</body>
</html>
~~~

**文本新增伪类**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>文本新增</title>
	<style>
		p {width: 300px; border: 1px solid #000; font: 12px/30px "宋体"; padding: 10px;}
		p:first-line {background: red;}
		p:first-letter {font-size: 30px;} /*注意：通过:first-letter设置样式的文本是选不中的*/
		p::selection {background: #f60; color: #690;} /*文本被选中的样式 注意使用双冒号*/
		p::before {content: "MiaoV"; display: block; border: 1px solid #000;} /*::before和::after 单冒号和双冒号都认*/
		p::after {content: "MiaoV"; display: block; border: 1px solid #000;} 
	</style>
</head>
<body>
	<p>前端开发的世界从未有过无声的寂静，精彩纷呈的互联网也不曾出现片刻安宁，在HTML5&CSS3被炒至沸沸扬扬的今天，全面系统地掌握此项技能，是加重技术含金量的重要砝码！妙味课堂现已为你开启一个崭新的职业规划……</p>
</body>
</html>
~~~

**排除元素**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
	<style>
		h1:not(.h2) {background: red;}
	</style>
</head>
<body>
	<h1>h1</h1>
	<h1 class="h2">h1</h1>
	<h1>h1</h1>
</body>
</html>
~~~

##新增颜色模式

- rgba
	- r	Red		红		0-255
	- g	Green	绿		0-255
	- b	Blue	蓝		0-255
	- a	Alpha	透明	0-1
- 实例: 背景透明，文字不透明
- 问题：注意边框颜色透明有问题
- Hsl
	- H	Hue			色调	任意数值
	- S saturation  饱和度	0%-100%
	- L	Lightness	亮度	0%-100%

**背景透明、文字不透明**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>rgba</title>
	<style>
		body {background: green;}
		.box {width: 200px; height: 200px; background: rgba(0, 0, 0, 0.5); color: #fff; font: 40px/100px "微软雅黑"; text-align: center;} /*背景透明但文字不透明*/
	</style>
</head>
<body>
	<div class="box">妙味课堂</div>
</body>
</html>
~~~

**背景不透明、文字透明**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>rgba</title>
	<style>
		.box {width: 200px; height: 200px; background: green; color: rgba(255, 255, 255, 0.5); font: 80px/100px "微软雅黑"; text-align: center;} /*背景不透明但文字透明*/
	</style>
</head>
<body>
	<div class="box">妙味课堂</div>
</body>
</html>
~~~

**背景不透明、边框透明**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>rgba</title>
	<style>
		.box {width: 200px; height: 190px; background: green; color: rgba(255, 255, 255, 0.5); font: 80px/90px "微软雅黑"; text-align: center; border: 10px solid rgba(0, 0, 0, 0.3);} /*边框颜色透明，会把后面背景露出来*/
	</style>
</head>
<body>
	<div class="box">妙味课堂</div>
</body>
</html>
~~~

##文字阴影

- text-shadow：x y blur color, …
- 参数
	- x		横向偏移
	- y		纵向偏移
	- blur	模糊距离
	- color	阴影颜色
- 文本阴影如果加很多层，会很卡
- 文字阴影应用
	- 最简单用法
		- text-shadow:2px 2px 4px black
	- 阴影叠加
		- text-shadow:2px 2px 0px red, 2px 2px 4px green;
		- 先渲染后面的，再渲染前面的
	- 几个好玩的例子
		- 层叠：color:red; font-size:100px; font-weight:bold; text-shadow:2px 2px 0px white, 4px 4px 0px red;
		- 光晕：color:white; font-size:100px; text-shadow:0 0 10px #fff, 0 0 20px #fff, 0 0 30px #fff, 0 0 40px #ff00de, 0 0 70px #ff00de, 0 0 80px #ff00de, 0 0 100px #ff00de, 0 0 150px #ff00de;
		- 火焰文字：text-shadow: 0 0 20px #fefcc9, 10px -10px 30px #feec85, -20px -20px 40px #ffae34, 20px -40px 50px #ec760c, -20px -60px 60px #cd4606, 0 -80px 70px #973716, 10px -90px 80px #451b0e; font-family:Verdana, Geneva, sans-serif; font-size:100px; font-weight:bold; color:white;


**text-shadow基本应用**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>文字阴影</title>
	<style>
		h1 { font: 100px/200px "微软雅黑"; text-align: center; text-shadow: 0 0 10px red; }
	</style>
</head>
<body>
	<h1>妙味课堂</h1>
</body>
</html>
~~~

**文字阴影的叠加**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>文字阴影的叠加</title>
	<style>
		h1 { font: 100px/200px "微软雅黑"; text-align: center; text-shadow: -5px -10px 1px red, 5px 10px 2px green, 1px 1px 5px yellow; }
	</style>
</head>
<body>
	<h1>妙味课堂</h1>
</body>
</html>
~~~

**浮雕文字效果**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>文字阴影</title>
	<style>
		h1 { font: 100px/200px "微软雅黑"; text-align: center; color: #fff; text-shadow: 2px 2px 4px #000; }
	</style>
</head>
<body>
	<h1>妙味课堂</h1>
</body>
</html>
~~~

**文字模糊效果**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>文字模糊</title>
	<style>
		h1 { font: 100px/200px "微软雅黑"; text-align: center; color: #000; text-shadow: 0 0 0 rgba(0, 0, 0, 1); border: 1px solid #000; transition: 1s; }
		h1:hover {color: rgba(0, 0, 0, 0); text-shadow: 0 0 20px rgba(0, 0, 0, 0.5);}
	</style>
</head>
<body>
	<h1>妙味课堂</h1>
</body>
</html>
~~~

##文字描边

- -webkit-text-stroke:宽度 颜色 (只有webkit内核浏览器支持，一定要加-webkit-前缀)

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>文字描边</title>
	<style>
		h1 { font: 100px/200px "微软雅黑"; text-align: center; color: #000; -webkit-text-stroke: 3px red; }
	</style>
</head>
<body>
	<h1>妙味课堂</h1>
</body>
</html>
~~~

##新增文本功能

- direction  定义文字排列方式(全兼容)
	- rtl 从右向左排列
	- ltr 从右向左排列
	- 注意要配合unicode-bidi 一块使用

- text-overflow 定义省略文本的处理方式
	- clip  无省略号
	- ellipsis 省略号 (注意配合overflow:hidden和white- space:nowrap一块使用) 

**direction**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>文字排版</title>
	<style>
		p {width: 300px; border: 1px solid #000; font: 14px/30px "宋体"; direction: rtl; unicode-bidi: bidi-override;}
	</style>
</head>
<body>
	<p>妙味课堂</p>
</body>
</html>
~~~

**超出显示省略号**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>文字排版</title>
	<style>
		p {width: 300px; border: 1px solid #000; font: 14px/30px "宋体"; white-space: nowrap; overflow: hidden; text-overflow: ellipsis;}
	</style>
</head>
<body>
	<p>妙味课堂具有人性化的IT培训机构妙味课堂具有人性化的IT培训机构</p>
</body>
</html>
~~~

##自定义文字

- 格式

~~~ html
@font-face {
    font-family: 'miaov';
    src: url('111-webfont.eot');
    src: url('111-webfont.eot?#iefix') format('embedded-opentype'),
         url('111-webfont.woff') format('woff'),
         url('111-webfont.ttf') format('truetype'),
         url('111-webfont.svg#untitledregular') format('svg');
    font-weight: normal;
    font-style: normal;

}
~~~

- 转换字体格式生成兼容代码http://www.fontsquirrel.com/fontface/generator

##弹性盒模型

- 注意在使用弹性盒模型的时候，父元素必须要加display:box 或 display:inline-box
- box-orient 定义盒模型的布局方向
	- horizontal 水平显示
	- vertical 垂直方向
- box-direction 元素排列顺序
	- normal 正序
	- reverse 反序
- box-ordinal-group 设置元素的具体位置
- box-flex 定义盒子的弹性空间
	- 子元素的尺寸 = 盒子的尺寸 * 子元素的box-flex属性值 / 所有子元素的box-flex属性值的和
- box-pack 对盒子富裕的空间进行管理
	- start 所有子元素在盒子左侧显示，富裕空间在右侧
	- end 所有子元素在盒子右侧显示，富裕空间在左侧
	- center 所有子元素居中
	- justify 富裕空间在子元素之间平均分布
- box-align 在垂直方向上对元素的位置进行管理
	- start 所有子元素在居顶
	- end 所有子元素在居底
	- center 所有子元素居中

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>弹性盒模型</title>
	<style>
		.box {height: 100px; border: 10px solid #000; font-size: 20px; color: #fff; padding: 10px; display: -webkit-box; -webkit-box-orient: horizontal; }
		.box div {width: 100px; height: 100px; background: red; border: 1px solid #fff;}

		/* .box div:nth-of-type(1){-webkit-box-ordinal-group:2;}
		.box div:nth-of-type(2){-webkit-box-ordinal-group:4;}
		.box div:nth-of-type(3){-webkit-box-ordinal-group:1;}
		.box div:nth-of-type(4){-webkit-box-ordinal-group:5;}
		.box div:nth-of-type(5){-webkit-box-ordinal-group:3;} */

		.box div:nth-of-type(1){width: 300px;}
		.box div:nth-of-type(2){-webkit-box-flex:2;}
		.box div:nth-of-type(3){-webkit-box-flex:3;}
		.box div:nth-of-type(4){-webkit-box-flex:4;}
		.box div:nth-of-type(5){-webkit-box-flex:5;}

	</style>
</head>
<body>
	<div class="box">
		<div>1</div>
		<div>2</div>
		<div>3</div>
		<div>4</div>
		<div>5</div>
	</div>
</body>
</html>
~~~

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>弹性盒模型</title>
	<style>
		.box {height: 200px; border: 10px solid #000; font-size: 20px; color: #fff; padding: 10px; display: -webkit-box; -webkit-box-orient: horizontal; -webkit-box-direction: reverse; -webkit-box-pack: justify; -webkit-box-align: end;}
		.box div {width: 100px; height: 100px; background: red; border: 1px solid #fff;}
	</style>
</head>
<body>
	<div class="box">
		<div>1</div>
		<div>2</div>
		<div>3</div>
		<div>4</div>
		<div>5</div>
	</div>
</body>
</html>
~~~

##盒模型新增属性

###盒模型阴影

- 用法
	- box-shadow: [inset] x y blur [spread] color
	- 参数
		- inset: 内投影
		- 不给: 外投影
	- x、y: 阴影偏移
	- blur: 模糊半径
	- spread: 扩展阴影半径
		- 先扩展原有形状，再开始画阴影
	- color

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>盒模型阴影</title>
	<style>
		.box {width: 100px; height: 100px; margin: 100px; background: red; box-shadow: 0 0 30px 30px #000, inset 0 0 30px yellow;}
	</style>
</head>
<body>
	<div class="box"></div>
</body>
</html>
~~~

###box-reflect 倒影

- direction 方向 above | below | left | right;
- 距离
- 渐变（可选）
- 目前只有webkit内核支持

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>box-reflect 倒影</title>
	<style>
		img {display: block; margin: 30px auto; -webkit-box-reflect: below 10px -webkit-linear-gradient(bottom, rgba(0, 0, 0, 1) 0, rgba(0, 0, 0, 0) 70%)}
	</style>
</head>
<body>
	<img src="images/Green Nature Wallpapers 10.jpg" width="400">
</body>
</html>
~~~

###resize 自由缩放

- both 水平垂直都可以缩放
- horizontal 只有水平方向可以缩放
- vertical 只有垂直方向可以缩放
- 注意：一定要配合overflow:auto一块使用

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>resize 自由缩放</title>
	<style>
		.box {width: 100px; height: 100px; background: url('images/Green Nature Wallpapers 10.jpg'); border: 5px solid red; resize: both; overflow: auto;}
	</style>
</head>
<body>
	<div class="box"></div>
</body>
</html>
~~~

###box-sizing 盒模型解析模式

- content-box 标准盒模型
	- width/height = border + padding + content
- border-box 怪异盒模型
	- width/height = content

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>box-sizing</title>
	<style>
		.box {width: 200px; height: 200px; padding: 50px; border: 10px solid #000; box-sizing: border-box;}
		.div {height: 50px; background: red;}
	</style>
</head>
<body>
	<div class="box">
		<div class="div"></div>
	</div>
</body>
</html>
~~~

##CSS3分栏布局

- column-width 栏目宽度
- column-count 栏目列数
- column-gap 栏目距离
- column-rule 栏目间隔线

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>分栏布局</title>
	<style>
		/* .wrap {width: 900px; border: 1px solid #000; font: 14px/28px "宋体"; color: #000; text-indent: 2em; -webkit-column-width: 250px;} */
		.wrap {width: 900px; border: 1px solid #000; font: 14px/28px "宋体"; color: #000; text-indent: 2em; -webkit-column-count: 4; -webkit-column-gap: 30px; -webkit-column-rule: 1px dashed red;}
	</style>
</head>
<body>
	<div class="wrap">
		<p>按校科研处部署，我社2014年科研工作量统计工作安排如下：1. 申报者按要求如实填写《个人科研工作量计分表（2014）》（附件1）。2. 成果计分方法和科研工作量考核指标请参照《上海外国语大学科研工作量化标准与奖惩办法》（附件2）。成果奖励标准请参照《上海外国语大学优秀科</p>
		<p>按校科研处部署，我社2014年科研工作量统计工作安排如下：1. 申报者按要求如实填写《个人科研工作量计分表（2014）》（附件1）。2. 成果计分方法和科研工作量考核指标请参照《上海外国语大学科研工作量化标准与奖惩办法》（附件2）。成果奖励标准请参照《上海外国语大学优秀科</p>
		<p>按校科研处部署，我社2014年科研工作量统计工作安排如下：1. 申报者按要求如实填写《个人科研工作量计分表（2014）》（附件1）。2. 成果计分方法和科研工作量考核指标请参照《上海外国语大学科研工作量化标准与奖惩办法》（附件2）。成果奖励标准请参照《上海外国语大学优秀科</p>
		<p>按校科研处部署，我社2014年科研工作量统计工作安排如下：1. 申报者按要求如实填写《个人科研工作量计分表（2014）》（附件1）。2. 成果计分方法和科研工作量考核指标请参照《上海外国语大学科研工作量化标准与奖惩办法》（附件2）。成果奖励标准请参照《上海外国语大学优秀科</p>
		<p>按校科研处部署，我社2014年科研工作量统计工作安排如下：1. 申报者按要求如实填写《个人科研工作量计分表（2014）》（附件1）。2. 成果计分方法和科研工作量考核指标请参照《上海外国语大学科研工作量化标准与奖惩办法》（附件2）。成果奖励标准请参照《上海外国语大学优秀科</p>
		<p>按校科研处部署，我社2014年科研工作量统计工作安排如下：1. 申报者按要求如实填写《个人科研工作量计分表（2014）》（附件1）。2. 成果计分方法和科研工作量考核指标请参照《上海外国语大学科研工作量化标准与奖惩办法》（附件2）。成果奖励标准请参照《上海外国语大学优秀科</p>
		<p>按校科研处部署，我社2014年科研工作量统计工作安排如下：1. 申报者按要求如实填写《个人科研工作量计分表（2014）》（附件1）。2. 成果计分方法和科研工作量考核指标请参照《上海外国语大学科研工作量化标准与奖惩办法》（附件2）。成果奖励标准请参照《上海外国语大学优秀科</p>
		<p>按校科研处部署，我社2014年科研工作量统计工作安排如下：1. 申报者按要求如实填写《个人科研工作量计分表（2014）》（附件1）。2. 成果计分方法和科研工作量考核指标请参照《上海外国语大学科研工作量化标准与奖惩办法》（附件2）。成果奖励标准请参照《上海外国语大学优秀科</p>
	</div>
</body>
</html>
~~~

##CSS3响应式布局

- 媒体类型
	- all 所有媒体
	- braille 盲文触觉设备
	- embossed 盲文打印机
	- print 手持设备
	- projection 打印预览
	- screen 彩屏设备
	- speech “听觉”类似的媒体类型
	- tty 不适用像素的设备
	- tv 电视
- 关键字
	- and
	- not not关键字是用来排除某种制定的媒体类型
	- only only用来定某种特定的媒体类型
- 媒体特性
	- (max-width: 600px)
	- (max-device-width: 480px) 设备输出宽度
	- (orientation: portrait) 竖屏
	- (orientation: landscape) 横屏
	- (-webkit-min-device-pixel-ratio: 2) 像素比
		- devicePixelRatio 设备像素比 window.devicePixelRatio=物理像素/dips
- 样式引入
	- &lt;link rel="stylesheet" type="text/css" href="../css/print.css" media="print" />
	- @import url("css/reset.css") screen and (min-width: 400px);
	- @media screen and (min-width: 最小宽度) || (max-width: 最大宽度) { 选择器 { 属性 : 属性值; } }
	- &lt;link rel="stylesheet" media="all and (orientation:portrait)" href="portrait.css">
	- &lt;link rel="stylesheet" media="all and (orientation:landscape)" href="landscape.css">
	- @media screen and (min-width:400px) and (max-width:500px) {.box {margin: 0 auto;}}
	- &lt;link rel="stylesheet" type="text/css" href="styleA.css" media="screen and (min-width: 800px)">
	- &lt;link rel="stylesheet" type="text/css" href="styleB.css" media="screen and (min-width: 600px) and (max-width: 800px)">
	- &lt;link rel="stylesheet" type="text/css" href="styleC.css" media="screen and (max-width: 600px)">

##移动端meta

- &lt;meta name="viewport" content="" />
	- width [pixel_value | device-width]
	- height [pixel_value | device-height]
	- user-scalable 是否允许缩放 (no || yes)
	- initial-scale 初始比例
	- minimum-scale 允许缩放的最小比例
	- maximum-scale 允许缩放的最大比例
	- target-densitydpi [dpi_value | device-dpi | high-dpi | medium-dpi | low-dpi]

##圆角

- border-radius: 1-4个数字 / 1-4个数字
	- 前面是水平，后面是垂直
	- 不给“/”则水平和垂直一样
		- border-radius: 10px/5px;
- 参数
	- 各种长度单位都可以: px, %, ...
	- %有时很方便
		- 但宽高一致时不太好
- 用法
	- 1个：都一样
		- border-radius: 一样
	- 2个：对角
		- border-radius: 左上&右下 右上&左下
	- 3个：斜对角
		- border-radius：左上 右上&左下 右下
	- 4个：全部，顺时针
		- boder-radius：左上 右上 右下 左下

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>圆角</title>
	<style>
		/* .box {width: 200px; height: 200px; border: 1px solid #000; border-radius: 20px;} */
		/* .box {width: 200px; height: 200px; border: 1px solid #000; border-radius: 20px 40px;} */
		/* .box {width: 200px; height: 200px; border: 1px solid #000; border-radius: 20px 40px 60px;} */
		 .box {width: 200px; height: 200px; border: 1px solid #000; border-radius: 20px 40px 60px 80px;} 
	</style>
</head>
<body>
	<div class="box"></div>
</body>
</html>
~~~

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>圆角</title>
	<style>
		 /* .box {width: 200px; height: 300px; border: 1px solid #000; border-radius: 100px/150px;} */ /*X轴半径/y轴半径*/

		 .box {width: 200px; height: 300px; border: 1px solid #000; border-radius: 20px 40px 60px 80px/10px 20px 30px 40px;}
	</style>
</head>
<body>
	<div class="box"></div>
</body>
</html>
~~~

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>圆角</title>
	<style>.box {width: 200px; height: 300px; border: 1px solid #000; border-radius: 50%;}
	</style>
</head>
<body>
	<div class="box"></div>
</body>
</html>
~~~

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>圆角</title>
	<style>
		.box {width: 400px; height: 400px; margin: 50px auto; transition: 5s linear;}
		.box div {width: 180px; height: 180px; margin: 10px; border: 1px solid #000; box-sizing: border-box; float: left; background: url('images/Green Nature Wallpapers 10.jpg') no-repeat;}
		.box div:nth-child(1), .box div:nth-child(4) {border-radius: 0 70%;}
		.box div:nth-child(2), .box div:nth-child(3) {border-radius: 70% 0;}
		.box:hover {-webkit-transform: rotate(720deg);}
	</style>
</head>
<body>
	<div class="box">
		<div></div>
		<div></div>
		<div></div>
		<div></div>
	</div>
</body>
</html>
~~~

##边框

- 边框图片 border-image
	- border-image-source 引入图片
	- border-image-slice 切割图片
	- border-image-width 边框宽度
	- border-image-repeat 图片的排列方式
		- round 平铺；repeat 重复；stretch 拉伸
- 边框颜色 border-colors(多边框颜色只在firefox下实现了)

##线性渐变

- 线性渐变格式
	- linear-gradient([&lt;起点>||&lt;角度>,]?&lt;点>,&lt;点>...)
	- 只能用在背景上
		- IE (IE9及以下)
			- filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='#ffffff',endColorstr='#ff0000',GradientType='1');
	- 参数
		- 起点：从什么方向开始渐变 默认：top
			- left、top、left top
		- 角度：从什么角度开始渐变
			- xxx deg的形式
		- 点：渐变的颜色和位置
			- black 50%，位置可选

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>线性渐变</title>
	<style>
		/* .box {width: 300px; height: 300px; border: 10px solid #000; background-image: -webkit-linear-gradient(left top, red, blue);} */
		/* .box {width: 300px; height: 300px; border: 10px solid #000; background-image: -webkit-linear-gradient(30deg, red, blue, yellow, green);} */
		/* .box {width: 300px; height: 300px; border: 10px solid #000; background-image: -webkit-linear-gradient(30deg, red 30px, blue 100px);} */
		/* .box {width: 300px; height: 300px; border: 10px solid #000; background-image: -webkit-linear-gradient(30deg, red 0, blue 50%, green 100%);} */
		.box {width: 300px; height: 300px; border: 10px solid #000; background-image: -webkit-repeating-linear-gradient(30deg, red 0, blue 30px);}
	</style>
</head>
<body>
	<div class="box"></div>
</body>
</html>
~~~

- 线性渐变实例（1）
	- 最简单
		- red, green
		- 从上到下
	- 起点位置
		- left top, red, green
		- 30deg, red, green
			- 逆时针
	- repeating-linear-gradient
- 线性渐变实例（2）
	- 加入点的位置
		- top, red 40%, green 60%
		- top, red 50%, green 50%
			- 同一个位置两个点——直接跳变
		- 也可以用px
	- 配合rgba
		- top, rgba(255, 255, 255, 1), rgba(255, 255, 255, 0)
	- 加入背景图片
		- background: -webkit-linear-gradient(top, rgba(255, 255, 255, 1) 30%, rgba(255, 255, 255, 0)), url(a.gif)
- 实例：百度音乐图片光影效果

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>线性渐变</title>
	<style>
		.wrap {width: 200px; height: 30px; overflow: hidden; border: 1px solid #000;}
		.box {width: 400px; height: 30px; background: -webkit-repeating-linear-gradient(15deg, green 0, green 10px, #fff 10px, #fff 20px); transition: 3s linear;}
		.wrap:hover .box {margin-left: -100px;}
	</style>
</head>
<body>
	<div class="wrap">
		<div class="box"></div>
	</div>
</body>
</html>
~~~

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>线性渐变</title>
	<style>
		.box {width: 300px; height: 300px; background: url(img/ppt.gif) no-repeat, url(images/1.png) repeat-y right 0;}
	</style>
</head>
<body>
	<div class="box"></div>
</body>
</html>
~~~

**百度音乐图片光影效果**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>线性渐变</title>
	<style>
		.box {width: 300px; height: 300px; background: -webkit-linear-gradient(-30deg, rgba(255, 255, 255, 0) 0, rgba(255, 255, 255, 0) 155px, rgba(255, 255, 255, 0.9) 170px, rgba(255, 255, 255, 0.9) 180px, rgba(255, 255, 255, 0) 200px) no-repeat -190px, url('images/Green Nature Wallpapers 10.jpg') no-repeat; transition: 1s;}
		.box:hover {background-position: 300px 0, 0 0;}
	</style>
</head>
<body>
	<div class="box"></div>
</body>
</html>
~~~

**线性渐变——IE兼容**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>线性渐变——IE兼容</title>
	<style>
		.box {width: 300px; height: 300px; background: -webkit-linear-gradient(red, blue); background: -moz-linear-gradient(red, blue); background: linear-gradient(red, blue); filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='red',endColorstr='blue',GradientType='0');}
	</style>
</head>
<body>
	<div class="box"></div>
</body>
</html>
~~~

##径向渐变

- radial-gradient([&lt;起点>]?[&lt;形状>||&lt;大小>,]?&lt;点>,&lt;点>...);
	- 起点：可以是关键字（left, top, right, bottom)，具体数值或百分比
	- 形状：ellipse, circle
	- 大小：具体数值或百分比，也可以是关键字(最近端，最近角，最远端，最远角，包含或覆盖(closest-side, closest-corner, farthest-sice, farthest-corner, contain or cover));
		- 注意firefox目前只支持关键字

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>径向渐变</title>
	<style>
		.box {width: 300px; height: 300px; border: 1px solid #000; float: left; margin: 10px;}
		.box:nth-child(1) {background: -webkit-radial-gradient(100px 50px, closest-side, red, blue);}
		.box:nth-child(2) {background: -webkit-radial-gradient(100px 50px, closest-corner, red, blue);}
		.box:nth-child(3) {background: -webkit-radial-gradient(100px 50px, farthest-side, red, blue);}
		.box:nth-child(4) {background: -webkit-radial-gradient(100px 50px, farthest-corner, red, blue);}
		.box:nth-child(5) {background: -webkit-radial-gradient(100px 50px, contain, red, blue);}
		.box:nth-child(6) {background: -webkit-radial-gradient(100px 50px, cover, red, blue);}
	</style>
</head>
<body>
	<div class="box"></div>
	<div class="box"></div>
	<div class="box"></div>
	<div class="box"></div>
	<div class="box"></div>
	<div class="box"></div>
</body>
</html>
~~~

##背景

- 多背景
	- 逗号分开
		- background: url(a.jpg) 0 0, url(b.jpg) 0 10%;
- 背景尺寸
	- background-size: x y
		- background-size: 100% 100%
		- cover 放大
		- contain 缩小
- background-origin: border | padding | content
	- border-box: 从border区域开始显示背景
	- padding-box: 从padding区域开始显示背景
	- content-box: 从content区域开始显示背景
- background-clip
	- border: 从border区域向外裁剪背景
	- padding: 从padding区域向外裁剪背景
	- content: 从content区域向外裁剪背景
	- no-clip: 从border区域向外裁剪背景
	- text: 只给文字添加背景，文字以外的背景都裁剪掉
- 实例：iphone开机动画

**iphone开机动画**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>iphone开机动画</title>
	<style>
		body {background: #000; text-align: center; font: 50px/200px "微软雅黑";}
		h1 {display: inline-block; color: rgba(255, 255, 255, 0.3); background: -webkit-linear-gradient(-30deg, rgba(255, 255, 255, 0) 100px, rgba(255, 255, 255, 1) 180px, rgba(255, 255, 255, 1) 240px, rgba(255, 255, 255, 0) 300px) no-repeat -300px; -webkit-background-clip: text;}
	</style>
	<script>
		window.onload = function(){
			var oH1 = document.getElementsByTagName('h1')[0];
			var oTimer = null;
			var iLeft = -300;

			function toMove(){
				oTimer = setInterval(function(){
					iLeft+=10;
					if(iLeft == 1000){
						iLeft = -300;
						clearInterval(oTimer);
					}
					oH1.style.backgroundPosition = iLeft + 'px 0px';
					
				}, 20)
			}
			
			setInterval(function(){
				toMove();
			}, 4000)
		}
	</script>
</head>
<body>
	<h1>MiaoV妙味课堂</h1>
</body>
</html>
~~~

##遮罩

- mask-image
- mask-position
- mask-repeat
- 实例：特殊形状的幻灯片效果

##transition过渡

- transition-property 要运动的样式 ( all || [attr] || none )
- transition-duration 运动时间
- transition-delay 延迟时间
- transition-timing-function 运动形式
	- ease : (逐渐变慢) 默认值
	- linear : (匀速)
	- ease-in : (加速)
	- ease-out : (减速)
	- ease-in-out : (先加速后减速)
	- cubic-bezier : 贝塞尔曲线 (x1, y1, x2, y2) http://matthewlein.com/ceaser
- 实例 : 幻灯片效果
- 过渡完成事件
	- webkit内核 :
		- obj.addEventListener('webkitTransitionEnd', function(){}, false);
	- firefox : 
		- obj.addEventListener('transitionend', function(){}, false);
- 实例1 : 苹果产品展示
- 实例2 : 360浏览器 ipad版导航

**transition的基本操作**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>transition</title>
	<style>
		.box {width: 100px; height: 100px; background: red;}
		/* .box {transition: 1s;} */
		/*.box {transition: 500ms width;}*/
		/*.box {transition: 1s all;}*/
		/*.box {transition: 3s width ease;}*/
		/*.box {transition: 3s width ease-in-out;}*/
		/*.box {transition: 3s width cubic-bezier(0.930, 0.415, 0.000, 1.610);}*/
		/* .box {transition: 1s width, 2s height, 3s background;} */ /*多样式过渡*/
		/*.box {transition: 1s width, 2s 1s height, 3s 3s background;}*/ /*延迟过渡*/
		.box:hover {background: blue; width: 500px; height: 300px;}
	</style>
	<script>
		
	</script>
</head>
<body>
	<div class="box"></div>
</body>
</html>
~~~

**过渡完成的事件以及问题一**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>transition</title>
	<style>
		.box {width: 100px; height: 100px; background: red; transition: 1s width, 2s height;}
	</style>
	<script>
		
	</script>
</head>
<body>
	<div class="box" id="box"></div>
	<script>
		var oBox = document.getElementById('box');

		//用transitionend事件，每个属性改变完一次就会触发一次
		oBox.onclick = function(){
			this.style.width = this.offsetWidth + 100 + 'px'; 
			this.style.height = this.offsetHeight + 100 + 'px';
		}
		addEnd(oBox, function(){
			alert('end');
		});

		function addEnd(obj, fn){
			obj.addEventListener('webkitTransitionEnd', fn, false);
			obj.addEventListener('transitionend', fn, false);
		}
	</script>
</body>
</html>
~~~

**过渡完成的事件以及问题二**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>transition</title>
	<style>
		.box {width: 100px; height: 100px; background: red; transition: 1s width}
	</style>
	<script>
		
	</script>
</head>
<body>
	<div class="box" id="box"></div>
	<script>
		var oBox = document.getElementById('box');

		oBox.onclick = function(){
			this.style.width = this.offsetWidth + 100 + 'px'; 
		}

		//transitonend之后，又改变属性，接着又触发了transition就形成了循环
		addEnd(oBox, function(){
			this.style.width = this.offsetWidth + 100 + 'px';
		});

		function addEnd(obj, fn){
			obj.addEventListener('webkitTransitionEnd', fn, false);
			obj.addEventListener('transitionend', fn, false);
		}
	</script>
</body>
</html>
~~~

**过渡完成事件问题二的处理方法**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>transition</title>
	<style>
		.box {width: 100px; height: 100px; background: red; transition: 1s width}
	</style>
	<script>
		
	</script>
</head>
<body>
	<div class="box" id="box"></div>
	<script>
		var oBox = document.getElementById('box');

		oBox.onclick = function(){
			this.style.width = this.offsetWidth + 100 + 'px'; 
			addEnd(oBox, end);
		}

		function end(){
			this.style.width = this.offsetWidth + 100 + 'px';
			removeEnd(this, end);
		}

		function addEnd(obj, fn){
			obj.addEventListener('webkitTransitionEnd', fn, false);
			obj.addEventListener('transitionend', fn, false);
		}

		function removeEnd(obj, fn){
			obj.removeEventListener('webkitTransitionEnd', fn, false);
			obj.removeEventListener('transitionend', fn, false);
		}
	</script>
</body>
</html>
~~~

##2D变换

- transform
	- rotate() 旋转函数 取值度数
		- deg 度数
		- transform-origin 旋转的基点
	- skew() 倾斜函数 取值度数
		- skewX()
		- skewY()
	- scale() 缩放函数 取值 正数、负数和小数
		- scaleX()
		- scaleY()
	- translate() 位移函数
		- translateX()
		- translateY()
- 实例1 : 钟表效果
- 实例2 : 怪异的导航

**旋转**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>旋转</title>
	<style>
		body {height: 400px; border: 1px solid #000;}
		.box {width: 100px; height: 100px; background: red; margin:100px auto 0; transition: 2s;}
		body:hover .box {-webkit-transform: rotate(30deg); -moz-transform: rotate(30deg);}
	</style>
	<script>
		
	</script>
</head>
<body>
	<div class="box" id="box">123</div>
</body>
</html>
~~~

**斜切**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>斜切</title>
	<style>
		body {height: 400px; border: 1px solid #000;}
		.box {width: 100px; height: 100px; background: red; margin:100px auto 0; transition: 2s;}
		/* body:hover .box {-webkit-transform: skewX(45deg); -moz-transform: skewX(45deg);} */
		/* body:hover .box {-webkit-transform: skewY(45deg); -moz-transform: skewY(45deg);} */
		body:hover .box {-webkit-transform: skew(15deg, 30deg); -moz-transform: skew(15deg, 30deg);}	
	</style>
	<script>
		
	</script>
</head>
<body>
	<div class="box" id="box">123</div>
</body>
</html>
~~~

**怪异导航**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>怪异导航</title>
	<style>
		ul {margin: 0; padding: 0; list-style: none;}
		li {float: left; width: 100px; text-align: center; height: 30px; border: 1px solid #fff; background: red; font: 12px/30px "宋体"; -moz-transform: skewX(30deg); -webkit-transform: skewX(30deg);}
		a {display: block; text-decoration: none; -moz-transform: skewX(-30deg); -webkit-transform: skewX(-30deg);}
	</style>
</head>
<body>
	<ul>
		<li><a href="#">妙味课堂</a></li>
		<li><a href="#">妙味茶馆</a></li>
	</ul>	
</body>
</html>
~~~

**缩放**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>缩放</title>
	<style>
		body {height: 400px; border: 1px solid #000;}
		.box {width: 100px; height: 100px; background: red; margin: 100px auto 0; transition: 2s;}
		/* body:hover .box {-webkit-transform: scaleX(0.5); -moz-transform: scaleX(0.5);} */
		body:hover .box {-webkit-transform: scale(0.5, -2); -moz-transform: scale(0.5, -2);}
	</style>
</head>
<body>
	<div class="box">123</div>	
</body>
</html>
~~~

**位移**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>位移</title>
	<style>
		body {height: 400px; border: 1px solid #000;}
		.box {width: 100px; height: 100px; background: red; margin: 100px auto 0; transition: 2s;}
		/* body:hover .box {-webkit-transform: translateX(100px); -moz-transform: translateX(100px);} */
		body:hover .box {-webkit-transform: translate(100px, -20px); -moz-transform: translate(100px, -20px);}
	</style>
</head>
<body>
	<div class="box">123</div>	
</body>
</html>
~~~

**transform的基点**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>transform的基点</title>
	<style>
		/* body {height: 300px; border: 1px solid #000;}
		.box {width: 100px; height: 100px; background: red; margin: 100px auto; transition: 5s; -webkit-transform-origin: right top; -moz-transform-origin: right top;} */
		body {height: 300px; border: 1px solid #000;}
		.box {width: 100px; height: 100px; background: red; margin: 100px auto; transition: 5s; -webkit-transform-origin: 10px 20px; -moz-transform-origin: 10px 20px;} /*transform-origin: 0 0; 如果是0 0就是左上角*/
		body:hover .box {-webkit-transform: rotate(360deg) scale(0.2); -moz-transform: rotate(360deg) scale(0.2);}
	</style>
</head>
<body>
	<div class="box"></div>
</body>
</html>
~~~

- transform 执行顺序问题 —— 后写先执行
- matrix(a,b,c,d,e,f) 矩阵函数
	- 通过矩阵实现缩放
		- x轴缩放 a=x*a c=x*c e=x*e
		- y轴缩放 b=y*b d=y*d f=y*f
	- 通过矩阵实现位移
		- x轴位移 e=e+x
		- y轴位移 f=f+y
	- 通过矩阵实现倾斜
		- x轴倾斜 c=Math.tan(xDeg/180*Math.PI)
		- y轴倾斜 b=Math.tan(yDeg/180*Math.PI)
	- 通过矩阵实现旋转
		- a=Math.cos(deg/180*Math.PI);
		- b=Math.sin(deg/180*Math.PI);
		- c=-Math.sin(deg/180*Math.PI);
		- d=Math.cos(deg/180*Math.PI);
- 变换兼容IE9以下IE版本只能通过矩阵来实现
	- filter:progid:DXImageTransform.Microsoft.Matric(M11=1, M12=0, M21=0, M22=1, SizingMethod='auto expand');
	- IE下的矩阵没有E和F两个参数 M11==a; M12==c; M21==b; M22==d

**transform执行顺序问题**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>transform的执行顺序问题</title>
	<style>
		body {height: 300px; border: 1px solid #000;}
		.box {width: 100px; height: 100px; background: red; margin: 10px; transition: 1s;} 
		body:hover .box:nth-of-type(1) {-webkit-transform: translateX(100px) scale(0.5); -moz-transform: translateX(100px) scale(0.5);}
		body:hover .box:nth-of-type(2) {-webkit-transform: scale(0.5) translateX(100px); -moz-transform: scale(0.5) translateX(100px); }/*第二个div的变化，scale在前，translate在后。后写的限制性，就是先位移再缩放，那么位移设置的100也被缩放了0.5，因此实际只位移了50px*/		
		
	</style>
</head>
<body>
	<div class="box">111</div>
	<div class="box">222</div>
</body>
</html>
~~~

**钟表效果**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>钟表效果</title>
	<style id="css">
		 #wrap {width: 200px; height: 200px; border: 2px solid #000; margin: 100px auto; border-radius: 50%; position: relative;}
		 #wrap ul {margin: 0; padding: 0; height: 200px; position: relative; list-style: none;}
		 #wrap ul li {width: 2px; height: 6px; background: #000; position: absolute; left: 99px; top: 0; -webkit-transform-origin: center 100px; -moz-transform-origin: center 100px;}
		 /* #wrap ul li:nth-of-type(1) {-webkit-transform: rotate(0); -moz-transform: rotate(0);}
		 #wrap ul li:nth-of-type(2) {-webkit-transform: rotate(6deg); -moz-transform: rotate(6deg);}
		 #wrap ul li:nth-of-type(3) {-webkit-transform: rotate(12deg); -moz-transform: rotate(12deg);}
		 #wrap ul li:nth-of-type(4) {-webkit-transform: rotate(18deg); -moz-transform: rotate(18deg);}
		 #wrap ul li:nth-of-type(5) {-webkit-transform: rotate(24deg); -moz-transform: rotate(24deg);}
		 #wrap ul li:nth-of-type(6) {-webkit-transform: rotate(30deg); -moz-transform: rotate(30deg);}
		 #wrap ul li:nth-of-type(7) {-webkit-transform: rotate(36deg); -moz-transform: rotate(36deg);}
		 #wrap ul li:nth-of-type(8) {-webkit-transform: rotate(42deg); -moz-transform: rotate(42deg);} */
		 #wrap ul li:nth-of-type(5n+1) {height: 12px;}
		 #hour {width: 6px; height: 45px; background: #000; position: absolute; left: 97px; top: 55px; -webkit-transform-origin: bottom; -moz-transform-origin: bottom;}
		 #min {width: 4px; height: 65px; background: #999; position: absolute; left: 98px; top: 35px; -webkit-transform-origin: bottom; -moz-transform-origin: bottom;}
		 #sec {width: 2px; height: 80px; background: red; position: absolute; left: 99px; top: 20px; -webkit-transform-origin: bottom; -moz-transform-origin: bottom;}
		 .ico {width: 20px; height: 20px; background: #000; border-radius: 50%; position: absolute; left: 90px; top: 90px;}
	</style>
</head>
<body>
	<div id="wrap">
		<ul id="ul1">
			<!-- <li></li>
			<li></li>
			<li></li>
			<li></li>
			<li></li>
			<li></li>
			<li></li>
			<li></li> -->
		</ul>
		<div id="hour"></div>
		<div id="min"></div>
		<div id="sec"></div>
		<div class="ico"></div>
	</div>
	<script>
		var oList = document.getElementById('ul1');
		var oCss = document.getElementById('css');
		var oHour = document.getElementById('hour');
		var oMin = document.getElementById('min');
		var oSec = document.getElementById('sec');
		var aLi = '';
		var sCss = '';
		for(var i=0; i<60; i++){
			sCss += '#wrap ul li:nth-of-type(' + (i+1) + ') {-webkit-transform: rotate(' + i*6 + 'deg); -moz-transform: rotate(' + i*6 + 'deg);}'
			aLi += '<li></li>'
		}
		oList.innerHTML = aLi;
		oCss.innerHTML += sCss;
		toTime();
		setInterval(toTime, 1000);
		function toTime(){
			var oDate = new Date();
			var iSec = oDate.getSeconds();
			var iMin = oDate.getMinutes() + iSec/60;
			var iHour = oDate.getHours() + iMin/60;

			oSec.style.WebkitTransform = 'rotate(' + iSec *6 + 'deg)';
			oSec.style.MozTransform = 'rotate(' + iSec *6 + 'deg)';

			oMin.style.WebkitTransform = 'rotate(' + iMin *6 + 'deg)';
			oMin.style.MozTransform = 'rotate(' + iMin *6 + 'deg)';

			oHour.style.WebkitTransform = 'rotate(' + iHour *30 + 'deg)';
			oHour.style.MozTransform = 'rotate(' + iHour *30 + 'deg)';
		}
	</script>
</body>
</html>
~~~

**扇形导航**

~~~ html
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>无标题文档</title>
<style>
body{ background:#f9f9f9;}
#menu{width:50px;height:50px; position:fixed;right:20px; bottom:20px; }
#menu_list{height:42px;width:42px; position:relative;margin:4px;}
#menu_list img{ border-radius:21px; position:absolute;left:0;top:0; -webkit-transition:0.5s all ease;}
#home{width:50px;height:50px;background:url(home.png) no-repeat; border-radius:25px; position:absolute; left:0;top:0; transition:1s;}
</style>
<script>
window.onload=function()
{
	var oHome=document.getElementById("home");
	var aImg=document.getElementById("menu_list").getElementsByTagName("img");
	var bOff=true;
	var iR=-150;
	for(var i=0;i<aImg.length;i++)
	{
		aImg[i].onclick=function()
		{
			this.style.transition="0.3s";
			this.style.WebkitTransform="scale(2) rotate(-720deg)";
			this.style.opacity=0.1;
			addEnd(this,end);
		};
	}
	function end()
	{
		this.style.transition="0.1s";
		this.style.WebkitTransform="scale(1) rotate(-720deg)";
		this.style.opacity=1;
		removeEnd(this,end);
	}
	oHome.onclick=function()
	{
		if(bOff)
		{
			this.style.WebkitTransform="rotate(-360deg)";
			for(var i=0;i<aImg.length;i++)
			{
				var oLt=toLT(iR,90/4*i);
				aImg[i].style.transition="0.5s "+i*100+"ms";
				aImg[i].style.left=oLt.l+"px";
				aImg[i].style.top=oLt.t+"px";
				aImg[i].style.WebkitTransform="scale(1) rotate(-720deg)";
			}
		}
		else
		{
			this.style.WebkitTransform="rotate(0deg)";
			for(var i=0;i<aImg.length;i++)
			{
				aImg[i].style.transition="0.5s "+(aImg.length-i-1)*100+"ms";
				aImg[i].style.left=0+"px";
				aImg[i].style.top=0+"px";
				aImg[i].style.WebkitTransform="scale(1) rotate(0deg)";
			}
		}
		bOff=!bOff;
	};
};
function toLT(iR,iDeg)
{
	return {l:Math.round(Math.sin(iDeg/180*Math.PI)*iR),t:Math.round(Math.cos(iDeg/180*Math.PI)*iR)}
}
function addEnd(obj,fn)
{
	obj.addEventListener('WebkitTransitionEnd',fn,false);
	obj.addEventListener('transitionend',fn,false);
}
function removeEnd(obj,fn)
{
	obj.removeEventListener('WebkitTransitionEnd',fn,false);
	obj.removeEventListener('transitionend',fn,false);
}
/*
	已知直角三角形的斜边长度和夹角 求对边(sin)和临边的长度
*/
</script>
</head>
<body>
<div id="menu">
	<div id="menu_list">
    	<img src="prev.png" alt=""/>
        <img src="open.png" alt="" />
        <img src="clos.png" alt="" />
        <img src="full.png" alt="" />
        <img src="refresh.png" alt="" />
    </div>
	<div id="home"></div>
</div>
</body>
</html>
~~~

**Matrix矩阵**

~~~ html
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>2d变换——Matrix矩阵</title>
<style>
	.box {width: 100px; height: 100px; background: red; transition: 1s;}
	.box:hover {-webkit-transform: matrix(0.5,0.38,-0.38,2,0,0); -moz-transform: matrix(0.5,0.38,-0.38,2,0,0);}
	/*
		标准浏览器：
		matrix(1,0,0,1,0,0) 默认情况
		matrix(a,b,c,d,e,f) 六个参数

		IE浏览器：
		filter: progid:DXImageTransform.Microsoft.Matrix(M11=1, M12=0, M21=0, M22=1, SizingMethod='auto expand');
		Matrix(M11==a, M12==c, M21==b, M22==d) 只有四个参数，而且顺序与标准下不同

	 */
</style>
</head>
<body>
	<div class="box"></div>
</body>
</html>
~~~

**通过矩阵Matrix实现位移**

~~~ html
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>通过矩阵Matrix实现位移</title>
<style>
	/*
		matrix(a,b,c,d,e,f) 六个参数
		位移：两个方向
			x： 参数e代表x轴的位移 e+disX
			y： 参数f代表y轴的位移 f+disY

		IE下没有e、f两个参数，因此无法直接实现位移，但是可以用定位来替换实现效果
	 */
	body {height: 300px; border: 1px solid #000;}
	.box {width: 100px; height: 100px; background: red; transition: 1s;}
	body:hover .box {-webkit-transform: matrix(1,0,0,1,100,300); -moz-transform: matrix(1,0,0,1,100,300);}
</style>
</head>
<body>
	<div class="box"></div>
</body>
</html>
~~~

**通过矩阵Matrix实现缩放**

~~~ html
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>通过矩阵Matrix实现缩放</title>
<style>
	/*
		matrix(a,b,c,d,e,f) 六个参数
		缩放：
			x轴缩放 a=x*a c=x*c e=x*e
			y轴缩放 b=y*b d=y*d f=y*f
	 */
	body {height: 300px; border: 1px solid #000;}
	.box {width: 100px; height: 100px; background: red; transition: 1s;}
</style>
</head>
<body>
	<div class="box" id="box"></div>
	<script>
		var oBox = document.getElementById('box');
		oBox.onclick = function(){
			oBox.style.WebkitTransform = 'matrix(0.5,0,0,0.2,0,0)';
			oBox.style.MozTransform = 'matrix(0.5,0,0,0.2,0,0)';
			oBox.style.transform = 'matrix(0.5,0,0,0.2,0,0)';
			oBox.style.filter = 'progid:DXImageTransform.Microsoft.Matrix(M11=0.5, M12=0, M21=0, M22=0.2, SizingMethod="auto expand")';
		}
	</script>
</body>
</html>
~~~

**通过矩阵Matrix实现倾斜**

~~~ html
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>通过矩阵Matrix实现倾斜</title>
<style>
	/*
		matrix(a,b,c,d,e,f) 六个参数
		倾斜：
			x轴倾斜 c=Math.tan(xDeg/180*Math.PI)
			y轴倾斜 b=Math.tan(yDeg/180*Math.PI)
	 */
	body {height: 300px; border: 1px solid #000;}
	.box {width: 100px; height: 100px; background: red; transition: 1s;}
</style>
</head>
<body>
	<div class="box" id="box"></div>
	<script>
		//Math.tan(30/180*Math.PI)约等于0.58
		var oBox = document.getElementById('box');
		oBox.onclick = function(){
			oBox.style.WebkitTransform = 'matrix(1,0, 0.58,1,0,0)';
			oBox.style.MozTransform = 'matrix(1,0,0.58,1,0,0)';
			oBox.style.transform = 'matrix(1,0,0.58,1,0,0)';
			oBox.style.filter = 'progid:DXImageTransform.Microsoft.Matrix(M11=1, M12=0.58, M21=0, M22=1, SizingMethod="auto expand")';
		}
	</script>
</body>
</html>
~~~

**通过矩阵Matrix实现旋转**

~~~ html
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>通过矩阵Matrix实现旋转</title>
<style>
	/*
		matrix(a,b,c,d,e,f) 六个参数
		旋转：
			a=Math.cos(deg/180*Math.PI);
			b=Math.sin(deg/180*Math.PI);
			c=-Math.sin(deg/180*Math.PI);
			d=Math.cos(deg/180*Math.PI);
	 */
	body {height: 300px; border: 1px solid #000;}
	.box {width: 100px; height: 100px; background: red; transition: 1s;}
</style>
</head>
<body>
	<div class="box" id="box"></div>
	<script>
		//Math.sin(30/180*Math.PI) 约为0.5
		//Math.cos(30/180*Math.PI) 约为0.87
		var oBox = document.getElementById('box');
		oBox.onclick = function(){
			oBox.style.WebkitTransform = 'matrix(0.87,0.5, -0.5,0.87,0,0)';
			oBox.style.MozTransform = 'matrix(0.87,0.5, -0.5,0.87,0,0)';
			oBox.style.transform = 'matrix(0.87,0.5, -0.5,0.87,0,0)';
			oBox.style.filter = 'progid:DXImageTransform.Microsoft.Matrix(M11=0.87, M12=0.5, M21=-0.5, M22=0.87, SizingMethod="auto expand")';

			// alert(this.offsetWidth);
		}
	</script>
</body>
</html>
~~~

**IE下的基点修正**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>IE基点修正</title>
	<style>
		.box {width: 100px; height: 100px; margin: 30px auto; position: relative; border: 1px solid #000;}
		#box {width: 100px; height: 100px; background: red; position: absolute; left: 0; top: 0;}
		/*#box:hover {-webkit-transform: rotate(360deg); -moz-transform: rotate(360deg);}*/
	</style>
</head>
<body>
	<div class="box">
		<div id="box"></div>
	</div>	
	<script>
		var oBox = document.getElementById('box');
		var iDeg = 0;
		setInterval(function(){
			iDeg++;
			toRotate(oBox, iDeg)
		}, 30)
		function toRotate(obj, iDeg){
			var a = Math.round(Math.cos(iDeg/180*Math.PI)*100)/100; //乘以100之后四舍五入，然后除以100
			var b = Math.round(Math.sin(iDeg/180*Math.PI)*100)/100;
			var c = -b;
			var d = a;

			obj.style.WebkitTransform = 'matrix(' + a + ',' + b + ', ' + c + ',' + d + ',0,0)';
			obj.style.MozTransform = 'matrix(' + a + ',' + b + ', ' + c + ',' + d + ',0,0)';
			obj.style.transform = 'matrix(' + a + ',' + b + ', ' + c + ',' + d + ',0,0)';
			obj.style.filter = 'progid:DXImageTransform.Microsoft.Matrix(M11=' + a + ', M12=' + c + ', M21=' + b + ', M22=' + d + ', SizingMethod="auto expand")';
			
			//下面两行修正IE下的基点问题
			obj.style.left = (obj.parentNode.offsetWidth-obj.offsetWidth)/2 + 'px';
			obj.style.top = (obj.parentNode.offsetHeight-obj.offsetHeight)/2 + 'px';
		}
	</script>
</body>
</html>
~~~

##3d变换

- transform-style (preserve-3d) 建立3D空间
- perspective 景深
- perspective-origin 景深基点: 视线是从哪个方向看过去的
- transform 新增函数
	- rotateX()
	- rotateY()
	- rotateZ()
	- translateZ()
	- scaleZ()
- 实例1 : 3D盒子
- 实例2 : 3D图片切换

**3d旋转**

~~~ html
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>3d变换</title>
<style>
	.box {width: 100px; height: 100px; padding: 100px; border: 5px solid #000; margin: 30px auto; -webkit-transform-style: preserve-3d; -moz-transform-style: preserve-3d; -webkit-perspective: 100px; -moz-perspective: 100px;}
	.div {width: 100px; height: 100px; background: red; transition: 1s;}
	/* .box:hover .div {-webkit-transform: rotateX(180deg); -moz-transform: rotateX(180deg);} */
	.box:hover .div {-webkit-transform: rotateY(180deg); -moz-transform: rotateY(180deg);}
	/* .box:hover .div {-webkit-transform: rotateZ(180deg); -moz-transform: rotateZ(180deg);}  */
</style>
</head>
<body>
	<div class="box">
		<div class="div">111</div>
	</div>
</body>
</html>
~~~

**3d的translateZ**

~~~ html
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>3d变换</title>
<style>
	.box {width: 100px; height: 100px; padding: 100px; border: 5px solid #000; margin: 30px auto; -webkit-transform-style: preserve-3d; -moz-transform-style: preserve-3d; -webkit-perspective: 200px; -moz-perspective: 200px;}
	.div {width: 100px; height: 100px; background: red; transition: 1s;}
	.box:hover .div {-webkit-transform: translateZ(100px); -moz-transform: translateZ(100px);}
</style>
</head>
<body>
	<div class="box">
		<div class="div">111</div>
	</div>
</body>
</html>
~~~

**3d小盒子**

~~~ html
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title></title>
<style>
	.wrap {width: 100px; height: 100px; padding: 100px; border: 5px solid #000; margin: 100px auto; -webkit-perspective: 200px; -moz-perspective: 200px;}
	.box {width: 100px; height: 100px; background: red; position: relative; -webkit-transform-style: preserve-3d; -moz-transform-style: preserve-3d; transition: 2s; -webkit-transform-origin: center center -50px; -moz-transform-origin: center center -50px;}
	.box div {width: 100px; height: 100px; position: absolute; color: #fff; font-size: 50px; text-align: center; line-height: 100px;}
	.box div:nth-of-type(1) {left: 0; top: -100px; background: #9c0; -webkit-transform-origin: bottom; -moz-transform-origin: bottom; -webkit-transform: rotateX(90deg); -moz-transform: rotateX(90deg);}
	.box div:nth-of-type(2) {left: -100px; top: 0; background: #cf3; -webkit-transform-origin: right; -moz-transform-origin: right; -webkit-transform: rotateY(-90deg); -moz-transform: rotateY(-90deg);}
	.box div:nth-of-type(3) {left: 0; top: 0; background: #ccf;}
	.box div:nth-of-type(4) {left: 100px; top: 0; background: #0c9; -webkit-transform-origin: left; -moz-transform-origin: left; -webkit-transform: rotateY(90deg); -moz-transform: rotateY(90deg);}
	.box div:nth-of-type(5) {left: 0; top: 100px; background: #69c; -webkit-transform-origin: top; -moz-transform-origin: top; -webkit-transform: rotateX(-90deg); -moz-transform: rotateX(-90deg);}
	.box div:nth-of-type(6) {left: 0; top: 0; background: #f0c; -webkit-transform: translateZ(-100px) rotateX(180deg); -moz-transform: translateZ(-100px) rotateX(180deg); }
	.wrap:hover .box {-webkit-transform: rotateX(180deg); -moz-transform: rotateX(180deg);}
</style>
</head>
<body>
	<div class="wrap">
		<div class="box">
			<div>1</div>
			<div>2</div>
			<div>3</div>
			<div>4</div>
			<div>5</div>
			<div>6</div>
		</div>
	</div>
</body>
</html>
~~~

**景深基点**

~~~ html
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title></title>
<style>
	.wrap {width: 100px; height: 100px; padding: 100px; border: 5px solid #000; margin: 100px auto; -webkit-perspective: 200px; -moz-perspective: 200px; -webkit-perspective-origin: left top; -moz-perspective-origin: left top;}
	.box {width: 100px; height: 100px; background: red; position: relative; -webkit-transform-style: preserve-3d; -moz-transform-style: preserve-3d; transition: 2s; -webkit-transform-origin: center center -50px; -moz-transform-origin: center center -50px;}
	.box div {width: 100px; height: 100px; position: absolute; color: #fff; font-size: 50px; text-align: center; line-height: 100px;}
	.box div:nth-of-type(1) {left: 0; top: -100px; background: #9c0; -webkit-transform-origin: bottom; -moz-transform-origin: bottom; -webkit-transform: rotateX(90deg); -moz-transform: rotateX(90deg);}
	.box div:nth-of-type(2) {left: -100px; top: 0; background: #cf3; -webkit-transform-origin: right; -moz-transform-origin: right; -webkit-transform: rotateY(-90deg); -moz-transform: rotateY(-90deg);}
	.box div:nth-of-type(3) {left: 0; top: 0; background: #ccf;}
	.box div:nth-of-type(4) {left: 100px; top: 0; background: #0c9; -webkit-transform-origin: left; -moz-transform-origin: left; -webkit-transform: rotateY(90deg); -moz-transform: rotateY(90deg);}
	.box div:nth-of-type(5) {left: 0; top: 100px; background: #69c; -webkit-transform-origin: top; -moz-transform-origin: top; -webkit-transform: rotateX(-90deg); -moz-transform: rotateX(-90deg);}
	.box div:nth-of-type(6) {left: 0; top: 0; background: #f0c; -webkit-transform: translateZ(-100px) rotateX(180deg); -moz-transform: translateZ(-100px) rotateX(180deg); }
	.wrap:hover .box {-webkit-transform: rotateX(180deg); -moz-transform: rotateX(180deg);}
</style>
</head>
<body>
	<div class="wrap">
		<div class="box">
			<div>1</div>
			<div>2</div>
			<div>3</div>
			<div>4</div>
			<div>5</div>
			<div>6</div>
		</div>
	</div>
</body>
</html>
~~~

**3d幻灯片**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>3d幻灯片</title>
	<style id="css">
		body, ul, ol {margin: 0; padding: 0;}
		li {list-style: none;}
		.wrap {width: 800px; margin: 100px auto 0;}
		#picList {width: 800px; height: 360px; -webkit-perspective: 800px; -moz-perspective: 800px;}
		#picList li {width: 20px; height: 360px; position: relative; -webkit-transform-style: preserve-3d; -moz-transform-style: preserve-3d; -webkit-transform-origin: center center -180px; -moz-transform-origin: center center -180px; float: left;}
		#picList li a {width: 100%; height: 100%; position: absolute; left: 0; top: 0;}
		#picList li a:nth-of-type(1) {background: url(img/1.jpg) no-repeat;}
		#picList li a:nth-of-type(2) {background: url(img/2.jpg) no-repeat; top: -360px; -webkit-transform-origin: bottom; -webkit-transform: rotateX(90deg); -moz-transform-origin: bottom; -moz-transform: rotateX(90deg);}
		#picList li a:nth-of-type(3) {background: url(img/3.jpg) no-repeat; -webkit-transform: translateZ(-360px) rotateX(180deg); -moz-transform: translateZ(-360px) rotateX(180deg);}
		#picList li a:nth-of-type(4) {background: url(img/4.jpg) no-repeat; top: 360px; -webkit-transform-origin: top; -webkit-transform: rotateX(-90deg); -moz-transform-origin: top; -moz-transform: rotateX(-90deg);}
		#picList li span {position: absolute; width: 360px; height: 360px; background: #333;}
		#picList li span:nth-of-type(1) {-moz-transform-origin: left; -moz-transform: rotateY(90deg); -webkit-transform-origin: left; -webkit-transform: rotateY(90deg); left: 0;}
		#picList li span:nth-of-type(2) {-moz-transform-origin: right; -moz-transform: rotateY(-90deg); -webkit-transform-origin: right; -webkit-transform: rotateY(-90deg); right: 0;}
		#btns {float: right; padding: 10px 0;}
		#btns li {width: 40px; height: 40px; background: #000; color: #fff; border-radius: 50%; font: italic 30px/40px Arial; float: left; margin: 0 5px; text-align: center; cursor: pointer;}
		#btns .active {background: orange;}
		/* #picList li:nth-of-type(1) a {background-position: 0 0;}
		#picList li:nth-of-type(2) a {background-position: -50px 0;}	
		#picList li:nth-of-type(8) a {background-position: -350px 0;} */
	</style>
	<script>
		window.onload = function(){

			var oPicList = document.getElementById('picList');
			var oCss = document.getElementById('css');
			var aBtns = document.getElementById('btns').getElementsByTagName('li');
			var aLi = null;
			var sLi = "";
			var sCss = "";
			var iLiW = 20;
			var iZindex = 0;
			var iNow = 0;
			var iLength = oPicList.clientWidth / iLiW;
			for(var i=0; i<iLength; i++){
				i > iLength/2 ? iZindex-- : iZindex++;
				sLi += '<li><a href="#"></a><a href="#"></a><a href="#"></a><a href="#"></a><span></span><span></span></li>';
				sCss += '#picList li:nth-of-type(' + (i + 1) + ') a {background-position: -' + i*iLiW + 'px 0;}';
				sCss += '#picList li:nth-of-type(' + (i + 1) + ') {z-index:' + iZindex + '}';
			}
			oPicList.innerHTML = sLi;
			oCss.innerHTML += sCss;
			aLi = oPicList.children;

			for(var i=0; i<aBtns.length; i++){
				(function(a){
					aBtns[a].onclick = function(){
						for(var i=0; i<aLi.length; i++){
							aLi[i].style.transition = '0.5s ' + i*30 + 'ms';
							aLi[i].style.WebkitTransform = 'rotateX(-' + a*90 + 'deg)';
							aLi[i].style.MozTransform = 'rotateX(-' + a*90 + 'deg)';
						}
						this.className = 'active';
						aBtns[iNow].className = '';
						iNow = a;
					}
				})(i)
			}
		}
	</script>
</head>
<body>
	<div class="wrap">
		<ul id="picList">
			<!-- <li>
				<a href="#"></a>
				<a href="#"></a>
				<a href="#"></a>
				<a href="#"></a>
				<span></span>
				<span></span>
			</li> -->
		</ul>
		<ol id="btns">
			<li class="active">1</li>
			<li>2</li>
			<li>3</li>
			<li>4</li>
		</ol>
	</div>
</body>
</html>
~~~

##animation

- 关键帧 —— keyFrames
	- 类似于flash
		- 只需指明两个状态，之间的过程由计算机自动计算
	- 关键帧的时间单位
		- 数字 : 0%、25%、100%等 (不写0%或100%的状态，就默认为已经设置的样式)
		- 字符 : from(0%)、to(100%)
	- 格式(1)
		- @keyframes 动画名称 { 动画状态 }
	- 格式(2)
		- @keygrames miaov_text { from {background: red}; to {background: green}; }
	- 可以只有to

**animation基本使用**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>animation</title>
	<style>
		@-webkit-keyframes move {
			0% {
				width: 100px;
			}
			50% {
				width: 1000px;
			}
			100% {
				width: 500px;
			}
		}
		@-moz-keyframes move {
			0% {
				width: 100px;
			}
			50% {
				width: 1000px;
			}
			100% {
				width: 500px;
			}
		}
		@keyframes move {
			0% {
				width: 100px;
			}
			50% {
				width: 1000px;
			}
			100% {
				width: 500px;
			}
		}
		.box {width: 100px; height: 100px; background: red; -webkit-animation: 2s move; -moz-animation: 2s move; animation: 2s move;}
	</style>
</head>
<body>
	<div class="box"></div>
</body>
</html>
~~~

##animate——调用动画

- 调用的标签(#div1、xxx:hover之类的)
	- 必要属性
		- animation-name 动画名称（关键帧名称)
		- animation-duration 动画持续时间
	- 例如:
		- -webkit-animation-name: 'miaov';
		- -webkit-animation-duration: 4s;
	- 例子：进度条
	- animation-play-state 播放状态 (running 播放和 paused 暂停)
- 可选属性
	- animation-timing-function 动画运动形式
		- linear 匀速
		- ease 缓冲
		- ease-in 由慢到快
		- ease-out 由快到慢
		- ease-in-out 由慢到快再到慢
		- cubic-bezier(number, number, number, number) : 特定的贝塞尔曲线类型，4个数值需在[0, 1]区间内
	- animation-delay 动画延迟
		- 只是第一次
	- animation-iteration-count 重复次数
		- infinite为无限次
	- animation-direction 播放前重置
		- 动画是否重置后再开始播放
		- alternate 动画直接从上一次停止的位置开始执行
		- normal 动画第二次直接跳到0%的状态开始执行
- animate——和JS结合
	- 通过class
		- 在class里加入animation的各种属性
		- 直接给元素加-webkit-animation-xxx样式
	- animation的问题
		- 写起来麻烦
		- 没法动态改变目标点位置
	- obj.addEventListener('webkitAnimationEnd', function(){}, false);
- 实例1 : 无缝滚动

**animation的其他参数使用**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>animation</title>
	<style>
		@-webkit-keyframes move {
			50% {
				width: 1000px;
			}
		}
		.box {width: 100px; height: 100px; background: red; -webkit-animation: 1s 1s move ease-in infinite;}
	</style>
</head>
<body>
	<div class="box"></div>
</body>
</html>
~~~

**走回字，支持动画暂停**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>走回字形</title>
	<style>
		@-webkit-keyframes doMove{
			0% {
				top: 0; left: 0;
			}
			25% {
				top: 0; left: 300px;
			}
			50% {
				top: 300px; left: 300px;
			}
			75% {
				top: 300px; left: 0;
			}
			100% {
				top: 0; left: 0;
			}
		}
		#wrap {width: 400px; height: 400px; border: 5px solid #000; position: relative;}
		.box {width: 100px; height: 100px; background: red; position: absolute; left: 0; top: 0; -webkit-animation: 4s doMove linear infinite;}
		#wrap:hover .box {-webkit-animation-play-state: paused;}
	</style>
</head>
<body>
	<div id="wrap">
		<div class="box"></div>
	</div>
</body>
</html>
~~~

**正序倒序播放**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>正序、倒序播放</title>
	<style>
		@-webkit-keyframes doMove{
			0% {
				top: 0; left: 0;
			}
			25% {
				top: 0; left: 300px;
			}
			50% {
				top: 300px; left: 300px;
			}
			75% {
				top: 300px; left: 0;
			}
			100% {
				top: 0; left: 0;
			}
		}
		#wrap {width: 400px; height: 400px; border: 5px solid #000; position: relative;}
		.box {width: 100px; height: 100px; background: red; position: absolute; left: 0; top: 0; -webkit-animation: 4s doMove linear infinite alternate;}
	</style>
</head>
<body>
	<div id="wrap">
		<div class="box"></div>
	</div>
</body>
</html>
~~~

**处理动画完毕之后回到默认样式的简单做法**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>animation</title>
	<style>
		@-webkit-keyframes move {
			0% {
				width: 100px;
			}
			100% {
				width: 500px;
			}
		}
		.box {width: 100px; height: 100px; background: red;}
		.move {-webkit-animation: 2s move; width: 500px;}
	</style>
</head>
<body>
	<div class="box move"></div>
</body>
</html>
~~~

**动画结束保持原状，与js结合的做法**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>animation</title>
	<style>
		@-webkit-keyframes move {
			0% {
				width: 100px;
			}
			100% {
				width: 500px;
			}
		}
		.box {width: 100px; height: 100px; background: red;}
		.move {-webkit-animation: 2s move; width: 500px;}
	</style>
</head>
<body>
	<div class="box" id="box"></div>
	<script>
		document.getElementById('box').onclick = function(){
			this.className = 'box move';
		}
	</script>
</body>
</html>
~~~

**animationend事件**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>animation</title>
	<style>
		@-webkit-keyframes move {
			0% {
				width: 100px;
			}
			100% {
				width: 500px;
			}
		}
		@-moz-keyframes move {
			0% {
				width: 100px;
			}
			100% {
				width: 500px;
			}
		}
		@keyframes move {
			0% {
				width: 100px;
			}
			100% {
				width: 500px;
			}
		}
		.box {width: 100px; height: 100px; background: red;}
		.move {-webkit-animation: 2s move; -moz-animation: 2s move; animation: 2s move; width: 500px;}
	</style>
</head>
<body>
	<div class="box" id="box"></div>
	<script>
		document.getElementById('box').onclick = function(){
			this.className = 'box move';
			addEnd(this, fn);
		}

		function fn(){
			alert('end');
		}

		function addEnd(obj, fn){
			obj.addEventListener('webkitAnimationEnd', fn, false);
			obj.addEventListener('animationend', fn, false);
		}
	</script>
</body>
</html>
~~~

**无缝滚动**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>无缝滚动</title>
	<style>
		@-webkit-keyframes move {
			0% {
				left: 0;
			}
			100% {
				left: -500px;
			}
		}
		#wrap {width: 500px; height: 100px; border: 1px solid #000; position: relative; margin: 100px auto; overflow: hidden;}
		#list {position: absolute; left: 0; top: 0; margin: 0; padding: 0; -webkit-animation: 3s infinite move linear; width: 200%;}
		#list li {list-style: none; width: 98px; height: 98px; border: 1px solid #fff; background: #000; color: #fff; font: 50px/98px Arial; text-align: center; float: left;}
		#wrap:hover #list {-webkit-animation-play-state: paused;}
	</style>
</head>
<body>
	<div id="wrap">
		<ul id="list">
			<li>1</li>
			<li>2</li>
			<li>3</li>
			<li>4</li>
			<li>5</li>
			<li>1</li>
			<li>2</li>
			<li>3</li>
			<li>4</li>
			<li>5</li>
		</ul>
	</div>
</body>
</html>
~~~

**3d图片轮换**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>3d图片轮换</title>
	<style>
		@-webkit-keyframes show {
			0% {
				-webkit-transform: rotateX(180deg);
				opacity: 0;
			}
			50%{
				-webkit-transform: rotateX(-20deg);
				opacity: 1;
			}
			60%{
				-webkit-transform: rotateX(18deg);
				opacity: 1;
			}
			70%{
				-webkit-transform: rotateX(-12deg);
				opacity: 1;
			}
			80%{
				-webkit-transform: rotateX(8deg);
				opacity: 1;
			}
			90%{
				-webkit-transform: rotateX(-6deg);
				opacity: 1;
			}
			100%{
				-webkit-transform: rotateX(0deg);
				opacity: 1;
			}
		}
		@-webkit-keyframes hide {
			0% {
				-webkit-transform: rotateX(0deg);
				opacity: 1;
			}
			100%{
				-webkit-transform: rotateX(-180deg);
				opacity: 0;
			}
		}
		#wrap {width: 400px; height: 300px; position: relative; margin: 40px auto; -webkit-perspective: 800px; -webkit-transform-style: preserve-3d;}
		img {width: 400px; height: 300px; position: absolute; left: 0; top: 0; -webkit-transform-origin: bottom; -webkit-transform: rotateX(-180deg); opacity: 0;}
		#wrap input {width: 60px; height: 60px; margin: 0; padding: 0; background: #ccc; top: 100px; position: absolute; border-radius: 50%; outline: none; cursor: pointer;}
		#wrap input:nth-of-type(1) {left: -100px;}
		#wrap input:nth-of-type(2) {right: -100px;}
		.show {-webkit-transform: rotateX(0deg); opacity: 1; -webkit-animation: 1s show;}
		.hide {-webkit-transform: rotateX(180deg); opacity: 0; -webkit-animation: 0.6s hide;}
	</style>
	<script>
		window.onload = function(){
			var oWrap = document.getElementById('wrap');
			var aBtn = oWrap.getElementsByTagName('input');
			var aImg = oWrap.getElementsByTagName('img');
			var iNow = 0;

			aBtn[0].onclick = function(){
				aImg[iNow].className = 'hide';
				iNow--;
				if(iNow < 0){
					iNow = aImg.length - 1;
				}
				aImg[iNow].className = 'show';
			}

			aBtn[1].onclick = function(){
				aImg[iNow].className = 'hide';
				iNow++;
				if(iNow >= aImg.length){
					iNow = 0;
				}
				aImg[iNow].className = 'show';
			}

		}
	</script>
</head>
<body>
	<div id="wrap">
		<input type="button" value="上一张" />
		<img src="images/img1.jpg" class="show" />
		<img src="images/img2.jpg" />
		<img src="images/img3.jpg" />
		<img src="images/img4.jpg" />
		<img src="images/img5.jpg" />
		<input type="button" value="下一张" />
	</div>
</body>
</html>
~~~

**3d折纸效果**

**第一种布局方法，位置难以确定，很难实现

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>3d折纸效果</title>
	<style>
		#wrap {width: 500px; margin: 0 auto; -webkit-perspective: 800px; -webkit-transform-style: preserve-3d;}
		#wrap div {height: 100px; border: 1px solid #000; background: #ccc;}
		#wrap div:nth-of-type(1) {-webkit-transform-origin: bottom; -webkit-transform: rotateX(45deg);}
		#wrap div:nth-of-type(2) {-webkit-transform-origin: top; -webkit-transform: rotateX(-45deg);}
		#wrap div:nth-of-type(3) {-webkit-transform-origin: top; -webkit-transform: rotateX(45deg);}
	</style>
	<script>
		window.onload = function(){
			
		}
	</script>
</head>
<body>
	<div id="wrap">
		<div>1</div>
		<div>2</div>
		<div>3</div>
	</div>
</body>
</html>
~~~

**3d折纸布局原理**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>3d折纸效果</title>
	<style>
		#wrap {width: 500px; margin: 0 auto; -webkit-perspective: 800px; -webkit-transform-style: preserve-3d; position: relative;}
		#wrap div {position: absolute; left: 0; top: 102px; width: 500px; -webkit-transform-origin: top; -webkit-transform-style: preserve-3d;}
		#wrap span {height: 100px; border: 1px solid #000; background: #ccc; display: block;}
		#wrap>div {top: 0;}
	</style>
	<script>
		window.onload = function(){
			
		}
	</script>
</head>
<body>
	<div id="wrap">
		<div style="-webkit-transform: rotateX(-45deg)">
			<span>1</span>
			<div style="-webkit-transform: rotateX(90deg)">
				<span>2</span>
				<div style="-webkit-transform: rotateX(-90deg)">
					<span>3</span>
					<div style="-webkit-transform: rotateX(90deg)">
						<span>4</span>
					</div>
				</div>
			</div>
		</div>
	</div>
</body>
</html>
~~~

**3d折纸最终效果**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>3d折纸效果</title>
	<style>
		@-webkit-keyframes open {
			0% {
				-webkit-transform: rotateX(-120deg);
			}
			25% {
				-webkit-transform: rotateX(30deg);
			}
			50% {
				-webkit-transform: rotateX(-15deg);
			}
			75% {
				-webkit-transform: rotateX(8deg);
			}
			100% {
				-webkit-transform: rotateX(0deg);
			}
		}
		@-webkit-keyframes close {
			0% {
				-webkit-transform: rotateX(0deg);
			}
			100% {
				-webkit-transform: rotateX(-120deg);
			}
		}
		body {margin: 0;}
		#wrap {width: 160px; margin: 30px auto;position: relative; -webkit-perspective: 800px;}
		#wrap h2 {height: 40px; background: #f60; color: #fff; font: bold 16px/40px "微软雅黑"; text-align: center; margin: 0; position: relative; z-index: 10;}
		#wrap div {position: absolute; top: 32px; width: 100%; left: 0; -webkit-transform-type: preserve-3d; -webkit-transform-origin: top; -webkit-transform: rotateX(-120deg);}
		#wrap span {display: block; height: 30px; background: #9f0; font: 12px/30px "宋体"; color: #fff; text-indent: 20px; box-shadow: inset 0 0 0 20px rgba(0,0,0,1); transition: 1s;}
		#wrap>div {top: 40px;}
		#wrap .show {-webkit-animation: 2s open; -webkit-transform: rotateX(0deg);}
		#wrap .close {-webkit-animation: 0.8s close; -webkit-transform: rotateX(-120deg);}
		#wrap .show>span {box-shadow: inset 0 0 0 20px rgba(0,0,0,0);;}
		#btn {position: absolute;}
	</style>
	<script>
		window.onload = function(){
			
		}
	</script>
</head>
<body>
	<input type="button" value="按钮" id="btn" />
	<div id="wrap">
		<h2>我是标题噢</h2>
		<div>
			<span>选项1</span>
			<div>
				<span>选项2</span>
				<div>
					<span>选项3</span>
					<div>
						<span>选项4</span>
						<div>
							<span>选项5</span>
							<div>
								<span>选项6</span>
								<div>
									<span>选项7</span>
								</div>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
	<script>
		var oBtn = document.getElementById('btn');
		var oWrap = document.getElementById('wrap');
		var aDiv = oWrap.getElementsByTagName('div');
		var iDelay = 200;
		var oTimer = null;
		var i = 0;
		var bOff = true;
		oBtn.onclick = function(){
			if(oTimer){
				return;
			} 
			if(bOff){
				i = 0;
				oTimer = setInterval(function(){
					aDiv[i].className = 'show';
					i++;
					if(i == aDiv.length){
						clearInterval(oTimer);
						oTimer = null;
						bOff = false;
					}
				}, iDelay)
			} else {
				i = aDiv.length - 1;
				oTimer = setInterval(function(){
					aDiv[i].className = 'close';
					i--;
					if(i < 0){
						clearInterval(oTimer);
						oTimer = null;
						bOff = true;
					}
				}, iDelay)
			}
		}
	</script>
</body>
</html>
~~~

