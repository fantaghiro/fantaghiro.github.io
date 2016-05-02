---
layout: post
title: Eloquent Javascript一书第四章最后关于list的练习题
category: study
description: 分别用了迭代和递归两种方式解决
tags:
- 学习笔记
- js
---

*Eloquent Javascript*一书第四章最后有一道练习题，题目是这样的：

js中的object可以用来产生各种各样的数据结构。一种常见的数据结构就是list。list是一系列相互嵌套的对象，第一个对象中包含对第二个对象的引用，第二个又引用第三个，以此类推：

```js
var list = {
    value : 1,
    rest: {
        value: 2,
        rest: {
            value: 3,
            rest: null
        }
    }
};
```

list这样的数据结构有个好处，就是它们能够共享一部分结构。比如说，如果我创建两个新的值：`{value: 0, rest: list}`和`{value: -1, rest: list}`（其中 list 指的都是之前定义的那个变量），那么它们都是相互独立的list，但是它们共享一部分结构，就是最后三个元素。除此以外，最初的那个list依旧还是合法的包含三个元素的list。

要求写出下面几个函数：

- arrayToList函数，能传入一个数组，生成对应的list
- listToArray函数，能传入一个list，生成相应的数组
- prepend函数，能传入一个元素和一个list，生成一个新的list，这个新list的元素就是传入的元素，这个新list的rest就是传入的list
- nth函数，传入一个list和一个序号，可以返回序号位置的元素值。如果序号位置没有元素的话，返回undefined

以下是我用递归方式写的函数：

```js
// Your code here.
function arrayToList(arr){
    if (arr.length == 1){
        return {value: arr[0], rest: null};
    } else {
        return {value: arr[0], rest: arrayToList(arr.slice(1))};
    }
}

function listToArray(list){
    var arr = [];
    if (list.rest == null){
        arr.push(list.value);
    } else {
        arr.push(list.value);
        arr = arr.concat(listToArray(list.rest));
    }
    return arr;
}

function prepend(value, list){
    return {value: value, rest: list};
}

function nth(list, n){
    return listToArray(list)[n];
}


console.log(arrayToList([10, 20]));
// → {value: 10, rest: {value: 20, rest: null}}
console.log(listToArray(arrayToList([10, 20, 30])));
// → [10, 20, 30]
console.log(prepend(10, prepend(20, null)));
// → {value: 10, rest: {value: 20, rest: null}}
console.log(nth(arrayToList([10, 20, 30]), 1));
// → 20
```

以下是书中作者使用迭代方式写的函数：

```js
function arrayToList(array) {
  var list = null;
  for (var i = array.length - 1; i >= 0; i--)
    list = {value: array[i], rest: list};
  return list;
}

function listToArray(list) {
  var array = [];
  for (var node = list; node; node = node.rest)
    array.push(node.value);
  return array;
}

function prepend(value, list) {
  return {value: value, rest: list};
}

function nth(list, n) {
  if (!list)
    return undefined;
  else if (n == 0)
    return list.value;
  else
    return nth(list.rest, n - 1);
}

console.log(arrayToList([10, 20]));
// → {value: 10, rest: {value: 20, rest: null}}
console.log(listToArray(arrayToList([10, 20, 30])));
// → [10, 20, 30]
console.log(prepend(10, prepend(20, null)));
// → {value: 10, rest: {value: 20, rest: null}}
console.log(nth(arrayToList([10, 20, 30]), 1));
// → 20
```

个人感觉迭代的效率更高一些，而且这里的迭代方式也比较直观。如果今后再遇到类似的编程问题的话，应当优先考虑迭代的方式。另外，迭代方式中的listToArray函数中的循环，也应该特别注意。除了数字循环以外，还可以利用对象是否依旧存在，来实现循环。
