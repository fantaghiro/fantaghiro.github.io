---
layout: post
title: 妙味课堂——HTML+CSS基础笔记
category: study
tags:
- html
- css
- 妙味课堂
- 前端基础
- 学习笔记
---

妙味课堂的课程讲得非常的清楚，受益匪浅。先把HTML和CSS基础课程部分视频的学习笔记记录如下：

- 这里是目录
{:toc}

#PS基础

##前端需要的PS技能
- PS技能（前端需要）：切图、修图、测量
- PS工具：
    - 移动工具
    - 矩形选框工具
    - 裁切工具
    - 吸管工具
    - 横排文字工具
    - 手抓（快捷键：空格）
    - 缩放（快捷键：Ctrl + 和 Ctrl -）
    - 标尺（快捷键：Ctrl R，主要是拖出参考线。矩形区域选择的时候，按住Ctrl，就能贴合参考线）
    - 自由变换（快捷键 Ctrl T）
    - 盖印可见图层（Ctrl Alt Shift E）
    - 储存为web格式（Ctrl Alt Shift S）

##图片格式
- PSD（源文件）
- JPG、GIF、PNG（导出图）
    - JPG：不支持透明半透明，所有空白区域填充白色（网页中的大图、高清图：体积大）
    - GIF：支持透明，不支持半透明（网页中的小图标、动态图片）
    - png8：支持透明，不支持半透明（网页中的小图标）
    - png24：支持透明，也支持半透明（图像中存在半透明效果的图片）

##PSD测量注意事项
- 文字右方和下方会有1像素的默认间隙

#代码初识

- html 超文本标记语言（结构）
- CSS 层叠样式表（样式）
- js javascript（行为）

文件编码格式与代码编码格式一致的时候，网页才不会出现乱码，才可以显示正常。

- GB2312 中文简体标准
- utf-8 国际标准

样式的位置：

- 行间样式
- 内部样式
- 外部样式表

##background

~~~
background: {
    url(bg.jpg) center top no-repeat gray fixed;
}
~~~

等价于：

~~~
#bg {
background-image: url(bg.jpg);
background-position: center top;
background-repeat: no-repeat;
background-color: gray;
background-attachment: fixed;
}
~~~

##border

- border-top/right/bottom/left
- solid dash dotted(IE6不支持)

## padding

- padding-top/right/bottom/left
- 内边距相当于给一个盒子加了填充厚度，会影响盒子大小

##margin

- margin-top/right/bottom/left
- 上下外边距会叠压
- 父子级包含的时候，子级的margin top会传递给父级；（内边距替代外边距）
- 如果给一个盒子仅设置margin-left: auto，那么盒子会跑到最右边；如果设置margin-right: auto，那么盒子就会跑到最左边。同时设置margin-left和margin-right为auto，可以使盒子居中。

##盒模型和结构样式

- 盒子大小 = border + padding + width/height
- 盒子宽度 = 左border + 左padding + width + 右padding + 右border
- 盒子高度 = 上border + 上padding + height + 下padding + 下border

常见样式——结构

- width 宽度
- height 宽度
- background 背景
- border 边框
- padding 内边距
- margin 外边距

复合属性：一个属性多个属性值的命令

##常见文本设置

- font: font-style | font-weight | font-size/line-height | font-family;
- font-size（一般为偶数，中文最小号12px）
- font-family（中文默认宋体、西文默认是arial，可用逗号分隔多种字体）
- color（英文、rgb、十六位进制色彩值）
- line-height（文字是在行高的上下居中）
- text-align
- text-indent（首行缩进，用em缩进字符）
- font-weight
- font-style
- text-decoration：underline、overline、line-through
- letter-spacing
- word-spacing（以空格为解析单位）

##img

- 注意写img的alt属性

##a标签

- target="_self"/"_blank"
- 在head中添加如下代码，可以让页面中所有的链接都在新页面中打开，其中base代表默认

~~~
<base target="_blank"/>
~~~

- a标签的作用
    - 链接（a标签中放链接）
    - 下载（href的路径是文件路径）
    - 锚点（a的href中放的是id）

##常见标签和SEO浅析

