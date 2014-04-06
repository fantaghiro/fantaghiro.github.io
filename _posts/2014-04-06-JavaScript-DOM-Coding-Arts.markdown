---
layout: post
title: JavaScript DOM编程艺术（第2版）读书笔记
category: writeups
tags:
- 读书笔记
- javascript
- 前端
---

<!--more-->

# 一、JavaScript简史

# 二、JavaScript语法

## 语法

### 语句

可换行分割也可分号分割，推荐后者

### 注释


- 单行注释用 //
- 多行注释用 /\* \*/

<!--
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


\+ \- / \* 

= 用于赋值

()

\+\+ \-\-

\+ 可用于拼接字符串

alert("10" + 20); 会返回字符串”2010“

alert (10 + 20); 会返回数值30

\+= 它可以一次性完成“加法和赋值”操作，例如：

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


\> < >= <= == != === !==

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

-->
