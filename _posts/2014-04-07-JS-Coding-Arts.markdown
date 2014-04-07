---
layout: post
title: JavaScript DOM编程艺术（第2版）读书笔记
category: writeups
tags:
- 读书笔记
- javascript
- 前端
---

# 一、JavaScript简史

# 二、JavaScript语法

## 语法

### 语句

可换行分割也可分号分割，推荐后者

### 注释

- 单行注释用 //
- 多行注释用 /\* \*/

### 变量

- 赋值
- 声明变量是好习惯但JS没有强制
  - var mood, age;
  - var mood = "happy", age = 33;
- 变量名
  - 允许包含字母、数字、美元符号、下划线
  - 第一个字符不可以是数字
  - 一般通过下划线或驼峰格式命名长变量名

### 数据类型

JS是弱类型语言（weakly typed）

【1】 字符串

可以用单引号或双引号。用双引号包住单引号，里面的单引号前面要嫁反斜线\进行转义；单引号包住双引号也如此。

【2】 数值

JS允许任意位小数，这样的数成为浮点数。也可以使用负数和负数浮点数。

【3】 布尔值

true 或 false

布尔值不是字符串，不要用引号括起来

### 数组

- var beatles = Array(4);
- var beatles = Array();
- beatles[0] = "John";
- var beatles = ["John", "Paul", "George", "Ringo"];
- var lennon = ["John", 1940, false];
- var name = "John"; beatles[0] = name;
- var names = ["Ringo", "John", "George", "Paul"]; beatles[1] = name [3];
- var lennon = ["John", 1940, false]; var beatles = []; beatles[0] = lennon; beatles[0][0] = "John";

关联数组：用字符串代替数字值

var lennon = Array(); lennon["name"] = "John"; lennon["year"] = 1940; lennon["living"] = false;

但是不推荐使用关联数组，这种情况下推荐使用对象（object）。

### 对象

var lennon = Object();
lennon.name = "John";
lennon.year = 1940;
lennon.living = false;

也可以写成

var lennon = { name:"John", year:1940, living:false };

如果建立 var beatles = Array(); beatles[0] = lennon; 那么beatles[0].name的值就是"John"。

也可以把beatles数组声明为对象而不是传统数组，如：

var beatles = {};
beatles.vocalist = lennon; 那么beatles.vocalist.name得值就是"John"。

## 操作

### 算数操作符


    + - / * 

    = 用于赋值

    ()

    ++ --

    + 可用于拼接字符串

alert("10" + 20); 会返回字符串”2010“

alert (10 + 20); 会返回数值30

    += 它可以一次性完成“加法和赋值”操作，例如：

var year = 2010;
var message = "The year is ";
message += year;

执行完上面语句后，变量message得值将是"The year is 2010"。

## 条件语句

if (condition) {
  statements;
}

if (condition) {
  statements; 
} else {
  statements;
}

### 比较操作符


    > < >= <= == != === !==

### 逻辑操作符


    && || !

## 循环语句

### while循环


while (condition) {
  statements;
}

do ... while 循环

do {
  statements;
} while (condition);

### for 循环


for (initial condition; test condition; alter condition) {
  statements;
}

如：

var beatles = Array ("John", "Paul", "George", "Ringo");

for (var count = 0; count < beatles.length; count++) {
  alert(beatles[count]);
}

##函数

定义函数的语法：

function name(arguments) {
  statements;
}

函数可以用变量传入数据，也可以用return返回数据。我们还可以把函数当作一种数据类型来使用，这意味着可以把一个函数的调用结果赋给一个变量。

###变量的作用域

全局变量 VS 局部变量

如果在某个函数中使用了var，那个变量就将被视为一个局部变量。函数在行为方面应该像是一个自给自足得脚本，在定义一个函数时，一定要把它内部的变量全部明确声明为局部变量。

##对象


对象里的数据可以通过两种形式访问：属性、方法

- 属性：隶属于某个特定对象才能调用的函数
- 方法：只有某个特定对象才能调用的函数

在JS里，属性和方法都使用“点”来访问：

- Object.property
- Object.method()

为给定对象创建一个实例需要使用new关键字。

我们可以利用JS创建自己的对象，JS中还有一系列预先定义的“内建对象”。