- 标题h标签
- 段落p标签
- 强调strong标签（粗体）
- 强调em标签（斜体）
- span标签
- 有序列表ol标签
- 无序列表ul标签
- 列表项li
- 定义列表dl
- 定义列表标题dt
- 定义列表项dd

浅析SEO（搜索引擎优化）

部分方法：
1. 页面标签语义化
2. 使用对SEO有利的标签：h1/h2/h3/strong/em...
3. 提高页面关键词密度
4. 其他

SEM：搜索引擎营销；（包含SEO）

##基础选择符

- id选择符 #
- class选择符 .
- 类型选择符 p div a img等
- 群组选择符 用逗号,分隔
- 包含选择符 用空格分隔
- 通配符 *

##选择符优先级

- 同级样式默认后者覆盖前者
- 样式优先级（级别问题，官大一级压死人；只看样式权重，与样式名称在html中的先后无关，只跟样式style中的先后顺序有关）
    - 类型选择符（1）
    - class选择符（10）
    - id选择符（100）
    - style行间样式（1000）
    - js动态修改行间样式

##a伪类详解

- link 未访问（默认）
- hover 鼠标悬停（鼠标划过）
- active 链接激活（鼠标按下）
- visited 访问过后（点击过后）
- 注意上面四者的书写顺序 a:link → a:visited → a:hover → a:active，这样在链接点击之后，a:hover和a:active的样式才不会被a:visited的样式覆盖，仍然起效。

a伪类的应用：

1. 四个伪类全用（搜索引擎、新闻门户、小说网站）
2. 一般网站只用 a {} 和 a:hover {}

a伪类的兼容

- IE6不支持a以外其他任何标签的伪类
- IE6以上的浏览器支持标签的hover伪类

##标签默认值样式重置

~~~
/* 默认样式重置（css reset） */
body, p, h1, h2, h3, h4, h5, h6, dl, dd { margin: 0; font-size: 12px; /* font-family */ }
ol, ul { list-style: none; padding: 0; margin: 0; }
a { text-decoration: none; }
img { border: none; }
……
~~~

##标签基本特性和转换

- 内联、内嵌、行内属性标签 a、span、strong、em
    - 默认同行可以继续跟同类型标签
    - 内容撑开宽度
    - 不支持宽高
    - 不支持上下的margin和padding
    - 代码换行被解析（如果内联元素在代码中换行了，那么在页面中，就会体现为内联元素之间的空隙）
- 块标签 p、div、h1~h6、ol、ul、dl
    - 默认独占一行显示
    - 没有宽度时，默认撑满一排
    - 支持所有css命令

- display: block; 显示为块
- display: inline; 显示为内嵌

##inline-block的特性和应用

特性：

- 块在一行显示
- 行内属性标签支持宽高
- 没有宽度的时候，内容撑开宽度

问题：

- 代码换行被解析（代码中inline-block换行写，在页面中inline-block元素之间会有空隙）
- IE6/7不支持块属性标签的inline-block

关于代码换行解析（页面中内联元素和inline-block元素之间的空隙）：

空隙为一个空格的大小，也就是页面上默认字号的一半。比如页面上默认字号为12px，那么它们之间的空隙就是6px。

inline-block的应用：分页导航

- 分析结构（div包一排a）
- a标签支持宽高并在一排显示，因此要设置inline-block
- 有hover效果
- 当前页的页码上不能点
    - cursor指针样式（规定要显示的光标的类型）
    - cursor: pointer | text | move ...
    - cursor: url(hand.cur), pointer; 如果前面图片没引入进来，就用后面的pointer

##前端规范

1. 所有标签的书写均为英文半角状态下的小写
2. id, class必须以字母开头
3. 所有标签必须闭合
4. html标签用tab键缩进
5. 属性值必须带引号
6. &lt;!-- html注释 --&gt; 注意注释内容与横线之间要有空格
7. /* css注释 */ 注意星号与文字之间要有空格
8. ul, li/ ol, li/ dl, dt, dd拥有父子级关系的标签
9. p, dt, h标签，里面不能嵌套块属性标签
10. a标签不能嵌套a
11. 尽量不要用内联元素去嵌套块

##浮动的原理 left/right/none 以及清除浮动的各种方法

