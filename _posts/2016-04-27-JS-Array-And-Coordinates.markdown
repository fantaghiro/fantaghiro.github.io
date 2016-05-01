---
layout: post
title: Javascript数组与坐标
category: study
description: 简单讨论一下JS中的数组与坐标的映射关系
tags:
- 学习笔记
- js
- 数组
- 坐标
---

前几日，看*Eloquent Javascript*一书，其中第二单元最后又这么一道题：用代码创建一串字符串，形成8×8的网格。其中，使用 newline character 也就是 \\n 来分行。网格的每个位置要么是一个空格，要么是一个#号。这些字符要形成黑白棋盘一样的布局。将这一串数组传给console.log之后，应当打出下面这样的形式：

```js
 # # # #
# # # # 
 # # # #
# # # #  
 # # # #
# # # # 
 # # # #
# # # # 
```

题目要求，要在程序中定义一个 size = 8 的变量，当传入不同的数值时，这个黑白棋盘的大小可以随意改变。一开始我自己写得很麻烦，进行了多重的判断和循环才得以实现。看了书上的参考代码之后，顿觉十分优雅：

```js
var size = 8;
var str = "";
for(var x = 0; x < size; x++){
	for(var y = 0; y < size; y++){
		if((x+y)%2){
			str += "#";
		} else {
			str += " ";
		}
	}
	str += "\n";
}
console.log(str);
```

在此例中，虽然题干中说的是网格，但是由于网格的单位大小相同，其实也可以视为坐标系来看待。

- 按照坐标来看，上述x和y分别代表了横坐标和纵坐标
- 按照网格来看，上述x和y分别代表了行号和列号

倒推回来，如果将网格的字符视为一个一维数组（先忽略其中的换行符），那么根据一维数组中某个元素的index，就可以得到它在这样一个网格中的行号和列号（或者说它在坐标系中的x和y值）。方法也十分常见：

对于一维数组，可以字形设置宽高，将其视为二维的来使用，例如：

```js
var arr = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11];
var width = 4, height = 3;
/*
0, 1, 2, 3,
4, 5, 6, 7,
8, 9, 10, 11
*/

//要想得到其中某个数字（比如6）在宽为4、高为3的网格（坐标系）中的位置（即坐标或行列号），可以通过该数字的index来反向取得。下面以数字6为例：

var index = arr.indexOf(6);
console.log(index);
var row = Math.floor(index/width);
var col = index % width;

console.log("row: ", row, "; col: ", col);
//row: 1; col: 2 注意，这时候row和col都是从0开始的

//另外根据坐标中的位置，也可以得到数组中某个处于这个位置的值，例如 (2, 1) 这个坐标位置的数字，我们看到是6。
//要得到6的位置，只需要用 x + y * width 就可以得到。如：2 + 1 * 4 = 6

//注意，行列的概念与坐标的概念，两者是相对的。如果得到行号和列号，那么行号所代表的其实是y轴的值；列号代表的其实是x轴的值。
```

可能引用*Eloquent Javascript*第7章中的一个例子，可以看得更明白。当我们面对的是二位数组时，可能使用行列的概念更加的直观，如：

```js
var grid = [["top left",    "top middle",    "top right"],
            ["bottom left", "bottom middle", "bottom right"]];
console.log(grid[1][2]);
// → bottom right
//这里的grid[1][2]中的1、2可以分别视为行号为1、列号为2（两者都是从0开始记）
```

如果面对的是一维数组，那么用坐标的概念就更为直观，如：

```js
var grid = ["top left",    "top middle",    "top right",
            "bottom left", "bottom middle", "bottom right"];
console.log(grid[2 + (1 * 3)]);
// → bottom right
//这里的grid[2 + (1 * 3)] 中的2为x值，1为y值，3为width。
```

关于网格与坐标的使用，*Eloquent Javascript*中用到过很多次。很有意思的就是在第7章 Electronic Life 里面，用到的几个对象：

首先与坐标相关的就是坐标点了。作者定义了一个名为Vector的对象，可以简单理解为坐标的操作：

```js
function Vector(x, y){
	this.x = x; this.y = y;
}
Vector.prototype.plus = function(other){
	return new Vector(this.x + other.x, this.y + other.y);
	//此处定义了两个向量相加的运算
}
Vector.prototype.times = function(factor){
	return new Vector(this.x * factor, this.y * factor);
	//此处定义了向量乘法的运算
}
```

现在坐标点有了，接下来就是坐标系或者网格了。作者定义了Grid这样一个对象，如下：

```js
function Grid(width, height){
	this.space = new Array(width * height);
	//该Grid中的space属性其实就是一个width*height这么长的一维数组
	this.width = width;
	this.height = height;
}
Grid.prototype.isInside = function(vector){
	return vector.x >= 0 && vector.x < this.width && vector.y >= 0 && vector.y < this.height;
	//该方法判断一个坐标是否在网格中
}
Grid.prototype.get = function(vector){
	return this.space[vector.x + this.width * vector.y];
	//此处定义了返回space这个数组中指定坐标位置的值的方法。这里就用到了 x + y * width 来寻找的
}
Grid.ptototype.set = function(vector, value){
	this.space[vector.x + this.width * vector.y] = value;
	//此处定义了设置space这个数组中指定坐标位置的值的方法。
}
//注意：space其实一直是一个一维数组，但是却可以将其视为二维分布的，根据坐标来进行设置和取值。
```

要看行列与坐标x、y的对应关系，下面这个例子可能更清楚一些

```js
var objectMap = [];
var plan = ["############",
   			"#     #    #",
   			"#   ~    ~ #",
   			"#  ##      #",
   			"#  ##  o####",
   			"#          #",
   			"############"];
var width = plan[0].length;
var height = plan.length;
var chr = {
	"#": "wall",
	" ": "null",
	"~": "water",
	"o": "human"
}
plan.forEach(function(line, y){ //注意这里的第二个参数是y，也就是行数
	for(var x = 0; x < line.length; x++){ //这里遍历的是x，也就是列数
		objectMap[x + y * line.length] = chr[line[x]];
	}
});
console.log(objectMap);

/*
["wall", "wall", "wall", "wall", "wall", "wall", "wall", "wall", "wall", "wall", "wall", "wall", 
"wall", "null", "null", "null", "null", "null", "wall", "null", "null", "null", "null", "wall", 
"wall", "null", "null", "null", "water", "null", "null", "null", "null", "water", "null", "wall", 
"wall", "null", "null", "wall", "wall", "null", "null", "null", "null", "null", "null", "wall", 
"wall", "null", "null", "wall", "wall", "null", "null", "human", "wall", "wall", "wall", "wall", 
"wall", "null", "null", "null", "null", "null", "null", "null", "null", "null", "null", "wall", 
"wall", "wall", "wall", "wall", "wall", "wall", "wall", "wall", "wall", "wall", "wall", "wall"]
 */
```