###内建对象

如Array对象、Math对象、Date对象等。

###宿主对象

由浏览器提供的预定义对象被称为宿主对象，如Form、Image、Element等。

#三、DOM

##文档：DOM中的“D”

##对象：DOM中的“O”

- 用户定义对象
- 内建对象
- 宿主对象

window对象对应着浏览器窗口本身，这个对象的属性和方法通常统称为BOM（浏览器对象模型）.BOM提供了window.open和window.blur等方法。BOM在JS中名声不好。

##模型：DOM中的“M”

##节点

- 元素节点
- 文本节点
- 属性节点

##获取元素

- getElementById(id)
- getElementsByTagName(tag) 注意这种方法返回的永远是一个对象数组（首先返回的是数组，第二、数组里每一项都是对象）
- getElementsByClassName(class) 注意：HTML5 DOM才支持；要指定多个类名，只要在字符串参数中用空格分隔类名即可）

getElementsByClassName方法很有用，但是要较新浏览器才可以，为了弥补不足，通常用下面的方法来实现自己得getElementByClassName:

{% highlight js linenos %}
function getElementsByClassName(node, classname) {
  if (node.getElementsByClassName) {
    //使用现有方法
    return node.getElementsByClassName(classname);
  } else {
    var results = new Array();
    var elems = node.getElementsByTagName("*");
    for (var i=0; i<elems.length; i++) {
      if(elems[i].className.indexOf(classname) != -1) {
        results[results.length] = elems[i];
      }
    }
    return results;
  }
}
{% endhighlight %}

##盘点知识点

- 一份文档就是一棵节点树
- 节点分为：元素节点、属性节点、文本节点等
- getElementById返回一个对象，对应一个特定的元素节点
- getElementsByTagName和getElementsByClassName将返回一个对象数组，分别对应着文档里的一组特定的元素节点
- 每一个节点都是一个对象

##获取和设置属性

###getAttribute

object.getAttribute(attribute)

###setAttribute

object.setAttribute(attribute, value)

注意：通过setAttribute对文档做出修改后，在通过浏览器得view source选项去查看文档的源代码时看到的仍将是改变前的属性值，也就是说，setAttribute做出的修改不会反映在文档本身的源代码里。这种“表里不一”得现象源自DOM得工作模式：先加载文档的静态内容，再动态刷新，动态刷新不影响文档的静态内容。这正是DOM的真正威力：对页面内容进行刷新却不需要在浏览器里刷新页面。

#四、案例研究：JavaScript图片库

##事件处理函数

- onmouseover
- onmouseout
- onclick

添加事件处理函数的语法为：event = "JavaScript statement(s)"

事件处理函数的工作机制：在给某个元素添加了事件处理函数后，一旦事件发生，相应的JavaScript代码就会执行。被调用的JavaScript代码可以返回一个值，这个值将被传递给那个事件处理函数。例如，给某个链接电价一个onclick事件处理函数，并让这个处理函数所触发的JavaScript代码返回布尔值true或false。这样依赖，当这个链接被点击时，如果那段JS代码返回的值是true，onclick事件处理函数就认为“这个链接被点击了”；反之，如果返回的值是false，onclick事件处理函数就认为“这个链接没有被点击”。

在onclick事件处理函数所触发的JS代码里增加一条return false语句，就可以防止用户被带到目标链接窗口。

###childNodes属性

在一棵节点树上，childNotes属性可以用来获取任何一个元素的所有子元素，它是一个包含这个元素全部子元素的数组：element.childNodes

###nodeType属性

用法：node.nodeType

nodeType属性总共有12种可取值，但其中仅有3种具有实用价值：

- 元素节点的nodeType属性值是1
- 属性节点的nodeType属性值为2
- 文本节点的nodeType属性值是3

###nodeValue属性

如果想改变一个文本节点的值，那就使用DOM提供的nodeValue属性，它用来得到（和设置）一个节点的值：node.nodeValue

###firstChild和lastChild属性

node.firstChild等价于node.childNodes[0]

node.lastChild等价于node.childNodes[node.childNodes.length-1]

#五、最佳实践

##平稳退化（优雅降级）

### “Javascript:”伪协议——不推荐