**浮动的定义：**元素加了浮动，会脱离文档流，按照指定的一个方向移动，直到碰到父级的边界或者另外一个浮动元素停止。

1. 使块元素在一行显示
2. 使内嵌元素支持宽高
3. 在不设置宽度的时候宽度由内容撑开
4. 脱离文档流（文档流是文档中可显示对象在排列时所占用的位置）
5. 提升层级半层（只够挤进元素本身，元素里面的内容，如文字，图片等，还是会被挤出来）

**clear left/right/both/none**

clear控制元素的某个方向上不能有浮动元素

**清除浮动（撑开父级元素）**

- 方法一、 给父级元素加高（问题：扩展性不好）

- 方法二、 给父级也加浮动（问题：页面中所有元素都加浮动，margin左右自动失效。Float's Bad!）

- 方法三、 用父级添加display: inline-block来清除浮动（问题：margin左右自动失效）

- 方法四、 在浮动元素下边加上&lt;div class="clear"&gt;&lt;/div&gt;空标签清浮动（问题：IE6最小高度19px；解决后IE6下还有2px偏差）

~~~
.clear {
    height: 0px;
    clear: both;
    font-size: 0;
}
~~~

**IE6下的最小高度问题：**

在IE6下高度小于19px的元素，高度会被当作19px处理

解决办法：给该元素加font-size: 0; 这样只能处理到最小2px，再小也没办法了。

- 方法五、在浮动元素下面加&lt;br clear="all" /&gt; （问题：不符合W3C标准，样式混入了html）
- 方法六、给浮动元素的父级元素加上clear类，然后给该元素的after伪类设置如下样式（问题：IE6、7不支持after伪类，为了兼容IE6、7，还要给父级元素加上样式zoom:1）

~~~
.clear:after {
    content: "";
    display: block;
    clear: both;
}
~~~

**注意：在IE6、7下，浮动元素的父级有宽度的话，就不用清除浮动。**

在IE中，子元素的宽高要么是跟着父级走的，要么是跟着内容走的。这个可以用haslayout来调节。但是haslayout不会自动控制。haslayout的默认值为false。但是用了特定样式的时候，haslayout会变成true。具体可以看这里[百度百科](http://baike.baidu.com/view/2945869.htm)的词条。

当haslayout触发的时候，会根据元素内容大小或者父级的大小来重新计算元素的宽高。所以在IE6、7下，如果给浮动元素的父级加了宽高的话，那么触发了haslayout。该父级元素就根据其内容，及子元素来重新计算宽高，也就清除了浮动。如果父级元素没有加宽高的话，通过加zoom: 1;来触发haslayout，就可以解决问题了。也就是说，为了兼容IE6、7，除了给父级元素加上clear类，然后该给父级元素的after伪类添加上述样式之外，还要给该父级元素加上zoom: 1;的样式。也就是如下代码：

**最终推荐使用的清楚浮动的方法**

~~~
.clear { /*用来处理IE6、7*/
    zoom: 1;
}
.clear:after { /*用来处理其他浏览器*/
    content: "";
    display: block; /*或display: table;也可以*/
    clear: both;
}
~~~

zoom的作用就是放大或缩小。zoom在不同浏览器中不兼容。

**overflow的作用：**

overflow并不是各浏览器兼容的。效果不同。overflow针对溢出的。

overflow的各个设置：

- auto 溢出显示滚动条
- scroll 默认就显示滚动条
- hidden 溢出隐藏
- visible 默认值

要执行overflow样式，首先要检测父级元素中的内容是否超出其宽高。如果子元素是浮动元素，父级元素又设置了固定宽高的话，如果子元素大于固定宽高的父级元素，并且父级元素设置了overflow: auto;会看到有滚动条出现。那说明，overflow不仅可以检测到浮动元素是否溢出，而且也可以让父级元素包住浮动的子元素。那么，即使父级元素没有设置宽高，给父级元素设置了overflow的样式，也可以清除浮动。

- 方法七：给浮动元素父级加overflow: hidden;或overflow: auto;来清除浮动，并且一定要配合zoom: 1使用。（问题：IE6下，overflow没有包住浮动子元素的功能，为了兼容，还是要加zoom: 1来解决一下）。










    

        


    

    
