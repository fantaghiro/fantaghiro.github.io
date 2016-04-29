---
layout: post
title: 一个函数究竟应该定义成多大？
category: study
description: 这里记录了Eloquent Javascript一书，第3章中一个很好的例子。
tags:
- 学习笔记
- js
- function
---

译自*Eloquent Javascript*第3章的部分内容：

将函数引入程序，有两种比较自然的方式。

第一种你会发现自己写了类似的代码好几遍。我们希望可以避免这种情况，因为代码写得越多藏得错就越多，而且别人想要理解你的代码，也要读得更多。因此，我们将重复的功能提取出来，给它一个名字，把它放到函数里面。

第二种你会发现自己需要很多功能，但是这些功能你都还没有写，但是又觉得它们值得有自己的函数。那么，你会先从命名函数开始，然后才会写到函数体的内容。你甚至会先写用到这些函数的代码，然后再实际定义函数究竟是怎么样的。

要给函数起个好名字有多难，就代表了你想要包装起来的概念有多清晰。下面就是一个例子：

我们想要写一个程序，用它来打印两个数字：cows和chickens的数量。在这两个数字后面，要有Cows和Chickens的字样。如果数字达不到三位，我们就在前面补上0。打出来应该像下面这样：

```
007 Cows
011 Chickens
```

很明显，这样一个函数需要两个参数：

```
function printFarmInventory(cows, chickens) {
  var cowString = String(cows);
  while (cowString.length < 3)
    cowString = "0" + cowString;
  console.log(cowString + " Cows");
  var chickenString = String(chickens);
  while (chickenString.length < 3)
    chickenString = "0" + chickenString;
  console.log(chickenString + " Chickens");
}
printFarmInventory(7, 11);
```

你发现要是别人也让你打印出pigs的数量呢？你就得剪切粘贴四行代码，然后修改。这时候，我们就停下来再思考一下。还有其他更好的办法，于是我们首先尝试：

```
function printZeroPaddedWithLabel(number, label) {
  var numberString = String(number);
  while (numberString.length < 3)
    numberString = "0" + numberString;
  console.log(numberString + " " + label);
}

function printFarmInventory(cows, chickens, pigs) {
  printZeroPaddedWithLabel(cows, "Cows");
  printZeroPaddedWithLabel(chickens, "Chickens");
  printZeroPaddedWithLabel(pigs, "Pigs");
}

printFarmInventory(7, 11, 3);
```

但是上面的printZeroPaddedWithLabel有点怪。一个函数里面裹了三件事：打印、补齐位数、添加标签。

我们不应该把所有重复的部分都提取出来。让我们把当个的*概念*提取出来：

```
function zeroPad(number, width) {
  var string = String(number);
  while (string.length < width)
    string = "0" + string;
  return string;
}

function printFarmInventory(cows, chickens, pigs) {
  console.log(zeroPad(cows, 3) + " Cows");
  console.log(zeroPad(chickens, 3) + " Chickens");
  console.log(zeroPad(pigs, 3) + " Pigs");
}

printFarmInventory(7, 16, 3);
```

这里的zeroPad函数，名称上面一目了然，别人也很容易看懂它是干什么的。而且它的用途还非常广泛。

函数可以大致分类两种：一种是要它的副作用（size effect）；另一种是要它的返回值。（当然，也可能同时有副作用和返回值啦）。

举例而言：第一个版本 printZeroPaddedWithLabel就是要它的side effect，让它打印出文字。第二个版本zeroPad就是要它的返回值。通常第二种方式更有用，因为它与其他代码的结合方式更灵活。

一个*纯粹的*函数就是产生值的函数，而且它不仅没有side effect，还不依赖于其它代码的side effect——比如，它不依赖于全局变量，因为有时候全局变量会被其他代码更改。24k纯函数有个很好的特性，就是你用同样的参数调用它，它总是产生同样的值（而且不影响其他任何东西）。这很好理解，因为调用这样一个函数，在脑子里就可以等同于使用它的结果，并且不会改变代码的意义。

当然，side effect也是有用的。一切都是视情况而定的。



