---
layout: post
title: 亚马逊Kindle电子书培训（三）
category: publishing
description: 亚马逊对于Vendor培训的第三天，附上自己译的电子书转码“通用格式指南”的一部分。
tags:
- kindle
- 电子书
- 亚马逊
- 培训
---

最后一天的培训，美其名曰高阶。其实对于学过HTML和CSS的人来说，意义不大。不论是Mobi还是Epub，底层源文件都是HTML或XML文件。电子书格式远比网页要简单的多、受限的多。不是所有的HTML标签和CSS样式都会在电子书中起效，而且电子书也根本不支持js脚本。最后一天的培训做了两件事情：一、一一列举了Kindle电子书支持的HTML标签和CSS样式；二、浏览了一遍Kindle电子书的Publishing Guideline。文档是英文的，对于我来说压力不大。在此，我就将该文档中的第三大部分，通用格式制作指南翻译在此，以便以后查阅。

**通用格式指南**

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

## 1 文本设置指南
<hr>
**1.1 BODY的文本设置必须使用默认**

流式排版的Kindle电子书中body的文本必须都是默认的设置。亚马逊鼓励内容创造者可以对标题，特殊段落、脚注、图表等用富有创新性的样式，但绝对不是body的文本。因为对body文本的样式设置都会覆盖掉用户自选的阅读的设置，这样，用户就会报告说阅读体验差。下面是几个最为重要的点需要提请注意：

* body的文本不能有强制对齐（比如左对齐或两段对齐）
* body的文本必须用默认的字号和行距。不能用类似&lt;font size="...">这样的样式标签或者在CSS中更改字号和行距。
* body的文本不能全部设置为粗体或者斜体，只能对其中的个别文字进行粗体或斜体设置。
* body的文本不能通篇用一个强制的颜色。如果你想在某个章节强制使用某种颜色，请不要用太浅或太深的颜色。非常浅的颜色在白色背景的设备或电子墨水设备上，会因为对比度不足而看不清楚。而非常深的颜色在设置为黑色背景的设备上又看不清楚。如果用灰色的话，请用hex值在#666到#999之间的颜色。
* body的文本不能用白色或黑色字体颜色。有用户报告说体验不好时因为他们把设备的背景色设置为了白色或黑色，然后相应颜色的文字就完全看不出来了。
* 用户反馈说他们拥有选择设备中提供的默认字体的选择权，这一点的体验非常好。

**1.2 在分页的地方用CSS设置**

不要在需要分页的地方通过添加空白行来实现，而应该使用CSS中的page-break-before和page-break-after属性来设置。

**1.3 设置段落**

KindleGen会自动为每段首行缩进。如果要改变这一设置，请为&lt;p>使用缩进样式。比如：

{% highlight html %}
<p style="text-indent: 0"> <!-- 首行无缩进 -->
<p style="text-indent: 10%"> <!-- 首行缩进10% -->
<p style="text-indent: 5em"> <!-- 首行缩进5个字符宽度 -->
{% endhighlight %}

要给每段之前添加一些间隙，在&lt;p>标签上使用margin-top样式。

**1.4 其他支持的编码**

只要满足以下两个条件，Kindle电子书就支持该编码：
* HTML文件中明确声明了编码
* 用于将源文件转码的电脑支持该编码并且知道如何将其转为UNICODE编码

亚马逊推荐在HTML文件中的&lt;head>部分中用&lt;meta>标签。例如：

{% highlight html %}
<html>
<head>
<!--...-->
<meta http-equiv="content-type" content="text/html; charset=iso-8859-1">
<!--...-->
{% endhighlight %}

**1.5 空格以及UNICODE字符**

仅支持正常空格字符、不可分空格字符(\&nbsp;)以及零宽不连字（\&zwnj;）。用其他空格会干扰选择区域、字典查词还有换行的算法。
不要使用UNICODE格式字符，它们也会造成问题。

**1.6 支持等宽字符**

如果使用以下标签或者属性，Kindle可以显示为等宽字符：&lt;pre>、&lt;samp>、&lt;kbd>、&lt;tt>、&lt;font face="courier">、&lt;font face="monospace">。

除了&lt;pre>标签以外，上面列出的标签都不会改变文本的对齐方式。如果要使文本左对齐的话，那么将这些标签包在一个&lt;div>标签里面，然后对这个&lt;div>设置text-align: left的CSS样式。

