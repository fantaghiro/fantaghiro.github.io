---
layout: post
title: 亚马逊Kindle电子书培训（三）
category: publishing
tags:
- Kindle
- 亚马逊
- 电子书
- 培训
---
第三天的培训，美其名曰高阶内容，但是个人感觉难度不是很大。因为前期自学了一些HTML和CSS方面的知识，第三天的培训其实就是对这些知识最基本部分的复习和基础应用的实践。所谓epub或者时mobi的电子书，无非是用特殊形式封装好的html（或者xml）文件而已。对这个有了基本认识，对电子书的神秘感也就荡然无存了。
<!--more-->

高阶培训中做了两件比较重要的工作，一是老师带领大家一起看了以下Kindle电子书支持的HTML标签都有哪些，并且向前来培训的编辑们普及了这些标签的基本意义和使用方法。二是带领大家浏览了一边Amazon Kindle Publishing Guidelines这份文件。文件内容十分全面细致，英文版对于我来说没有什么障碍，但是感觉还是值得在这里简要记一下，以备日后查阅。

目前Kindle支持的电子书格式为Kindle Format 8 （KF8）。该格式替换了之前的mobi 7，添加了部分HTML5和CSS3的支持。目前KF8支持以下功能：

* 文本布局（包括行距、对齐、外边距、颜色、定义样式和边框）
* 支持段落首字下沉
* 支持包含块状文字、气泡提示、侧边栏和图片等的浮动元素，浮动元素中的文字时可以换行的
* 支持带有项目符号的有序和无序列表
* 支持技术或教材书籍所必须的嵌套表格和单元格合并
* 支持页面或文字后面有背景图片
* 支持SVG，并可以实现无损放大缩小
* 支持嵌入字体，允许出版商对书籍进行个性化处理
* 支持圆角文本框
* 支持阴影效果
* 支持带轮廓的文本
* 支持多个或重复的背景图片
* 支持颜色渐变
* 可以使用CSS选择器对文本或其他元素的属性进行精确控制
* 对特定屏幕大小支持固定布局

## 文本设置指南
<hr>
**Rule 1. Body的文本设置必须使用默认**

流式排版的Kindle电子书中body的文本必须都是默认的设置。亚马逊鼓励内容创造者可以对标题，特殊段落、脚注、图表等用富有创新性的样式，但绝对不是body的文本。因为对body文本的样式设置都会覆盖掉用户自选的阅读的设置，这样，用户就会报告说阅读体验差。下面是几个最为重要的点需要提请注意：
* body的文本不能有强制对齐（比如左对齐或两段对齐）
* body的文本必须用默认的字号和行距。不能用类似<code>&lt;font size=“...”></code>这样的样式标签或者在CSS中更改字号和行距。
* body的文本不能全部设置为粗体或者斜体，只能对其中的个别文字进行粗体或斜体设置。
* body的文本不能通篇用一个强制的颜色。如果你想在某个章节强制使用某种颜色，请不要用太浅或太深的颜色。非常浅的颜色在白色背景的设备或电子墨水设备上，会因为对比度不足而看不清楚。而非常深的颜色在设置为黑色背景的设备上又看不清楚。如果用灰色的话，请用hex值在#666到#999之间的颜色。
* body的文本不能用白色或黑色字体颜色。有用户报告说体验不好时因为他们把设备的背景色设置为了白色或黑色，然后相应颜色的文字就完全看不出来了。
* 用户反馈说他们拥有选择设备中提供的默认字体的选择权，这一点的体验非常好。

**Rule 2. 在分页的地方用CSS设置**

不要在需要分页的地方通过添加空白行来实现，而应该使用CSS中的page-break-before和page-break-after属性来设置。

**Rule 3. 设置段落**

KindleGen会自动为每段首行缩进。如果要改变这一设置，请为<code>&lt;p></code>使用缩进样式。比如：
* <code>&lt;p style=“text-indent: 0”></code> -- 首行无缩进
* <code>&lt;p style=“text-indent: 10%”></code> --首行缩进10%
* <code>&lt;p style=“text-indent: 5em”></code> --首行缩进5个字符宽度

要给每段之前添加一些间隙，在<code>&lt;p></code>标签上使用margin-top样式。

**Rule 4. 其他支持的编码**

只要满足以下两个条件，Kindle电子书就支持该编码：
* HTML文件中明确声明了编码
* 用于将源文件转码的电脑支持该编码并且知道如何将其转为UNICODE编码

