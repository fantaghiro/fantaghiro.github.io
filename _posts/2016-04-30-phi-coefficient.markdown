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

将两个变数排成2×2列联表，注意1和0的位置必须如下表。若只变动x或只变动y的0/1位置，计算出来的phi相关系数会正负号相反。若同时变动x和y的0/1位置，则计算出来的phi相关系数相同。phi相关系数的基本概念是：两个二元变数的观察值若大多落在2×2列联表的“主对角线”（英语：diagonal：左上-右下线）栏位，亦即若观察值大多为(x,y)=(1,1),(0,0)这两种组合，那么这两个变数呈正相关。反之，若两个二元变数的观察值大多落在“非对角线”（英语：off-diagonal：主对角线以外的位置）栏位，对应于2×2列联表，亦即若观察值大多为(x,y)=(0,1),(1,0)这两种组合，则这两个变数呈负相关。例如，我们从两个随机二元变数(x,y)抽样得出这样的2×2列联表：

||y=1|y=0|总计|
|---|---|---|---|
|**x=1**|n<sub>11</sub>|n<sub>10</sub>|n<sub>1·</sub>|
|**x=0**|n<sub>01</sub>|n<sub>00</sub>|n<sub>0·</sub>|
|**总计**|n<sub>·1</sub>|n<sub>·0</sub>|n|

其中n<sub>11</sub>, n<sub>10</sub>, n<sub>01</sub>, n<sub>00</sub>都是非负数的栏位记次值，它们加总为n，亦即观察值的个数。由上面的表格可以得出x和y的phi相关系数如下：

\phi = (n<sub>11</sub>n<sub>00</sub> - n<sub>10</sub>n<sub>01</sub>) / Math.sqrt(n<sub>1·</sub>n<sub>0·</sub>n<sub>·0</sub>n<sub>·1</sub>)

假如说，我们有下面100条数据，是关于性别与使用左手还是右手的记录，我们应该怎样得到上面这样一个表格呢？

```js
var log = {
    {"sex": "male", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "female", "hand": "left"},
    {"sex": "male", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "male", "hand": "left"},
    {"sex": "male", "hand": "right"},
    {"sex": "female", "hand": "left"},
    {"sex": "male", "hand": "right"},
    {"sex": "male", "hand": "left"},
    {"sex": "male", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "male", "hand": "left"},
    {"sex": "female", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "male", "hand": "left"},
    {"sex": "female", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "male", "hand": "left"},
    {"sex": "male", "hand": "right"},
    {"sex": "female", "hand": "left"},    
    {"sex": "male", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "male", "hand": "left"},
    {"sex": "male", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "male", "hand": "left"},
    {"sex": "female", "hand": "right"},
    {"sex": "female", "hand": "left"},
    {"sex": "male", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "male", "hand": "left"},
    {"sex": "male", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "male", "hand": "left"},
    {"sex": "male", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "male", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "female", "hand": "right"},
    {"sex": "male", "hand": "right"},
}
```

通过手工计数，我们得到下表：

||男=0|女=1|总计|
|---|---|---|---|
|右=0|43|44|87|
|左=1|9|4|13|
|总计|52|48|100|

根据上表，00位置代表“男性、右手”，01代表“男性、左手”，10代表“女性、右手”、11代表“女性、左手”。

将位置00、01、10、11的数值与一维数组table中的值对应，可以有两种看待的方式：

第一种：如果将00、01、10、11视为二进制数的话，那么他们代表的就分别是0、1、2、3（即右侧第一位的1计数为1、右侧第二位上的1计数为2，两者相加得到对应于一维数组中的index），那么分别于一维数组对应，就对应着table[0]、table[1]、table[2]、table[3]。

那么phi的计算方式应当如下：

```js
function phi(table){
    return (table[3]*table[0] - table[2]*table[1])/Math.sqrt((table[2] + table[3]) *
                (table[0] + table[1]) *
                (table[1] + table[3]) *
                (table[0] + table[2]));
}
```

另外，要用程序的方式得到原本我们手工计数的那张表格，我们要对数据进行遍历：

```js
var table = [0, 0, 0, 0];

log.forEach(function(item){
    var index = 0;
    if(item["sex"] == "female"){
        index += 1; //如果为女，相当于列联表的右侧第一位为1
    }
    if(item["hand"] == "left"){
        index += 2 //如果为左手，相当于列联表的左侧第一位为1
    }
    table[index] += 1; //每次循环，table相应的位置的值计数加1
});

console.log(table); //[43, 44, 9, 4]
```


```js
//然后将得到的table代入上面的phi函数中即可得到结果
console.log(phi(table)); //-0.133319729973268
```

第二种：如果依然将00、01、10、11视为网格的坐标的话，那么也很简单。将其转化为一维数组，只需要通过 x + y \* width 这个公式就可以得到相应位置的值（表格width为2）：00位置对应 table[0 \* 2 + 0]、01位置对应 table[0\*2 + 1]、10位置对应[1 \* 2 + 0]、11位置对应的是table[1\*2 + 1]，那么这时候00、01、10、11分别对应的也是table[0]、table[1]、table[2]、table[3]，与上面的一种方式得到的是同一个数组。注意，此时的00、01、10、11一定要搞清楚哪个是x、哪个是y。这时候其实前面一个数值对应的是y的值；而后面一个对应的是x的值。后续算法与上一中算法也是相同的。