出版商可以用自己的字体。亚马逊有质量检查环节，可以确保这些字体能够在电子墨水设备上显示正常，而且不影响阅读体验。但是不要用Charis字体，在Kindle阅读器中已经用更高质量的字体替换它。

**1.7 支持的CSS**

在早期的Kindle平台中，仅支持最为基本的CSS样式，但是在KF8里面，对于CSS2和CSS3的样式支持已经大大提升。为了确保设置的CSS起作用，请在发布之前务必要在不同的设备上预览一下。

对于例如字号、宽度、高度、外边距、内边距、缩进的CSS设置，应尽量避免固定值。为了能在不同大小和分辨率的屏幕上都有良好的展示效果，请在给这些属性设置的时候用百分比。

当设置外边距和内边距的时候，请用百分比而不是em。这样外边距句不会随着字号变大而变宽。外边距的值必须等于或大于0，才能确保文本不超出屏幕或者不发生重叠。对于普通的body的文本，请总是将左右外边距设置为0，这样用户在使用设备默认选项的时候，就可以选择不同的外边距了。

为了分页的需要，Kindle阅读器不推荐将行高设置在1.2em或120%以下。

对于例如首字母下沉的元素，请用百分比或相对单位设置（不论是正值还是负值），不要使用固定值。（例如：对于下沉字母，用font-size: 300%)。下沉字母的最上方应该与body的文本对齐。为了实现下沉字母效果，亚马逊推荐使用以下CSS代码：