亚马逊推荐在HTML文件中的<code>&lt;head></code>部分中用<code>&lt;meta></code>标签。例如：

<pre>
&lt;html&gt;
&lt;head&gt;
...
&lt;meta http-equiv=“content-type” content=“text/html; charset=iso-8859-1&gt;
...
</pre>

**Rule 5. 空格以及UNICODE字符**

仅支持正常空格字符、不可分空格字符（\&nbsp;）以及零宽不连字（\&zwnj;）。用其他空格会干扰选择区域、字典查词还有换行的算法。

不要使用UNICODE格式字符，它们也会造成问题。

**Rule 6. 支持等宽字符**

如果使用以下标签或者属性，Kindle可以显示为等宽字符：<code>&lt;pre></code>, <code>&lt;code></code>, <code>&lt;samp></code>, <code>&lt;kbd></code>, <code>&lt;tt></code>, <code>&lt;font face=“courier”></code>, <code>&lt;font face=“monospace”></code>。

除了<code>&lt;pre></code>标签以外，上面列出的标签都不会改变文本的对齐方式。如果要使文本左对齐的话，那么将这些标签包在一个<code>&lt;div></code>标签里面，然后对这个<code>&lt;div></code>设置text-align: left的CSS样式。

出版商可以用自己的字体。亚马逊有质量检查环节，可以确保这些字体能够在电子墨水设备上显示正常，而且不影响阅读体验。但是不要用Charis字体，在Kindle阅读器中已经用更高质量的字体替换它。

**Rule 7. 支持的CSS**

在早期的Kindle平台中，仅支持最为基本的CSS样式，但是在KF8里面，对于CSS2和CSS3的样式支持已经大大提升。为了确保设置的CSS起作用，请在发布之前务必要在不同的设备上预览一下。

对于例如字号、宽度、高度、外边距、内边距、缩进的CSS设置，应尽量避免固定值。为了能在不同大小和分辨率的屏幕上都有良好的展示效果，请在给这些属性设置的时候用百分比。

当设置外边距和内边距的时候，请用百分比而不是em。这样外边距句不会随着字号变大而变宽。外边距的值必须等于或大于0，才能确保文本不超出屏幕或者不发生重叠。对于普通的body的文本，请总是将左右外边距设置为0，这样用户在使用设备默认选项的时候，就可以选择不同的外边距了。

为了分页的需要，Kindle阅读器不推荐将行高设置在1.2em或120%以下。

对于例如首字母下沉的元素，请用百分比或相对单位设置（不论是正值还是负值），不要使用固定值。（例如：对于下沉字母，用font-size: 300%)。下沉字母的最上方应该与body的文本对齐。为了实现下沉字母效果，亚马逊推荐使用以下CSS代码：

例：

<pre>
p.para {
    font-family: “Times New Roman”;
    font-size: 4em;
    margin-bottom: 0;
    margin-top: 0;
    text-align: justify;
    text-indent: 0;
}
@media amzn-kf8
{
    span.dropcaps
    {
        font-weight: normal;
        font-size: 320%;
        float: left;
        margin-top: -0.3225em;
        margin-bottom: -0.3245em;
    }
}
@media amzn-mobi
{
    span.dropcaps
    {
        font-size: 3em;
        font-weight: bold;
    }
}
</pre>
<pre>
&lt;p class=“para”>&lt;span class=“dropcaps”>T&lt;/span>here is a sample
</pre>

**Rule 9. 自定义字体选择**

一本书最基本最主要的字体应该时设置在&lt;body&gt;上。如果你想添加一些额外的字体设置，比如粗体或者斜体，那么要保证这些样式是设置在文本上的而不是字体上的，这样不论用户选择哪一种字体，这些带有样式的元素都能正确显示。以下是两组正确以及错误的自定义字体的方式。

* 错误的HTML代码

<pre>
&lt;html>
&lt;body>
&lt;p style=“font-family: PrimaryFont”>
Primary font content&lt;/p>
&lt;p style=“font-family: SecondaryFont”>
Secondary font content&lt;/p>
&lt;p style=“font-family: PrimaryFont”>
Primary font content&lt;/p>
&lt;p style=“font-family: PrimaryFont”>
Primary ofnt content&lt;/p>
&lt;/body>
&lt;/html>
</pre>

* 正确的HTML代码