###内嵌的事件处理函数——如果JS被禁用，也照样无效

###能够优雅降级的方案

{% highlight js %}
    function popUp(winURL) {
      window.open(winURL, "popup", "width=320, height=480");
{% endhighlight %}

{% highlight html %}
    &lt;a href="http://www.example.com/" onclick="popup(this.href; return false;)"> Example&lt;/a>
{% endhighlight %}

按照上面的例子，将href设为真实值，即使js被禁用，依然还是可用的，虽然链接功能上有一点折扣（因为没有打开一个新窗口），但是并未彻底失效。

##向CSS学习

- 结构与样式分离
- 渐进增强

##分离JavaScript

JS不要求事件必须在HTML文档里处理，我们可以在外部JavaScript文件里把一个事件添加到HTML文档中的某个元素上：element.event = action...

##向后兼容

### 对象检测

if (method) {
statements
}

例如：

function myFunction() {
  if (document.getElementById) {
    statements using getElementById
  }
}

另一种方法：

if (!method)

例如：

if (!getElementById) return false;

###浏览器嗅探技术

##性能考虑

###尽量少访问DOM和尽量减少标记

###合并和放置脚本

脚本在标记中的位置对页面的初次加载时间也有很大影响。传统上，我们都把脚本放在文档的&lt;head&gt;区域，这种放置方法有问题。位于&lt;head&gt;块中的脚本会导致浏览器无法并行加载其他文件（如图像或其他脚本）。一般来说，根据HTTP规范，浏览器每次从同一个域名中最多只能同时下载两个文件。而在下载脚本期间，浏览器不会下载其他任何文件，即使是来自不同域名得文件也不会下载，所有其他资源都要等脚本加载完毕后才能下载。

把所有&lt;script&gt;标签都放到文档的末尾，&lt;/body&gt;之前，就可以让页面变得更快。

###压缩脚本

应该有两个js版本，一个是工作副本，可以修改代码看注释；另一个是精简副本，通常在文件名里面加上min字样。

#六、案例研究：图片库改进版

##它支持平稳退化吗

##它的JavaScript语HTML标记是分离的吗

###添加事件处理函数

1）检查点

> 结构化程序设计中有一条：函数应该只有一个入口和一个出口。但是作者认为，函数可以有多个出口。如果出口有多个，则要集中在函数开头部分才可以接受

2）变量名里有什么

3）遍历

4）改变行为

5）完成JavaScript函数

###共享onload事件

方法一：

window.onload = function(){
  firstFunction();
  secondFunction();
}

方法二：

{% highlight js %}
function addLoadEvent(func) {
  var oldonload = window.onload;
  if (typeof window.onload != 'function') {
    window.onload = func;
  } else {
    window.onload = function() {
    oldonload();
    func();
    }
  }
}
{% endhighlight %}

addLoadEvent函数将要完成的操作：

- 把现有的window.onload事件处理函数的值存入变量oldonload
- 如果在这个处理函数上还没有绑定任何函数，就像平时那样把新函数添加给它
- 如果在这个处理函数上已经绑定了一些函数，就把新函数追加到现有指令的末尾


这样如果在页面加载完毕的时候执行两个函数，就可以写：

{% hightlight js %}
addLoadEvent(firstFunction);
addLoadEvent(secondFunction);
{% endhighlight %}

###不要做太多的假设

###优化

三元操作符：

variable = condition? if true : if false

###键盘访问

有些用户可能更喜欢使用键盘。另外，用Tab键跳到一个链接上，然后按下回车也将启用当前链接。因此对于链接来说，有时onclick事件是不够的，还需要onkeypress事件来处理键盘事件。

按下任何一个按键都会触发onkeypress事件。有一种简单的方法能够使onkeypress事件模仿onclick事件，如：

{% highlight js %}
links[i].onkeypress = links[i].onclick;
{% endhighlight %}

但是，小心onkeypress！

尽量不要用onkeypress，有很多情况下会出错！幸运的是onclick事件处理函数比想象得更聪明。即使用tab键移动到某个链接然后按下回车的动作也会触发onclick事件。

###把JavaScript与CSS结合起来

###DOM Core和HTML-DOM

迄今为止学到的几个DOM方法“

- getElementById
- getElementsByTagName
- getAttribute
- setAttribute

这些都是DOM Core得组成部分，不专属于JavaScript。支持DOM的任何一种程序设计语言都可以使用它们。不仅可用于处理网页，还可用于处理任何一种标记语言（比如XML）编写出来的文档。

仅用于网页的话，可以考虑使用HTML-DOM，例如在HTML-DOM中

document.getElementsByTagName("forms")可以简化为document.forms

element.getAttribute("src")可以简化为element.src

#七、动态创建标记

##一些传统方法

<h3>document.write</h3>

缺点：违背了”行为应该与表现分离“的原则；使代码变得不易阅读

<h3>innerHTML属性</h3>

{% highlight html %}
&lt;div id="testdiv">
&lt;p>This is &lt;em>my&lt;/em> content.&lt;/p>
&lt;/div>
{% endhighlight %}

上面这串代码得结构如下：

- 元素节点div下面有属性节点id="testdiv"、元素节点p
- 元素节点p下面有文本节点This is、元素节点em、文本节点 content.
- 元素节点em下面有文本节点my

但是id为testdiv的div得innerHTML是整个的

{% highlight html %}
&lt;p>This is &lt;em>my&lt;/em> content.&lt;/p>
{% endhighlight %}

##DOM方法

###createElement方法

如：document.createElement("p");

两步：

- 创建一个新元素
- 把这个新元素插入节点树

###appendChild方法

如：parent.appendChild(child);

###createTextNode方法

语法：document.createTextNode(text);

###在已有元素前插入一个新元素

语法：parentElement.insertBefore(newElement, targetElement);

其中

- 新元素：你想插入的元素(newElement)
- 目标元素：你想把这个新元素插入到哪个元素(targetElement)之前
- 父元素：目标元素的父元素(parentElement)

###在现有方法后插入一个新元素

【1】编写insertAfter函数

{% highlight js %}
function insertAfter(newElement, targetElement) {
  var parent = targetElement.parentNode;
  if (parent.lastChild == targetElement) {
    parent.appendChild(newElement);
} else {
  parent.insertBefore(newElement, targetElement.nextSibling);
}
{% endhighlight %}

【2】使用insertAfter函数

##Ajax

###XMLHttpRequest对象

###渐进增强与Ajax

###Hijax

#八、充实文档的内容

##不应该做什么

理论上，你可以用JS把一些重要的内容添加到网页上。事实上这是一个坏主意，因为这样依赖JS就没有任何空间去平稳退化。那些缺乏必要的JS支持的访问者就会永远也看不到你的重要内容。

因此下面两条原则要牢记在心：

- 渐进增强
- 平稳退化

##检索和添加信息

在需要对文档里的现有信息进行检索时，以下DOM方法最有用：

- getElementById
- getElementByTagName
- getAttribute

在需要把信息添加到文档里去时，以下DOM方法最有用：

- createElement
- createTextNode
- appendChild
- insertBefore
- setAttribute

#九、CSS-DOM

##三位一体的网页

- 结构层
- 表示层
- 行为层

###结构层（structural layer）

由HTML或XHTML之类的标记语言负责创建。标签（tag），也就是那些出现在尖括号里的单词，对网页内容的语义含义做出描述。

###表示层（presentation layer）

由CSS负责完成

###行为层（behavior layer）

行为层负责内容应该如何响应事件这一问题。这是JavaScript语言和DOM主宰得领域。

###分离

- 使用(X)HTML去搭建文档的结构；
- 使用CSS去设置文档的呈现效果
- 使用DOM脚本去实现文档的行为

不过，这三种技术之间存在着一些潜在的重叠区域。

##style属性

style属性是一个对象

###获取样式

element.style.property

例如：

- element.style.color
- element.style.fontFamily

注意：不管CSS样式属性的名字里有多少个连字符，DOM一律采用驼峰命名法来表示它们。如CSS属性background-color对应着DOM属性backgroundColor

通过style属性获取样式有很大的局限性，因为style属性只能返回内嵌样式，来自外部文件的样式不能用DOM style属性检索出來。

###设置样式

复制操作来设置样式：

element.style.property = value

注释：style对象的属性值永远是一个字符串。如果赋值的时候，value没有加引号，那么JS会把它当作变量处理。

##何时该用DOM脚本设置样式

###根据元素在节点树里的位置来设置样式

###根据某种条件反复设置某种样式

###响应事件

##className属性

可以用setAttribute得方式做这件事，例如：element.setAttribute("class", "intro");

也可以用下面的这种方式：element.className = "intro";

不过这样只能替换类名，要追加类名用这种方式：
element.className += " intro; 注意在intro前面有空格

也可以用如下函数实现。实现步骤如下：

1. 检查className属性的值是否为null
2. 如果是，把新的class设置值直接赋给className属性
3. 如果不是，把一个空格和新的class设置值追加到className属性上去

函数代码如下：

{% highlight js %}
function addClass(element, value) {
  if (!element.className) {
    element.className = value;
  } else {
    newClassName = element.className;
    newClassName += " ";
    newClassName += value;
    element.className = newClassName;
  }
}
{% endhighlight %}

注意对函数进行抽象，使其更具有通用性。

#十、用JavaScript实现动画效果

##动画基础知识

###位置

###时间

JavaScript函数setTimeout能够让某个函数在经过一段预定的时间之后才开始执行。这个函数带有两个参数：第一个参数通常是一个字符串，其内容是将要执行的那个函数的名字；第二个参数是一个数值，它以毫秒为单位设定了需要经过多长时间后才开始执行第一个参数所给出的函数：

setTimeout("function", interval);

在绝大多数时候，把这个函数调用赋值给一个变量将是个好主意：

variable = setTimeout("function", interval);

如果想取消某个正在排队等待执行的函数，就必须事先像上面这样把setTimeout函数的返回值赋给一个变量。你可以用一个名为clearTimeout得函数来取消“等待执行”队列里的某个函数。这个函数需要一个参数——保存着某个setTimeout函数调用返回值的变量：

clearTimeout(variable);

###时间递增量

JS中的parseInt可以把字符串里的数值信息提取出来。如果把一个以数字开头的字符串传递给这个函数，它将返回一个数值：

parseInt(string)

例如：parseInt("39 steps"); 这个函数调用将返回数值：39

parseInt函数的返回值通常是整数。如果需要提取的是带小数点的数值（也就是浮点数），就应该使用相应得parseFloat函数：

parseFloat(string)

例子：moveElement函数

{% highlight js %}
function moveElement(elementID, final_x, final_y, interval) {
  if (!document.getElementById) return false;
  if (!document.getElementById(elementID)) return false;
  var elem = document.getElementById(elementID);

  /*如果上一个movement动画还没有执行完毕，
  就停止执行上一个，而执行下一个*/
  if (elem.movement) {
    clearTimeout(elem.movement);
  }

  var xpos = parseInt(elem.style.left);
  var ypos = parseInt(elem.style.top);
  if (xpos == final_x && ypos == final_y) {
    return true;
  }
  if (xpos < final_x) {
    xpos++;
  }
  if (xpos > final_x) {
    xpos--;
  }
  if (ypos < final_y) {
    ypos++;
  }
  if (ypos > final_y) {
    ypos--;
  }
  elem.style.left = xpos + "px";
  elem.style.top = ypos + "px";
  var repeat = "moveElement('"+elementID+"',"+final_x+"，“+final_y+"，”+interval+")";
  movement = setTimeout(repeat, interval);
}
{% endhighlight %}

#十一、HTML5

##HTML5简介

##来自朋友的忠告

[Modernizr](http://www.modernizr.com/)

要使用Modernizr编写文档，通常都要给<html>元素添加一个no-js类：

{% highlight html %}
&lt;html class="no-js">
{% endhighlight %}

利用这个类，可以在浏览器不支持JS得情况下应用CSS样式。

{% highlight css %}
.nojs selector {
  style properties 
}
{% endhighlight %}

Modernizr脚本一定要放在&lt;head&gt;元素中。这是为了能够让它在文档呈现之前能够创建好新的HTML5元素。如果把它放到文档末尾，等不到它发挥作用，浏览器就开始呈现文档并应用样式了。

##几个示例

###Canvas

###音频和视频

###表单

#十二、综合示例（略）

#附录 JavaScript库（略）