{% highlight css %}
p.para {
    font-family: "Times New Roman";
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
{% endhighlight %}

{% highlight html %}
<p class="para"><span class="dropcaps">T</span>here is a sample
{% endhighlight %}

**1.8 页码**

Kindle电子书并不与实体书的页码总是对应。因此，在书中不要添加任何有关页码的信息。页码也不应该出现在交叉引用或者索引中。亚马逊可以生成作为图书额外元数据的页码。亚马逊生成的页码是基于其自己内部技术。

**1.9 自定义字体选择**

一本书最基本最主要的字体应该时设置在&lt;body>上。如果你想添加一些额外的字体设置，比如粗体或者斜体，那么要保证这些样式是设置在文本上的而不是字体上的，这样不论用户选择哪一种字体，这些带有样式的元素都能正确显示。以下是两组正确以及错误的自定义字体的方式。

错误的HTML代码

{% highlight html %}
<html>
<body>
<p style="font-family: PrimaryFont">
Primary font content</p>
<p style="font-family: SecondaryFont">
Secondary font content</p>
<p style="font-family: PrimaryFont">
Primary font content</p>
<p style="font-family: PrimaryFont">
Primary ofnt content</p>
</body>
</html>
{% endhighlight %}

正确的HTML代码

{% highlight html %}
<html>
<body style="font-family: PrimaryFont">
<p>Primary font content</p>
<p style="font-family: SecondaryFont">
Secondary font content</p>
<p>Primary font content</p>
<p>Primary font content</p>
</body>
</html>
{% endhighlight %}

同样的结果也可以用CSS样式表实现。下面是一组正确以及错误的CSS代码。

错误的CSS代码

{% highlight css %}
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
{% endhighlight %}

正确的CSS代码

{% highlight css %}
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
{% endhighlight %}

##2 封面图片设置指南
<hr>

**2.1 营销封面必须得有**

营销封面最好是2560×1600px、350dpi。这样的图片在高清的Kindle设备上可以确保显示清晰。图片大小不得超过5MB。

营销封面如果没有达到2560×1600，那么在上传的时候，会有一个提示。如果图片最小边小于500px，那么在网站上根本就不显示了。

如果封面图片小于推荐的大小，那么亚马逊强烈推荐您重新制作一幅符合推荐大小的图片。不要拉伸图片来达标，因为这样图片显示出来效果可能会很差。

封面图片上的内容：
* 不能侵犯其他出版社或艺术家的版权
* 不要提到价格或者其他临时性的促销活动
 
**2.2 内容封面也必须得有**

请提供一幅高分辨率的大图片作为内容封面，因为如果封面太小的话，亚马逊的质检环节不会让这本书通过。

通过OPF文件来设置封面，可以通过以下这两种方法：

方法一：

{% highlight xml %}
<manifest>
<!--...-->
<item id="cimage" media-type="image/jpeg" href="other_cover.jpg" properties="cover-image"/>
<!--...-->
</manifest>
{% endhighlight %}

以上这种写法符合IDPF 3.0标准，详情请参见[http://idpf.org/epub/30/spec/epub30-publications-20111011.html#sec-item-property-values](http://idpf.org/epub/30/spec/epub30-publications-20111011.html#sec-item-property-values)。

方法二：（下划线内容为必须、下同）

{% highlight xml %}
<metadata>
<!--...-->
<meta name="cover" content="my-cover-image" />
<!--...-->
</metadata>
<!--...-->
<manifest>
<!--...-->
<item href="MyCoverImagejpg" id="my-cover-image" media-type="image/jpeg" />
<!--...-->
</manifest>
{% endhighlight %}

**2.3 内容封面不能出现两次**

除了上面提到的方法之外，不要再在内容中添加封面，如果添加了，那么可能在图书中会出现两次封面。

但是对于流式排版的书籍来说有一种特殊情况：如果你希望封面是HTML格式的，从而能够兼容其他供应商的软件，那么除了按照上面方式设置好封面以外，还要在OPF文件中，添加如下标签：

{% highlight xml %}
<spine> <itemref idref="my-html-cover" linear="no" /> </spine>
<!--...-->
<manifest> <item id="my-html-cover" href="cover.html" media-type="application/xhtml+xml" /> </manifest>
<!--...-->
{% endhighlight %}

同时，在landmarks nav元素中，添加如下标签：

{% highlight xml %}
<nav epub:type="landmarks">
<ol> <li><a epub:type="cover" href="cover.html "> Cover Image </a> </li></ol> </nav>
{% endhighlight %}

设置封面，还可以在OPF文件中使用下面一种写法，而非使用landmarks nav元素：

{% highlight xml %}
<guide> <reference type="cover" title="Cover Image" href="cover.html" /> </guide>
{% endhighlight %}

##3 目录设置指南
<hr>

亚马逊强烈建议您为所有书籍设置HTML TOC。HTML目录适用与大多数书籍，固定布局的童书、绘本或漫画除外。

**3.1 推荐使用逻辑目录**

亚马逊强烈建议所有的图书包含逻辑目录和HTML目录。这对于提高阅读体验十分重要，因为读者可以通过这个目录在不同章节间比较容易的跳转。用户在一开始就期待能够看到一个HTML目录，而逻辑目录也给用户提供了在书中跳转的一种新途径。如果书长于20页，那么添加逻辑目录就变得尤为重要了。

逻辑目录时通过toc nav元素或者用于XML应用的导航控制文件（NCX）生成的。**注意：**固定布局的书不支持嵌套的锚点标签。
用toc nav元素创建逻辑目录

toc nav元素符合IDPF 3.0标准，详情可见： [http://idpf.org/epub/30/spec/epub30-contentdocs-20111011.html#sec-xhtml-nav-def-model](http://idpf.org/epub/30/spec/epub30-contentdocs-20111011.html#sec-xhtml-nav-def-model)和[http://idpf.org/epub/30/spec/epub30-contentdocs-20111011.html#sec-xhtml-nav-def-types-toc](http://idpf.org/epub/30/spec/epub30-contentdocs-20111011.html#sec-xhtml-nav-def-types-toc)。

创建toc nav元素能够同时创建逻辑目录和HTML目录。

例：

{% highlight html %}
<nav epub: type="toc">
<ol>
<li><a href="Sway_body.html#preface_1">AUTHOR'S NOTE</a></li>
<li><a href="Sway_body.html#part_1">PART ONE</a>
   <ol>
   <li><a href="Sway_body.html#chapter_1">THE HOUSES, 1969</a></li>
   <li><a href="Sway_body.html#chapter_2">ROCK AND ROLL, 1962</a></li>
   <li><a href="Sway_body.html#chapter_3">THE EMPRESS, 1928–1947</a></li>
   </ol>
</li>
</ol>
</nav>
{% endhighlight %}

下面这段取自OPF文件的代码告诉你如何在&lt;manifest>标签中声明toc nav元素。

例：

{% highlight xml %}
<manifest>
<item id="toc" properties="nav" href="xhtml/toc.xhtml" media-
type="application/xhtml+xml"/>
{% endhighlight %}

可以选择将其用于&lt;spine>标签，这样就可以被用来当作HTML目录。

{% highlight xml %}
<spine>
<itemref idref="toc" />
{% endhighlight %}

用NCX创建逻辑目录NCX时IDPF2.0的一部分，请参见http://www.niso.org/workrooms/daisy/Z39- 86-2005.html#NCX。

例：

{% highlight xml %}
<navMap>
<navPoint class="titlepage" id="L1T" playOrder="1">
<navLabel><text>AUTHOR'S NOTE</text></navLabel>
<content src="Sway_body.html#preface_1" />
</navPoint>
<navPoint class="book" id="level1-book1" playOrder="2">
<navLabel><text>PART ONE</text></navLabel>
<content src="Sway_body.html#part_1" />
<navPoint class="chapter" id="level2-book1chap01" playOrder="3">
<navLabel><text>THE HOUSES, 1969</text></navLabel>
<content src="Sway_body.html#chapter_1" />
</navPoint>
<navPoint class="chapter" id="level2-book1chap02" playOrder="4">
<navLabel><text>ROCK AND ROLL, 1962</text></navLabel>
<content src="Sway_body.html#chapter_2" />
</navPoint>
<navPoint class="chapter" id="level2-book1chap03" playOrder="5">
<navLabel><text>THE EMPRESS, 1928–1947</text></navLabel>
<content src="Sway_body.html#chapter_3" />
</navPoint>
</navPoint>
</navMap>
{% endhighlight %}

下面这段取自OPF文件的代码说明了如何将NCX目录添加到一本书中。在&lt;manifest>标签中声明NCX：

{% highlight xml %}
<manifest>
<item id="toc" media-type="appication/x-dtbncx+xml" href="toc.ncx" />
{% endhighlight %}

将其用在&lt;spine>中：

{% highlight xml %}
<spine toc="toc">
{% endhighlight %}

**3.2 HTML的目录必须设置好链接**

在每一本书的开头放置一个HTML目录，这样用户就可以在不同位置（比如章节）之间方便跳转。目录中的各项目必须是HTML链接，这样用户可以点击后去往指定位置。如果目录没有添加链接，那么在Kindle中是没有用处的。

**3.3 HTML的目录必须被引用**

为了能让用户在Kindle菜单中跳转到目录页，在OPF文件中的guide标签中必须引用TOC；或者在用于导航的HTML文件中的landmarks nav元素中必须引用TOC。

在每一种Kindle设备或者应用中，在用户界面上都有一个元素，允许用户从书中任何地方跳转到TOC。

以下是一个在guide标签中引用TOC的示例：

{% highlight xml %}
<guide><reference type="TOC" title="Table of Contents" href="toc.html" /></guide>
{% endhighlight %}

以下是一个在landmarks van元素中引用TOC的示例：

{% highlight html %}
<nav epub:type="landmarks">
<ol><li><a epub:type="toc" href="toc.html">Table of Contents</a></li></ol>
</nav>
{% endhighlight %}

**3.4 在目录中不能出现表格**

不要用HTML的&lt;table>标签创建目录。如果目录中有&lt;table>标签的话，那么目录中的链接就无法点击从而不起作用。表格仅用于表格数据，而不能用于布局。

**3.5 在目录中不要出现页码**

在目录中不要使用页码。Kindle电子书并不是与实体书的页码始终对应。

如果你是从Word中导入的文件，那么使用Word中的标题样式和目录功能。在Word中创建的目录能够正常导入并转换成符合要求的目录。

**3.6 将目录放在书的最前面**

将HTML的目录放在书的一开始而不是结束位置。这样可以确保用户在阅读一开始就可以很自然的见到目录。如果目录放置的位置不正确，那么就会影响到"上次阅读位置"功能。正确的放置位置可以确保用户下载试读样张的时候，能够包含目录。

**3.7 套装书要添加目录**

对于包含不止一本书的套装书来说，在文件开头包含一个含有所有分册书目录的总目录。

##4 LANDMARK NAV元素设置指南
<hr>

**4.1 推荐的LANDMARKS NAV元素**

Kindle平台支持用landmarks nav元素来定义封面、目录以及开始位置（"到开始处"的那个位置）。不要将起始位置设置为空白页。

亚马逊不推荐您在OPF文件中添加额外的landmarks nav元素，因为这样做会使菜单里面的选项灰化，导致用户感到迷惑。

注意！landmarks nav元素，尤其是TOC landmark nav元素并不能替代目录本身。

landmarks nav元素是IDPF3.0标准中的一部分，请参见：[http://idpf.org/epub/30/spec/epub30-contentdocs-20111011.html#sec-xhtml-nav-def-model](http://idpf.org/epub/30/spec/epub30-contentdocs-20111011.html#sec-xhtml-nav-def-model)和[http://www.idpf.org/epub/30/spec/epub30-contentdocs-20111011.html#sec-xhtml-nav-def-types-landmarks](http://www.idpf.org/epub/30/spec/epub30-contentdocs-20111011.html#sec-xhtml-nav-def-types-landmarks)

##5 GUIDE ITEM设置指南
<hr>

**5.1 推荐的GUIDE ITEM**

Kindle平台支持使用guide item设置封面、目录以及开始位置（"到开始处"的那个位置）。不要将起始位置设置为空白页。
亚马逊不推荐您在OPF文件中添加额外的guide item，因为这样做会使菜单里面的选项灰化，导致用户感到迷惑。
注意！Guide item，尤其是TOC guide item并不能替代目录本身。

##6 图片设置指南
<hr>

下面这些规则适用于大部分图书，但是不适用于拥有很多图片的固定布局的童书（请见第4章）以及固定布局的绘本、漫画（请见第5章）。对于封面图片的设置，请见3.2。

**6.1 使用支持的格式**

Kindle平台支持GIF、BMP、JPEG、不透明的PNG以及SVG图片。

当将图片用于表格、图示、地图等包含文字的内容时，要特别注意最终图片的清晰度。

在HTML标签&lt;img>中添加src属性来设置图片。

使用分辨率为300dpi或300ppi的图片。

**6.2 KINDLEGEN 平台会自动转换图片**

单个图片最大为5MB。一个epub最大不能超过650MB。

要想得到最佳效果，在将文件放入KindleGen之前，请将图片在图片大小范围内优化至最高质量。如果自动的图片转换效果不佳的话，请尝试在导入到KindleGen之前优化图片。

**6.3 使用彩色图片**

请在可能并且恰当的情况下，使用彩色图片。Kindle的电子墨设备目前是黑白屏幕，但是在Kind Fire、Kindle for iPhone以及Kindle for PC中，是可以看到色彩的。

**6.4 照片请用JPEG格式**

请使用JPEG格式的照片且图片的质量因子不能低于40。请使用文件大小范围内分辨率最大的照片。KindleGen会重新对这些图片进行处理，使其符合文件格式的要求。

照片不能太小，至少要达到600×800。小于300×400的照片实在是太小，转换期间可能会不予通过。

如果照片是GIF格式或者图片太小的话，即使将图片转换为JPEG格式或人为加大图片大小，对于呈现质量来说也无济于事。还是要找到源头，创建分辨率足够大的JPEG图片。

**6.5 线条图案或者文字请使用GIF格式**

线条图案指的是用有限数量的纯色绘制而成的图案（例如由Illustrator、Paint或PowerPoint绘制的图片）。文本、图表都属于线条图案。

线条图案需要用GIF格式。因为JPEG的算法尝试将图片各部分混在一起，导致线条图案原本清晰的边角变得模糊。

用线条图案替代的文字一定要棱角分明，清晰可读。

在将图片导入到KindleGen之前，先对线条图案的GIF文件进行优化。重新设置图片大小或者压缩JPEG图片会造成线条图案图片的模糊不清和不自然，因此对于线条图案，最好避免使用KindleGen里面的自动转换功能。

优化GIF图片，使其不超过127KB，可以尝试使用如下方法：
* 尝试减少所有色彩的数量。这样做不会改变图片的质量。由于某些反锯齿算法，看起来是黑白色的线条图案可能实际上是彩色的。
* 如果有的话，请去掉图片四周的边距。在剪裁图片的时候，考虑一下图片在白色、褐色和黑色背景上显示出来的效果如何。
* 如果需要的话，改变图片大小，但是要注意文本一定要清晰可读。（参见6.6）

**6.6 线条图案或文字的图片大小和字号大小的要求**

图片中如果包含文本的话，图片不能远远大于屏幕大小。Kindle电子墨设备允许翻转图片，使其能显示得更大些。Kindle Fire和Kindle for iPhone应用都允许放大、缩小或左右移动图片。但是，如果线条图案的图片太大的话，会明显影响阅读体验。

下面这两条规则可以保证包含文字的线条图案的图片在所有Kindle平台上都能显示良好。
* 图片最大不能超过500×600。这样可以避免图片在Kindle设备上被缩小造成上面的文字不可读。
* 小写字母a的高度最小不得低于6px。
* 
以上这两条规则限制了某些表格不能作为图片呈现。非常大的图片要重新进行排版。

**6.7 优先使用HTML，其次考虑图片**

不要将大段文字用图片的形式呈现。如果要包含一整段文字的话，那么不要用图片，而要用HTML。

注意：图片会随着屏幕大小而伸缩，造成文字不可读。而HTML格式的文字会换页显示。

**6.8 图片标题的放置**

亚马逊推荐将图片标题放到相应图片的下方，这样用户可以先看到图片后看到标题。在图片和标题之间添加换行符（例如使用&lt;br />标签），以确保图片标题不会出现在图片的旁边。

**6.9 控制图片的宽高比**

保留图片的宽高比，图片的宽和高不能双双都设置为一个固定的百分比。要么是宽、要么是高可以设置为一个固定的比例（比如100%），其中一个设置为固定百分比之后，另外一个值就要设置为auto，以保留宽高比。

**6.10 用SVG格式正确显示文字**

要用SVG正确显示文字，在SVG代码中，对&lt;text>标签使用字号属性。

例：

{% highlight html %}
<html>  
<body>  
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <text x="20" y="20" font-size=20 fill="red">svg text sample</text>  
</svg> 
</body>  
</html>
{% endhighlight %}

**3.6.11 使用支持的SVG标签和元素**

出版商可以在HTML文件中通过行内标签&lt;svg>、&lt;img>、&lt;embed>或&lt;object>标签引用SVG文件。详情请参见SVG规范http://www.w3.org/TR/SVG/。

例：

{% highlight html %}
<html> 
<body> 
<svg xmlns="http://www.w3.org/2000/svg"><!—Inline SVG--></svg> 
<img src="svgfile1.svg"/> 
<embed src="svgfile2.svg"/> 
<object src="svgfile3.svg"/> 
</body> 
</html>
{% endhighlight %}

支持的SVG元素包括：
&lt;circle> 
&lt;clipPath> 
&lt;defs> 
&lt;ellipse> 
&lt;feBlend> 
&lt;feColorMatrix> 
&lt;feComponentTransfer> 
&lt;feComposite> 
&lt;feConvolveMatrix> 
&lt;feDiffuseLighting> 
&lt;feDisplacementMap> 
&lt;feDistantLight> 
&lt;feFlood> 
&lt;feFuncA> 
&lt;feFuncB> 
&lt;feFuncG> 
&lt;feFuncR> 
&lt;feGaussianBlur> 
&lt;feMerge>
&lt;feMergeNode> 
&lt;feMorphology> 
&lt;feOffset> 
&lt;fePointLight> 
&lt;feSpecularLighting> 
&lt;feSpotLight> 
&lt;feTile> 
&lt;feTurbulence> 
&lt;Filter> 
&lt;font-face> 
&lt;font-face-name> 
&lt;font-face-src> 
&lt;line> 
&lt;linearGradient> 
&lt;marker> 
&lt;mask> 
&lt;metadata> 
&lt;path> 
&lt;pattern> 
&lt;polygon> 
&lt;polyline> 
&lt;radialGradient> 
&lt;rect> 
&lt;stop> 
&lt;style> 
&lt;svg> 
&lt;symbol> 
&lt;text> 
&lt;textPath> 
&lt;tref> 
&lt;tspan> 
&lt;use>

请参阅：[http://www.webkit.org/projects/svg/status.xml](http://www.webkit.org/projects/svg/status.xml)

##7 表格制作指南
<hr>

**7.1 表格仅用于呈现表格数据**

注意！表格仅可以用来呈现表格数据。在Kindle电子书中不允许用表格来实现布局。不要对对话、脚本、年表、目录、列表、侧边栏使用表格。

**7.2 避免大表格**

用图片来显示的表格不能换页，这是因为整幅图片都必须在一个屏幕上显示出来。如果表格是用HTML中的&lt;table>标签实现的，那么就可以实现表格的分页，同时鼠标还可以点到表格的单元格里面。如果表格比屏幕大很多，那么用户使用的时候，要左右移动屏幕才能看全，这十分影响阅读体验。

为了达到最佳的用户体验，表格中的单元格不能包含整段文字也不能包含大幅图片。

如果表格太大，而且单元格中包含了很多文字的话，那么考虑将表格重新排列，保证文字的可读性。单列的设置了不同字号的HTML的文字对于用户来说是最佳阅读体验。

**7.3 创建简单的HTML表格**

用&lt;table>标签创建包含有标准行、列的简单表格。这样的表格在现有的Kindle设备以及Kindle for iPhone上可以正常显示为表格。在Kindle 1上，这些表格会被压缩（所有内容在一列中呈现）。KF8支持嵌套表格和合并单元格，但是亚马逊推荐出版商要谨慎使用嵌套和合并单元格，仅在迫不得已的情况下使用。

colspan和rowspan这样的属性值必须小于等于表格的总列或行数。

**7.4 在需要的时候分割表格**

有的时候，需要将表格显示成图片，但是图片又太大了，使得在Kindle屏幕上显示的时候看不清楚，这时候，分割表格就是一个不错的选择。下面是一个例子，教你如何将一个表格分割成两页上的表格。同样方法也可以用于多页的表格图片。

例：在图片纵向60%的位置分割，然后将表头复制到下面那一部分图片的上方。将下面的一部分图片和复制的表头拼成一幅图片。这样，最后两幅图片是等宽的，而且都是带有表头的。

编辑的时候使用源图片，而不是使用转换过的GIF图片，否则的话图片会转换成GIF两次，造成图片质量低下。

**7.5 优化表格，使其达到最佳大小**

优化后的表格不能大于Kindle屏幕的10倍大小。Kindle屏幕大约是24行60个字符，Kindle DX可以显示更多字符。字数限制指的是每行上显示的字符数。行数和每行上的最多字符数有多种搭配（详见下图）。如果给定行数的表格，字符数超过了限制，那么就请将该表格分割为更小的表格或图片。

行数、（每行）最多字数<br>
1—24、600<br>
25—48、300<br>
49—72、180<br>
72—120、120<br>
121—240、60<br>

##8 Adobe Digital Editions兼容性指南
<hr>

当使用Adobe Digital Editions的时候，确保manifest里面item的id是唯一的。Adobe Digital Editions并不强制ID的唯一性，这一点与IDPF的标准是不一致的。

{% highlight xml %}
<manifest>
<item id="css1" href="core.css" media-type="text/css"/>
<item id="css2" href="template.css" media-type="text/css"/>
</manifest>
{% endhighlight %}

## 9 样式指南
<hr>

**9.1 用缩进式的HTML目录**

要创建一个实用的、可导航的、多层级的目录，亚马逊推荐在HTML目录中使用如下语法。下面这个例子说明了利用style属性和CSS类写同一效果的两种方法：

使用style属性：

{% highlight html %}
<div>Section 1</div> 
<div style="margin-left:1em;">Chapter 1</div>
<div style="margin-left:1em;">Chapter 2</div>
<div style="margin-left:1em;">Chapter 3</div>
<div style="margin-left:2em;">Subchapter 1</div>
<div style="margin-left:2em;">Subchapter 2</div>
<div style="margin-left:1em;">Chapter 4</div> 
<div style="margin-left:2em;">Subchapter 1</div>
<div>Section 2</div>
{% endhighlight %}

使用CSS类：
{% highlight html %}
<style> 
div.chapter { margin-left: 1em} 
div.subchapter { margin-left: 2em} 
</style>
<div>Section 1</div>
<div class="chapter">Chapter 1</div> 
<div class="chapter">Chapter 2</div> 
<div class="chapter">Chapter 3</div> 
<div class="subchapter">Subchapter 1</div> 
<div class="subchapter">Subchapter 2</div> 
<div class="chapter">Chapter 4</div> 
<div class="subchapter">Subchapter 1</div> 
<div>Section 2</div>
{% endhighlight %}

**9.2 正确设置侧边栏**

要给KF8格式的书中添加侧边栏内容，通过CSS添加float元素。但是，如果电子书格式是Mobi 7，则要在侧边栏内容的上下添加&lt;hr />标签，将其与主干内容的文本区分开来。当指定浮动元素的位置的时候，避免使用负的em值。

## 10 HTML指南
<hr>

**10.1 建立结构清晰的HTML文档（XHTML）**

KF8支持HTML5.0，但是下面这些HTML的特性无法完全支持：forms、frames和Javascript。
当为Kindle建立HTML或者XHTML源文档的时候，请参阅下面这几本启蒙书，它会告诉你如何创建结构清晰的HTML文档。

[HTML, XHTML, and CSS by Elizabeth Castro (published by Peachpit Press)](http://www.amazon.com/HTML-XHTML-and-CSS/dp/B000SEFC5Q)、[Beginning HTML with CSS and XHTML: Modern Guide and Reference by David Schultz and Craig Cook (published by Apress)](http://www.amazon.com/Beginning-HTML-CSS-XHTML-Reference/dp/B001D25ZPE)和[Beginning Web Programming with HTML, XHTML, and CSS by John Duckett (published by Wrox)](http://www.amazon.com/Beginning-Programming-HTML-XHTML-ebook/dp/B000VZQVVG)。

**10.2 锚点必须加在格式标签的前面**

对的写法：

{% highlight html %}
<a name=”Chapter1”/><h1>Chapter 1</h1>
{% endhighlight %}

错的写法：

{% highlight html %}
<h1><a name=”Chapter1”/>Chapter 1</h1>
{% endhighlight %}

**10.3 Epub中的Guide Item是可选的**

Guide item在Epub格式中是可选的，但是非常推荐可以添加进去。Kindle支持封面、目录以及文本guide item。如果你选择不添加封面、目录的guide item，这些项目也还是会在Kindle目录中出现，不过是以灰化不可点击的形式。

**10.4 使用单列布局；避免绝对位置**

使用单列布局，尽量避免使用position: absolute来进行对齐。

**10.5 用position: absolute来设定图片上面显示的文字**

图片上面显示的文字需要精确定位，因此可以用position: absolute来实现。仅将该属性设置用于例如童书这样的固定布局的书籍，使文字固定在相对于背景图片元素的特定位置。

**10.6 避免使用负值**

在定位文本和设定外边距的时候，避免使用负值。以负值来定位，而且没有用内边距抵消的话，会造成内容显示到屏幕外面。比如说，如果你想要text-indent: -2em，那么要同时设置padding-left: 2em。

**10.7 避免使用脚本**

不支持脚本。在转换的时候，所有源文件中的脚本都会被删去。带有动画的SVG也是不支持的。

**10.8 避免对行高使用负值**

不要将行高设为负值。不支持这样的设置。

##11 嵌入字体指南
<hr>

KF8支持在电子书中嵌入字体。这些字体可以是Open Type（OTF）或True Type（TTF）。Kindle不推荐使用Type 1（Postscript）字体。为了能够给Kindle读者以最佳阅读体验，使用Type 1字体的流式排版的电子书都会用Kindle的默认字体显示。在支持KF8的设备或者应用中，用户可以选择是否使用出版社提供的字体。

对嵌入电子书的字体文件进行了有意识的混淆，从而减少复用的可能性，但是出版商自己也有责任确保拥有字体的使用权限和许可。除非嵌入的字体对于内容意义有影响，否则亚马逊推荐使用安装在Kindle设备和应用中的默认系列字体，因为这些字体本身就经过挑选，以保证高质量的文字显示。

目前，在设备以及应用中，只有嵌入的字体是不可得的。出版商不需要在Kindle书中包含进Charis字体，因为这是一种开源授权字体。当选择某一种字体的时候，请考虑有视觉障碍的人的使用和视觉感受，选择简单、清晰，并且在所有平板或电子墨背景上能够产生鲜明对照的字体。

##12 外部链接指南
<hr>

只有在能够直接提升阅读体验、完善阅读内容的情况下，才考虑在Kindle电子书中添加外部链接。下面几种是可以考虑添加外链的情况：

* 链接至与内容直接相关的多媒体内容
* 链接至额外的辅助资源（例如：核对清单、评测表格、模型图案等类似的可供打印的材料）
* 链接至主题网址（例如：在关于美国政府的书中添加链接至whitehouse.gov的链接）
* 链接至图书或作者的社交媒体（例如：Twitter）

下面是避免添加的一些外链：

* 链接至淫秽内容
* 链接至亚马逊以外的eBook网店
* 链接至需要填入用户信息的网页表单（例如：邮箱、地址等）
* 链接至违法、有害、侵权或粗鲁的内容
* 链接至恶意内容（例如：病毒、钓鱼网站等）。

亚马逊保留自行移除这些链接的权利。