<pre>
&lt;html>
&lt;body style=“font-family: PrimaryFont”>
&lt;p>Primary font content&lt;/p>
&lt;p style=“font-family: SecondaryFont”>
Secondary font content&lt;/p>
&lt;p>Primary font content&lt;/p>
&lt;p>Primary font content&lt;/p>
&lt;/body>
&lt;/html>
</pre>

同样的结果也可以用CSS样式表实现。下面是一组正确以及错误的CSS代码。
* 错误的CSS代码

<pre>
body {
font-size: asize;
}
.indent {
font-size: asize;
font-family: PrimaryFont;
}
.sidebar-text {
font-family: SecondaryFont;
weight: bold;
}
</pre>

* 正确的CSS代码

<pre>
body {
font-family: PrimaryFont;
font-size: asize;
}
.indent {
font-size: asize;
}
.sidebar-text {
font-family: SecondaryFont;
weight: bold;
}
</pre>

## 封面图片设置指南
<hr>

**Rule 1. 营销封面必须得有**

营销封面最好是2560×1600px、350dpi。这样的图片在高清的Kindle设备上可以确保显示清晰。图片大小不得超过5MB。

营销封面如果没有达到2560×1600，那么在上传的时候，会有一个提示。如果图片最小边小于500px，那么在网站上根本就不显示了。

如果封面图片小于推荐的大小，那么亚马逊强烈推荐您重新制作一幅符合推荐大小的图片。不要拉伸图片来达标，因为这样图片显示出来效果可能会很差。

封面图片上的内容：
* 不能侵犯其他出版社或艺术家的版权
* 不要提到价格或者其他临时性的促销活动

**Rule 2. 内容封面也必须得有**

请提供一幅高分辨率的大图片作为内容封面，因为如果封面太小的话，亚马逊的质检环节不会让这本书通过。

通过OPF文件来设置封面，可以通过以下这两种方法：

方法一：

<pre>
&lt;manifest>
...
&lt;item id=“cimage” media-type=“image/jpeg” href=“other_cover.jpg” properties=“cover-image”/>
...
&lt;/manifest>
</pre>

