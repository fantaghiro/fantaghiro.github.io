---
layout: post
title: Javascript的For循环
category: study
description: 深入理解JS中的for循环
tags:
- 学习笔记
- js
- 循环
---

*Eloquent Javascript*第二章的第一个练习题十分简单，题目要求利用console.log打出下面一个三角形状：

```
#
##
###
####
#####
######
#######
```

第一反应是for循环，用`for(var i = 1; i < 8; i++)`。但是看过答案之后，发现自己的方法还是比较笨的。在作者提供的答案中，是这样写的：

```
for(var str = "#"; str.length < 8; str += "#"){
    console.log(str);
}
```

我个人感觉十分优雅，同时也感觉到自己以前对for循环的理解有些太机械化了。在w3schools上，对于for循环是这样明确说明的：

```
for (语句1; 语句2; 语句3)
{
    被执行的代码块
}
//语句1：在循环（代码块）开始前执行
//语句2：定义运行循环（代码块）的条件
//语句3：在循环（代码块）已被执行之后执行
```

针对for循环，[这里](https://javascriptweblog.wordpress.com/2010/10/11/rethinking-javascript-for-loops/) 有一篇非常好的文章。在此记录下其中的几个例子。

- 这里是一个目录。
{:toc}

通常情况下，for循环是这样用的：

```
for(var i = 0; i < arr.length; i++){
    //do something to each member
}
```

但事实上，对于数组的遍历，目前使用高阶函数的形式更为普遍，如下：

```
arr.forEach(function(item){
    //do something to item
})
```

虽然如此，for循环作为js中的老鸟，还是有些奇技淫巧的，例如文章作者提供了下面这个生成菲波那切数列的代码，用的就是for循环：

```
for(
    var i=2, r=[0, 1];
    i<15 || alert(r);
    r.push(r[i-1] + r[i-2]), i++
);
//alerts "0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377"
```

## for循环基础知识

解剖一下for循环，包含以下四个部分：

```
for (初始代码; 循环条件; 重复的表达式){
    重复的代码
}
```

- 以上所有四个部分都是可选的（不必须）
- 初始代码不非得是变量赋值——任何合法的表达式都可以
- 循环条件和重复表达式不能包含变量声明
- 如果重复代码值包含一句或更好，那么大括号也不是必须的
- 重复的表达式是在重复的代码执行完成之后才进行运算的

将上面的for循环用while循环来模拟，就是下面这个样子：

```
初始代码();
while(循环条件()){
    重复的代码();
    重复的表达式();
}
```

## 探索使用模式

### 传统的数组遍历

```
for(var i = 0; i < arr.length; i++){
    var member = arr[i];
    doSomething(member);
}
```

### 存储数组长度以提高效率

```
for(var i = 0, l = arr.length; i < l; i++){
    var member = arr[i];
    doSomething(member);
}
```

针对这一应用，有人向作者提出异议，认为l会变成全局变量。作者后续举例说明，此处的l仍然是局部变量：

```
var l;
var test = function(arr) {
    for (var i=0, l=arr.length; i<l; i++) {
        var member = arr[i];
    }
    alert(l);
};
test([0,1,2]); //运行到test里面的alert，弹出3
alert(l); //运行到本句，弹出undefined
```

### 将循环条件和重复表达式合并

```
for (var i = arr.length; i--){
    var member = arr[i];
    doSomething(member);
}
```

当i减到0的时候，循环条件即为假，于是循环就停止了。当然，这只适用于你可以倒着遍历的时候。

### 在循环条件那里为member赋值

一般member的赋值都是在大括号里面，其实可以将其移到循环条件处。一旦`each`是undefined的时候，循环就停止了。

```
for(var i = 0, each; each = arr[i]; i++){
    doSomething(each);
}
```

或者：

```
for(var each, i = -1; item = arr[++i];){
    doSomething(each);
}
```

这种写法只适用于密集数组，而且数组里面不能有null、0、“”、或false这样的值。

### 稀疏数组的检测

我们可以将上述模式反过来，检查稀疏数组。下面就是有效检测undefined参数：

```
var func = function(a, b, c){
    for(var i = 0; arguments[i] !== undefined; i++);
    var allArguments = (i >= arguments.callee.length);
    //...
}
```

### 省略大括号

大括号里面重复的代码和小括号里面重复的表达式，其实目的都一样。因此，如果重复代码可以很轻易地放到重复表达式里面，那么整个大括号也就不需要了：

```
function sum(arr){
    for(var i = arr.length, r = 0; i--; r += arr[i]);
    return r;
}
sum([3, 5, 0, -2, 7, 8]); //21
```

### 在循环条件那里藏着一个最终finally执行的语句

我们可以使用布尔运算符 \|\| 来定义循环结束之后，finally运行的一个语句。例如，上面的sum函数，可以设置在运算结束后，alert结果：

```
function sum(arr){
    for(var i = arr.length, r = 0; i-- || alert(r); r += arr[i]);
    return r;
}
```

但是，如果你循环结束后finally执行的语句返回的不是false的值，那么就陷入无限循环了。因此，要避免这样的问题，可以在final的表达式里面添加 && 运算，确保最后有false的值：

```
function sumAndMultiply(arr, x){
    for(var i = arr.length, r=0; i-- || ((r = r * x) && false); r += arr[i]);
    return r;
}
sumAndMultiply([3, 5, 0, -2, 7, 8], 5); //105
```

也有人推荐使用void运算符：

```
function sumAndMultiply(arr, x) {
        for (var i=arr.length, r=0; i-- || void (r = r*x); r += arr[i]);
    return r;
}
```

### 在初始代码处不进行变量声明

```
function myFunction(arr){
    var i;
    //...
    for(i = 0; i < arr.length; i++){
        //...
    }
    //...
}
```

下面的这种用法不见得好，但是你能看到，初始代码里确实不非得声明变量：

```
var i = 0;
for (
    console.log('start:', +new Date);
    i < 1000 || console.log('finish:', +new Date);
    i++
)
```

