---
layout: post
title: phi相关系数的算法
category: study
description: 记录一种简单的相关系数的算法
tags:
- 学习笔记
- 数学
- 统计
- 相关性
---

在阅读*Eloquent Javascript*一书时，在第四章中碰到了phi coefficient的计算问题，决定仔细记录一下。

内容与[该页](https://zh.wikipedia.org/wiki/Phi%E7%9B%B8%E9%97%9C%E4%BF%82%E6%95%B8)相同。

在*维基百科*中，phi相关系数是这样定义的：

> 在统计学里，phi相关系数是测量两个二元变数（binary variables or dichotomous variables）之间相关性的工具，由卡尔·皮尔森发明。

算法如下：

将两个变数排成2×2列联表，注意1和0的位置必须如下表。若只变动x或只变动y的0/1位置，计算出来的phi相关系数会正负号相反。phi相关系数的基本概念是：两个二元变数的观察值若大多落在2×2列联表的“主对角线”（英语：diagonal：左上-右下线）栏位，亦即若观察值大多为(x,y)=(1,1),(0,0)这两种组合，那么这两个变数呈正相关。反之，若两个二元变数的观察值大多落在“非对角线”（英语：off-diagonal：主对角线以外的位置）栏位，对应于2×2列联表，亦即若观察值大多为(x,y)=(0,1),(1,0)这两种组合，则这两个变数呈负相关。例如，我们从两个随机二元变数(x,y)抽样得出这样的2×2列联表：

||y=1|y=0|总计|
|x=1|n<sub>11</sub>|n<sub>10</sub>|n<sub>1·</sub>|
|x=0|n<sub>01</sub>|n<sub>00</sub>|n<sub>0·</sub>|
|总计|n<sub>·1</sub>|n<sub>·0</sub>|n|

其中n<sub>11</sub>, n<sub>10</sub>, n<sub>01</sub>, n<sub>00</sub>都是非负数的栏位记次值，它们加总为n，亦即观察值的个数。由上面的表格可以得出x和y的phi相关系数如下：

\phi = (n<sub>11</sub>n<sub>00</sub> - n<sub>10</sub>n<sub>01</sub>) / Math.sqrt(n<sub>1·</sub>n<sub>0·</sub>n<sub>·0</sub>n<sub>·1</sub>)

对应js的函数如下：

```js
function phi(table) {
  return (table[3] * table[0] - table[2] * table[1]) /
    Math.sqrt((table[2] + table[3]) *
              (table[0] + table[1]) *
              (table[1] + table[3]) *
              (table[0] + table[2]));
}
```
