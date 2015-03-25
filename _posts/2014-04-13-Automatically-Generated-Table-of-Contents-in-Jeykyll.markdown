---
layout: post
title: 在Jekyll搭建的Github博客当中使用kramdown解析器自动生成目录树
category: writeups
description: 博客正文中个层级的内容线性排列，很难看清层次。所以想用自动生成目录树来解决一下。
tags:
- Jekyll
- kramdown
- 技巧
---

昨天生成了博客文章之后，收到了Github发来的邮件。内容说“您的网页已经成功生成，但是发现您的网站的Markdown的解析器是Maruku。Maruku是陈旧的解析器，可能会生成无效的Markdown或HTML，导致您的网站崩溃。”云云。邮件中发来的链接直接推荐我将博客网站的Maruku解析器换为kramdown。我顺藤摸瓜，有探了探kramdown解析器的一些强大功能，发现里面的coderay和自动生成目录的功能对于我来说相当实用。

在写读书笔记的时候，经常会出现这种情况。就是你想清晰地将图书架构在网页上罗列清楚，按照图书目录的结构来撰写总结或者感想。这时候目录树显得格外实用。为了实现这样一个目录树，我试过几种方法。

【方法一：手写法】

手写目录树，添加恰当的CSS样式。缺点：麻烦。

【方法二：使用现有JS脚本】

找到了一个叫做jstree的js脚本。有折叠效果。PC和手机上自适应。但是手机上的显示效果经测试不太理想。

【方法三：用freemind来做读书笔记，然后生成网页】

freemind的兼容性很好，可以导出为各种格式。这一点xmind和很多其他脑图工具都比不上。如果用Boogunote来记笔记的话，也可以与freemind无缝互通。这点真是很好。但是freemind也是因为太老牌了，所以整个界面做的不太显好。而且，除了目录标题以外，其余内容是以注释弹出框的形式出现的。使用freemind做过脑图，并生成过html文件的应该都知道。

【方法四：用kramdown自动生成目录（目前采纳）】

目前采纳的这种方法比较好的一点就是不需要额外手写目录。略有遗憾的是生成的目录不是可以折叠的形式。不过总体上来说，效果不错，由于不额外添加样式，就是简单地在html中生成列表，因此，无论在PC还是在手机上显示都没有什么问题。具体方法如下：

1. 按照正常做的那样在Markdown中写各级标题。例如：

{% highlight html %}

# Header1
{:.no_toc}

content under header1

# Header2

content under header2

## Subheader2-1

content under subheader2-1

## subheader2-2

content under subheader2-2

{% endhighlight %}

上述代码会生成如下内容：

# Header1
{:.no_toc}

content under header1

# Header2

content under header2

## Subheader2-1

content under subheader2-1

## subheader2-2

content under subheader2-2

2. 在想要插入目录的位置添加一个有序或无序列表。第一个列表项的内容无所谓，因为生成的目录会自动替换这一行的内容，在第一个列表项下面添加{:toc}，例如：

{% highlight html %}
- 这里是一个目录
{:toc}
{% endhighlight %}

下面就是自动生成的目录树：

- 这里是一个目录
{:toc}

注意到什么没有？为什么Header 1没有在自动生成的目录里面？那是因为在Header1的markdown下面添加了{:.no_toc}，表示这一个标题不自动产生目录项。

Done。