以上这种写法符合IDPF 3.0标准，详情请参见[http://idpf.org/epub/30/spec/epub30- publications-20111011.html#sec-item-property-values](http://idpf.org/epub/30/spec/epub30- publications-20111011.html#sec-item-property-values)。

方法二：

<pre>
&lt;metadata>
...
&lt;meta name=“cover” content=“my-cover-image” />
...
&lt;/metadata>
...
&lt;manifest>
...
&lt;item href=“MyCoverImagejpg” id=“my-cover-image” media-type=“image/jpeg” />
...
&lt;/manifest>
</pre>

在metadata里面使用name=“cover”是必须的。

**Rule. 3 内容封面不能出现两次**

除了上面提到的方法之外，不要再在内容中添加封面，如果添加了，那么可能在图书中会出现两次封面。

但是对于流式排版的书籍来说有一种特殊情况：如果你希望封面是HTML格式的，从而能够兼容其他供应商的软件，那么除了按照上面方式设置好封面以外，还要在OPF文件中，添加如下标签：

<pre>
&lt;spine> &lt;itemref idref="my-html-cover" linear="no" /> &lt;/spine>
  ...
&lt;manifest> &lt;item id="my-html-cover" href="cover.html" media-
type="application/xhtml+xml" /> &lt;/manifest>
...
</pre>

其中，linear=“no”是必须的。

同时，在landmarks nav元素中，添加如下标签：

<pre>
&lt;nav epub:type="landmarks">
&lt;ol> &lt;li>&lt;a epub:type="cover" href="cover.html "> Cover Image &lt;/a> &lt;/li>&lt;/ol> &lt;/nav>
</pre>

其中，epub: type=“cover”是必须的。

设置封面，还可以在OPF文件中使用下面一种写法，而非使用landmarks nav元素：

<pre>
&lt;guide> &lt;reference type="cover" title="Cover Image" href="cover.html" /> &lt;/guide>
</pre>

其中，type=“cover”是必须的。

## 图表内容设置指南
<hr>

亚马逊强烈建议您为所有书籍设置HTML TOC。HTML目录适用与大多数书籍，固定布局的童书、绘本或漫画除外。

**Rule 1. 推荐使用逻辑目录**

亚马逊强烈建议所有的图书包含逻辑目录和HTML目录。这对于提高阅读体验十分重要，因为读者可以通过这个目录在不同章节间比较容易的跳转。用户在一开始就期待能够看到一个HTML目录，而逻辑目录也给用户提供了在书中跳转的一种新途径。如果书长于20页，那么添加逻辑目录就变得尤为重要了。

逻辑目录时通过toc nav元素或者用于XML应用的导航控制文件（NCX）生成的。**注意：**固定布局的书不支持嵌套的锚点标签。

* 用toc nav元素创建逻辑目录

toc nav元素符合IDPF 3.0标准，详情可见：[http://idpf.org/epub/30/spec/epub30-contentdocs-20111011.html#sec-xhtml-nav-def-model](http://idpf.org/epub/30/spec/epub30-contentdocs-20111011.html#sec-xhtml-nav-def-model)和[http://idpf.org/epub/30/spec/epub30-contentdocs-20111011.html#sec-xhtml-nav-def-types-toc](http://idpf.org/epub/30/spec/epub30-contentdocs-20111011.html#sec-xhtml-nav-def-types-toc)。

创建toc nav元素能够同时创建逻辑目录和HTML目录。

例：

<pre>
&lt;nav epub: type=“toc”>
&lt;ol>
&lt;li>&lt;a href=”Sway_body.html#preface_1">AUTHOR'S NOTE&lt;/a>&lt;/li>
&lt;li>&lt;a href=”Sway_body.html#part_1">PART ONE&lt;/a>
   &lt;ol>
   &lt;li>&lt;a href="Sway_body.html#chapter_1">THE HOUSES, 1969&lt;/a>&lt;/li>
   &lt;li>&lt;a href="Sway_body.html#chapter_2">ROCK AND ROLL, 1962&lt;/a>&lt;/li>
   &lt;li>&lt;a href="Sway_body.html#chapter_3">THE EMPRESS, 1928–1947&lt;/a>&lt;/li>
   &lt;/ol>
&lt;/li>
&lt;/ol>
&lt;/nav>
</pre>

下面这段取自OPF文件的代码告诉你如何在&lt;manifest&gt;标签中声明toc nav元素。

例：

<pre>
&lt;manifest>
&lt;item id="toc" properties="nav" href="xhtml/toc.xhtml" media-
type="application/xhtml+xml"/>
</pre>
可以选择将其用于&lt;spine&gt;标签，这样就可以被用来当作HTML目录。
<pre>
&lt;spine>
&lt;itemref idref=“toc” />
</pre>

* 用NCX创建逻辑目录

NCX时IDPF2.0的一部分，请参见[http://www.niso.org/workrooms/daisy/Z39- 86-2005.html#NCX](http://www.niso.org/workrooms/daisy/Z39- 86-2005.html#NCX)。

例：

<pre>
&lt;navMap>
&lt;navPoint class="titlepage" id="L1T" playOrder="1">
&lt;navLabel>&lt;text>AUTHOR'S NOTE&lt;/text>&lt;/navLabel>
&lt;content src=”Sway_body.html#preface_1" />
&lt;/navPoint>
&lt;navPoint class="book" id="level1-book1" playOrder="2">
&lt;navLabel>&lt;text>PART ONE&lt;/text>&lt;/navLabel>
&lt;content src=”Sway_body.html#part_1" />
&lt;navPoint class="chapter" id="level2-book1chap01" playOrder="3">
&lt;navLabel>&lt;text>THE HOUSES, 1969&lt;/text>&lt;/navLabel>
&lt;content src="Sway_body.html#chapter_1" />
&lt;/navPoint>
&lt;navPoint class="chapter" id="level2-book1chap02" playOrder="4">
&lt;navLabel>&lt;text>ROCK AND ROLL, 1962&lt;/text>&lt;/navLabel>
&lt;content src="Sway_body.html#chapter_2" />
&lt;/navPoint>
&lt;navPoint class="chapter" id="level2-book1chap03" playOrder="5">
&lt;navLabel>&lt;text>THE EMPRESS, 1928–1947&lt;/text>&lt;/navLabel>
&lt;content src="Sway_body.html#chapter_3" />
&lt;/navPoint>
&lt;/navPoint>
&lt;/navMap>
</pre>

下面这段取自OPF文件的代码说明了如何将NCX目录添加到一本书中。在&lt;manifest&gt;标签中声明NCX：

<pre>
&lt;manifest>
&lt;item id=“toc” media-type=“appication/x-dtbncx+xml” href=“toc.ncx” />
</pre>
将其用在&lt;spine&gt;中：
<pre>
&lt;spine toc=“toc”>
</pre>

