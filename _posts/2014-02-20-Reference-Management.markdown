---
layout: post
title: 我的文献管理环境
category: edu
description: 文献管理对我来说已经是个老大难问题了。
tags:
- 文献管理
- 科研
- 软件评测
---

今天终于搭建成功了一个自己比较满意的文献管理环境。前期测试期间试用了Mendeley, Zotero, Colwiz, Note-express, CNKI E-learning。但是由于下面的几点需求，最终决定了这样的方案：

> #### Windows系统下 ####
> Zotero + FileLocator
> #### Mac系统下 ####
> Zotero + Spotlight

下面讲一下这样决定的原因。首先，我所阅览的文献大多来自CNKI的中文文献，很多软件对于抓取国外文献的题录都轻而易举，但是对于国内文献却无能为力，比如Mendeley、Colwiz。在抓取题录方面Note-express的功能是最强的。下载下来的PDF文档拖进去，立即就有题录信息的列表出来。但是个人发现在Zotero配合使用其Chrome的插件Zotero Connector之后，其实效果也不错。打开CNKI某一个文件的网页，在浏览器地址栏右侧会出现一个文件样式的图标，点击即可将相关文献的元数据抓取到Zotero里面了。在这里不得吐槽一下CNKI的E-learning，自家出的软件，竟然连自家文献的题录都抓取不好，实在不该。

由于Zotero是Windows和Mac平台都有的，也就是说两个平台上的文献题录问题已经解决。下面需要解决的问题就是文献内容检索，具体来说就是PDF的检索问题。这一点，Mendeley做得比较好，但是由于题录问题没有解决所以作罢，另择它法。Zotero号称安装了相应搜索的高级插件，就可以实现PDF的全文检索。但事实情况是，我发现Zotero的PDF全文检索功能存在有缺陷，经常出现检索不到或者检索结果不准确。另外，Zotero不提供检索结果文件内容快速预览的方式，因此即使检索出来某个文件含有关键词，也还是要打开文件才能查看得到。那么没有办法，最终决定在Windows上使用FileLocator这个软件，解决检索问题。有兴趣的同学可以瞅瞅善用佳软的针对该软件的[详细介绍](http://xbeta.info/filelocator-pro.htm)。

对于Mac来说，PDF的全文检索是默认内建的，因此省去了不少气力。

环境搭好，开始种花养草吧！
