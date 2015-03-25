---
layout: post
title: 妙味课堂——JavaScript基础课程笔记
category: study
tags:
- js
- 妙味课堂
- 前端基础
- 学习笔记
---

集中时间把秒微课堂JS的基础课程上完，并且认真完成了课后练习。感觉在JS方面的技能算是入了个门了。课后练习的作业完成的代码我都汇总在了[这里](http://fantaghiro.github.io/miaov/)。至于视频课的学习笔记，则记录如下。

- 目录
{:toc}


#JS入门基础_热身课程

##写JS的步骤
1. 先实现布局
2. 想出实现原理
3. 了解JS语法

##希望把某个元素移除的实现
- display: none; 显示为无
- visibility: hidden; 隐藏
- width \ height
- 透明度
- left \ top
- 拿与背景色相同的div盖住该元素
- 利用margin值
- ……

##获取元素

- getElementById() ——静态方法，前面只能跟document
- document.body、document.title 页面中只有一个的元素
- getElementsByTagName() ——动态方法，前面可以跟document也可以跟其他元素，返回的是一个类似数组的元素的集合
    - 有类似数组的length
    - 有类似数组的应用方式，比如ali[0]
    - 在用TagName的时候，必须要加上中括号[]
    - 所谓的动态方法，是指通过js动态添加的元素，getElementsByTagName()也可以找到，但是document.getElementById是找不到的

##事件

事件：鼠标事件、键盘事件、系统事件、表单事件、自定义事件

- onclick
- onmouseover
- onmousedown
- onmouseout
- onmouseup
- onmousemove
- ……

###如何添加事件
- 元素.onmouseover

###函数

函数可以理解为命令，做一些事情，如:

function abc() { //肯定不会主动执行！
   ...
}

1. 直接调用：abc();
2. 事件调用：元素.事件 = 函数名 (oDiv.onclick = abc;)
3. ……

function(){} 匿名函数

元素.事件 = function(){}

###测试

- alert(1); 带确定按钮的警告框；alert('ok'); 'ok' 字符串
- 初学者：最好保持随时写，随时测试的习惯

###变量

- var li = document.getElementById('lis');
- var num = 123;
- var name = 'leo';

#JS的属性操作

##HTML属性操作

- 属性名
- 属性值

- 属性的读操作：获取、找到
    - 元素.属性名
- 属性的写操作：替换、修改
    - 元素.属性名 ＝ 新的值
    - 添加的话，需要用 +=

- innerHTML 读取元素内的所有HTML代码
    
字符串连接：加号

###属性读写操作的注意事项

- JS属性中不允许出现“-”，例如font-size改为fontSize
- class在js里面是保留字，在js作用class要用className
- 所有的相对路径都别拿来做判断（如img的src、还有href）
- 颜色值不要拿来做判断（因为有red、#f00、rgb(250, 0, 0)等写法
- 相对路径也不要拿来做判断
- innerHTML的值别拿来做判断
- IE6、IE7、IE8中表单元素的type更改不了，不支持，会报错；其他的都可以。
- 在有些浏览器中，直接更改float值可能不支持。在js中，可以用IE(styleFloat)和非IE(cssFloat)来区别对待。
- 不能用来做判断的东西，可以创造一个开关，利用布尔值来实现

关于兼容：

- 技术上：必须能做到掌握兼容性（兼容性问题的解决方案）
- 需求上：商量着来（提供最准确的呈现方案）

###[]中括号的使用

- 点“.”后面的值无法修改
- 中括号[]里面的值可以修改；JS中允许把"."替换成“[]”

##条件判断

- if(条件){……};
- if(条件){……} else {……};
- if(条件1){……} else if(条件2) {……} else if(条件3) {……} else {……};

##数组

- “放数据的仓库”
- 中括号[]，半角都好分隔，最后一个数据后面不要加逗号
- 数组的length属性
- 为数组最后塞东西用push(); 

#for应用

for循环的使用场景：

- 如果想要重复执行某些代码
- 每次执行的时候，有个数字在变化

for循环的执行顺序：1→234→234……

1. var i = 0;
2. i < 3; 关键步骤
3. 括号里面的所有代码
4. i++

注意下面这样一个循环：

~~~
for (var i=0; i<aLi.length; i++) {
  aLi[i].onclick = function(){
    alert(i);
  }
}
~~~

以上代码会弹出一个3，而不是一次0、1、2；这里注意，如果在for循环里面包了一个函数，函数里面用了i，那么由于作用域的关系，i不会像你想象的那样逐次增加。

##cssText文本格式化与属性操作

- oDiv.style.cssText = 'width: 200px; height: 200px;';
- cssText不会动head的style中的设置；但是会改变行间样式（注意，是替换行间样式，而非新增行间样式）

##按钮点击之后，不再重复功能的思路

1. 找按钮的麻烦，比如点击一次之后，设置oBtn.disabled = true;
2. 继续找按钮的麻烦，比如点击一次后，将按钮隐藏oBtn.style.display = 'none';
3. 将按钮添加的东西清空，然后再添加一次，先清空再生成
4. 用判断

##this指向及this应用

window是js中的”老大“

~~~
function fn1(){
    alert(this);
}
fn1();
~~~

上述代码中执行函数fn1()相当于window.fn1();因此，在函数体内弹出这个this仍然是window。

~~~
function fn1(){
    alert(this);
}
oBtn.onclick = fn1;
~~~

上述用按钮的点击事件调用的fn1函数，最终弹出来的是这个按钮，而不是window。

~~~
function fn1(){
    alert(this);
}
oBtn.onclick = function(){
    alert(this)
}
~~~

上述代码，点击按钮弹出的this仍然是oBtn这个按钮。

~~~
function fn1(){
    alert(this);
}
oBtn.onclick = function(){
    fn1();
}
~~~

上述代码，点击oBtn按钮，弹出的就不再是oBtn这个对象，而是window。

~~~
<input id="btn2" type="button" value="按钮2" onclick="alert(this)" />
~~~

上述代码是行间事件，弹出的this就是这个按钮btn2。

~~~
function fn1(){
    alert(this);
}
<input id="btn2" type="button" onclick="fn1();" value="按钮2” />
~~~

上述代码中，弹出的this就是window。

- this: 调用当前方法（函数）的那个对象

~~~
function fn1(){
    this
}

fn1(); this ＝> window

oDiv.onclick = fn1; this => oDiv

oDiv.onclick = function(){
    this => oDiv
};

oDiv.onclick = function(){
    fn1(); fn1()里面的this => window
}

<div onclick="  this  "></div> this => div

<div onclick = "  fn1();  "></div>  fn1()里面的this => window
~~~

~~~
<script>

fn1(this);
function fn1(obj){
  obj => window
}

oDiv.onclick = function(){
  this
  fn1(this);
};
function fn1(obj){ obj => oDiv }

</script>
~~~

~~~
<input type="button" value="按钮1" />
<input type="button" value="按钮2" />
<input type="button" value="按钮3" />

window.onload = function(){
  var aBtn = document.getElementsByTagName('input');
  for(var i=0; i<aBtn.length; i++) {
    aBtn[i].onclick = function(){
      this.style.background = 'yellow';
    }
  }
}
~~~

上述代码的作用与下面这段代码的作用等价，注意that的使用方法。

~~~
<input type="button" value="按钮1" />
<input type="button" value="按钮2" />
<input type="button" value="按钮3" />

window.onload = function(){
  var aBtn = document.getElementsByTagName('input');
  var that = null; 
  
  for(var i=0; i<aBtn.length; i++) {
    aBtn[i].onclick = function(){
      that = this;
      fn1();
    };
  }
  function fn1(){
    //this => window
    that.style.background = 'yellow';
  }
}
~~~

上述代码还等价于下面这段代码：

~~~
<input type="button" value="按钮1" />
<input type="button" value="按钮2" />
<input type="button" value="按钮3" />

window.onload = function(){
  var aBtn = document.getElementsByTagName('input');
  
  for(var i=0; i<a.aBtn.length; i++) {
    aBtn[i].onclick = fn1; //注意不要在fn1后面加括号
  }
  
  function fn1(){
    this.style.background = 'yellow';
  }
}
~~~

#自定义属性、索引值

##自定义属性的读写操作

~~~ js
winddow.onload = function(){
  var aBtn = document.getElementsByTagName('input');
  
  aBtn[0].abc = 123; //自定义属性
  
  // alert(aBtn[0].abc); 自定义属性的读
  // aBtn[0].abc = 456; 自定义属性的写
}
~~~

JS可以为任何HTML元素添加任意个自定义属性

##自定义属性应用

用自定义属性可以元素添加开关属性，作为控制开关。如下面这个例子：

~~~ js
window.onload = function(){
  var aLi = document.getElementsByTagName('li');
  // var onOff = true; 一个onOff只能控制一个开关。要为多个元素设置各自的开关，就要给每个元素加个onOff开关。
  
  for(var i=0; i<aLi.length; i++) {
    aLi[i].onOff = true;
    aLi[i].onclick = function(){
      if (this.onOff){
        this.style.background = 'url(img/active.png)';
        this.onOff = false;
      } else {
        this.style.background = 'url(img/normal.png)';
        this.onOff = true;
      }
    }
  }
}
~~~

##获取自身递增数字及匹配数组内容

在网页上设置三个按钮，默认值为0，每点击一次按钮，字母依次ABCD轮换。

~~~ html
<input type="button" value="0" />
<input type="button" value="0" />
<input type="button" value="0" />
~~~

~~~ js
  var aBtn = document.getElementsByTagName('input');
  var arr = ['A', 'B', 'C', 'D'];
  
  for(var i=0; i<aBtn.length; i++){
    aBtn[i].num = 0;
    aBtn[i].onclick = function(){
      this.value = arr[this.num]
      this.num++;
      if(this.num === arr.length){
        this.num = 0;
      };
    };
  };
~~~

##添加索引值、匹配数组、HTML元素

把三个按钮的value与数组里面的值依次进行匹配。

~~~ html
<input type="button" value="btn1" />
<input type="button" value="btn2" />
<input type="button" value="btn3" />
~~~

~~~js
window.onload = function(){
  var aBtn = document.getElementsByTagName('input');
  var arr = ['莫涛','张森','杜鹏'];
  
  for(var i=0; i<aBtn.length; i++){
    aBtn[i].index = i; //自定义属性index，添加索引值
    aBtn[i].onclick = function(){
      //alert(i); //不会弹出1、2，直接弹出3，也就是aBtn的长度。也就是说，在基础阶段，在for循环所包的函数里面再用i是不靠谱的。
      this.value = arr[this.index];
    };
  };
}
~~~

上面是通过索引值匹配数组值，匹配HTML中的元素也是同理。

想建立”匹配“、”对应“关系，就用索引值。

#数据类型、类型转换

**ECMAScript：**标准、核心

##数据类型

- HTML标签类型：
    - block
    - inline
    - inline-block
    - table
    - ……
- JS中的数据类型：
    - 数字（NaN属于数字类型）
    - 字符串
    - 布尔值
    - 函数类型
    - 对象
        - obj
        - []
        - {}
        - null （空是不能添加自定义属性的）
    - 未定义 undefined

typeof用来判断数据类型。

字符串方法charAt()：通过字符串的下标获取子字符串。

对象可以添加自定义属性。如果把函数扔给了对象，就给该对象添加了一个方法。

##JS数据类型转换

把字符串转成数字的方法：

###JS方法：Number();

~~~ js
var a = '100';
alert(a + 100); //'100100'

var b = '00100';
alert(Number(b)); //100

var c = '+100';
alert(Number(c)); //100

var d = '';
alert(Number(d)); //0

var e = '   ';
alert(Number(e)); //0

var f = true;
alert(Number(f)); //1

var g = false;
alert(Number(g)); //0

var i = [];
alert(Number(i)); //0 空数组用Number转出来是0

var j = [''];
alert(Number(j)); //0

var k = [123];
alert(Number(k)); //123

var l = ['123'];
alert(Number(l)); //123

var o = null;
alert(Number(o)); //0

----------------------------
var m = [1,2,3];
alert(Number(m)); //NaN

var json = {abc:123};
alert(Number(json)); //NaN

var json2 = {};
alert(Number(json2)); //NaN 即使是空json，Number方法也转不了

var h = function(){};
alert(Number(h)); //NaN

var p;
alert(Number(p)); //undefined 

var q = '100px';
alert(Number(q)); // NaN
~~~

###parseInt与parseFloat

~~~ js
var a = '100px';
alert(parseInt(a)); //100

var b = '100px123456789';
alert(parseInt(b)); //100

var d = '-100px';
alert(parseInt(d)); //-100 parseInt还是认加减号的

var e = '   100px';
alert(parseInt(e)); //100 parseInt也是认空格的

var f = '000000100px';
alert(parseInt(f)); //100

var g = '12.34元';
alert(parseInt(g)); //12 parseInt只能转出整数
------------------------------
var c = true;
alert(parseInt(c)); //NaN

//parseInt也不能用于转函数等

~~~

parseInt()方法还有一个参数，就是按照几进制来转，比如parseInt(a, 10);表示按照十进制来转；parseInt(b, 2);表示按照二进制来转。

~~~ js
var a = '12.34元';
alert(parseFloat(a)); //12.34

var b = '12.3.4元';
alert(parseFloat(b)); //12.3 parseFloat只认第一个小数点
~~~
**parseInt和parseFloat的配合使用**，可以来判断某个值是整数还是小数，如下：

~~~ js
var num = '200.345';
if(parseInt(num) == parseFloat(num)) {
  alert(num + '是整数');
} else {
  alert(num + '是小数');
}
~~~

##JS中稀奇古怪的隐式类型转换

显式类型转换（强制类型转换）：

- Number();
- parseInt();
- parseFloat();

隐式类型转换：

- \- \* \/ \% 减、乘、除、取模可以将字符串转成数字
- \+ 加号可以将数字转成字符串
- \+\+ \-\- 加加、减减运算符可以把字符串转成数字
- &lt; &gt; 大于号、小于号可以把字符串转成数字，一定要注意是进行数字的比较还是字符串的比较
- ! 取反 把右边的数据类型转成布尔值
- ==

~~~ js
alert('200' - 3); //197
alert(200 + '3'); //2003

var a = '10';
a++;
alert(a); //11

alert('10'>9); //true
alert('1000000'>'9'); //false
//注意：数字的比较和字符串的比较不同；字符串的比较是一位一位的比较。

alert(!'ok'); //false
alert(!100); //false

alert('2' == 2); //true
alert('2' === 2); //false 三个等号不仅判断值，还会先判断两者的类型
~~~

隐式类型转换转不出来，也会返回一个NaN，例如：alert('......' - 9);就会弹出NaN。

##isNaN应用实例

NaN: (not a number)。Nan是个不是数字的数字类型。所有的数字都是数字类型，但不是所有的数字类型都是数字。

- NaN是个数字类型，但它不是个数字。
- 一旦写程序中出现了NaN，肯定说明进行了非法的运算操作。
- NaN是个false。
- NaN与自己都不相等。

~~~ js
var a = Number('abc');
//alert(a); //NaN
//alert(typeof(a)); //number

if(a) { //会弹出‘假’，说明NaN是false
  alert('真');
} else {
  alert('假');
}

//alert(a === a); //false NaN比较，比出false
~~~

**isNaN：**is not a Number 是不是不是个数字（不是数字）。

isNaN();是个方法，用来干活的。

- 帮助判断某些值是不是数字。
- 不喜欢数字、讨厌数字(不是讨厌数字类型，isNaN遇到NaN就很喜欢，会返回true，但是NaN就是个数字类型) 用来判断数字。如alert(isNaN(2)); 返回false。alert(isNaN('我爱你')); 返回true。alert(isNaN(function(){})); 返回true。

isNaN的判断过程，将括号里面的东西扔给Number，Number转出来数字，就返回false；转不出来就返回true。

~~~ js
alert(isNaN('250'));
//Number() '250' => 250 => false

alert(isNaN(true));
//Number() true => 1 => false

alert(isNaN([]));
//Number() [] => 0 => false
~~~

下面是一个isNaN的小应用：

~~~ html
<input type="text" />
<input type="button" value="判断输入值是不是数字" />
~~~

~~~ js
window.onload = function(){
  var aInp = document.getElementsByTagName('input');
  var str = '';
  
  aInp[1].onclick = function(){
    str = aInp[0].value
    //alert(type of str); //总是返回string 从HTML中拿到的内容，类型都是字符串
    
    if(isNaN(str)){
      alert(str + '不是数字');
    } else {
      alert(str + '是数字');
    }
  }
}
~~~

#函数传参

参数 ＝ JS的数据类型：

- 数字
- 字符串
- 布尔值
- 函数
- 对象
- 未定义

###参数类型判断

~~~ js 
fn1(100);
fn1('miaov');
fn1(function(){alert(1);});

function fn1(a){
  if(typeof a === 'number' && a === a) {
    alert(a+20);
  } else if (typeof a === 'string'){
    alert(a.charAt(2));
  } else if (typeof a === 'function'){
    a();
  }
}
~~~

##重用代码步骤##

1. 尽量保证HTML代码结构一致，可以通过父级选取子元素
2. 把核心的主程序实现，用函数包起来
3. 把每组里不同的值找出来，通过传参实现 

#JS作用域

**什么是作用域**

- 域：空间、范围、区域
- 作用：读、写

##浏览器的“JS解析器”

“JS解析器”：浏览器中专门用来读JS的程序。它至少做下面两件事（当然还有其他事情）：

1. 准备工作（“找一些东西”）：根据var、function、参数找东西 —— **JS的预解析**
    
    a = 未定义
    所有的变量，在正式运行代码之前，都提前赋了一个值：未定义
    fn1 = function fn1(){alert(2);}
    所有的函数，在正式运行代码之前，都是整个函数块
    
    遇到重名的，只留一个
2. 逐行解读代码
    每读一行，就会回到预解析的库里面去看一眼。
    碰上表达式（带有 = + - * / % ++ -- ! 参数……都是表达式）能够改变值的是表达式。碰上表达式，就到库里面去修改值。

~~~ js
alert(a); //未定义
var a=1; //在库里面a的值由未定义换成1
function fn1(){alert(2);}
~~~

~~~ js
alert(a); //弹出：function a(){alert(4);}
var a=1; //预解析中的a改为了1
alert(a);  //弹出1
function a(){alert(2);}//函数声明，没有改变a的值。什么也没发生。
alert(a); //继续弹出1，因为a在预处理库里面的值没有被改过。
var a=3; //预处理中a的值变为3
alert(a); //弹出3
function a(){alert(4);} //函数声明，什么也没有发生
alert(a); //继续弹出3
a(); //报错 a is not a function
~~~

以上代码在预解析中的过程如下：

1）预解析： var function 参数 ……
    读到 var a = 1 => a 未定义
    读到 function a(){alert(2);} => a = functiona(){alert(2);} 
    变量与函数重名了，就只留下函数：
    a = function(){alert(2);}
    读到 var a = 3 => a 未定义，这里与上面名为a的函数重名了，所以还是保留a = function(){alert(2);}
    读到function a(){alert(4);} => a = function a(){alert(4);} 与前面的 a = function(){alert(2);}重名，根据上下文，后面的函数覆盖了前面的函数，所以预解析就只留下了 a = function(){alert(4);}
2）逐行解读代码
    读到表达式，表达式可以修改预解析的值。参数也可以改变预解析的值。
    遇到函数调用，又要做两件事：预解析、逐行解析代码
    函数声明，不是表达式，不改变预解析里面的值。

##作用域

- 在&lt;script&gt;标签里面声明的函数和变量，都是全局函数和全局变量（但是js解析器要把一块的事情处理完，然后处理另外一块事情）**自上而下**
- 函数：函数也是个域，也是先找后执行。**由里到外**
- 对象 {}

**作用域链**：从子级作用域跳到父级作用域的过程

~~~ html
<script>
alert(a); //报错：a is not defined。因为在预解析里面压根就没有a这个东西
</script>

...

<script>
var a = 1;
</script>
~~~

~~~ html
<script>
alert(a); //不报错，会弹出undefined。因为预解析里面有a这个东西，但是由于执行的时候，还没有改变a的值，因此a的值为undefined
var a = 1;
</script>

...

<script>
</script>
~~~

~~~ html
<script>
var a = 1; //预解析里面存了a，并且a的值存为1
</script>

...

<script>
alert(a); //弹出1
</script>
~~~

~~~ js
var a = 1; //预处理中的全局变量a的值改为1
function fn1(){
    alert(a);
    var a = 2;
} //函数声明，什么也不做
fn1(); //遇到函数调用，开始进行预解析和逐行解读代码。在函数内，先预解析出一个局部的 a 是未定义（局部的a与全局的a一点关系都没有）；然后读代码，alert(a)弹出的是undefined；然后继续执行，遇到表达式，将局部的变量a的值改为2。这时fn1的函数执行已经完成了。
alert(a); //弹出全局变量a为1
~~~

以上代码在js解析器中的模拟如下：
 
 1）预解析 var function 参数……
    a = ...
    fn1 = function fn1(){
        alert(a);
        var a=2;
    }
2) 逐行解析代码

另外一段代码：

~~~ js
var a = 1; //预处理中的全局变量a的值改为1
function fn1(){
    alert(a);
    a = 2;
} //函数声明，什么也不做
fn1(); //遇到函数调用，开始进行预解析和逐行解读代码。在函数内，没有任何函数和变量声明，因此预解析里面没东西；然后读代码，alert(a)，在局部没有找到预解析的a，于是从子级作用域跳到父级作用域去找，找到了全局的a，所以弹出的是全局变量a的值1；然后继续执行，遇到表达式，将全局变量a的值改为2。这时fn1的函数执行已经完成了。
alert(a); //弹出全局变量a为2
~~~

~~~ js
var a = 1; //预处理中的全局变量a的值改为1
function fn1(a){ //参数本质上就是一个局部变量
    alert(a);
    a = 2;
} //函数声明，什么也不做
fn1(); //遇到函数调用，开始进行预解析和逐行解读代码。在函数内，找到参数a，因此预处理里面有个局部的a是未定义。；然后读代码，alert(a)，弹出的是局部的a为undefined；然后继续执行，遇到表达式，将局部变量a的值改为2。这时fn1的函数执行已经完成了。
alert(a); //弹出全局变量a为1
~~~

~~~ js
var a = 1; //预处理中的全局变量a的值改为1
function fn1(a){ //参数本质上就是一个局部变量
    alert(a);
    a = 2;
} //函数声明，什么也不做
fn1(a); //遇到函数调用，开始进行预解析和逐行解读代码。在函数内，找到局部参数a，因此预处理里面有个局部的a是未定义。；然后读代码，读到第一行function fn1(a)，这时有参数进来，把全局的a的值1赋给了局部变量a，这时局部变量a的值变为1，alert(a)，弹出的是局部的a为1；然后继续执行，遇到表达式，将局部变量a的值改为2。这时fn1的函数执行已经完成了。
alert(a); //弹出全局变量a为1
~~~

##想要获取函数内的值

- 方法一、把全局变量用到函数里面。因为函数可以读写全局变量。见下面的代码：

~~~ js
var str = '';
function fn1(){
    var a = '大鸡腿~';
    str = a;
}
fn1();
~~~

- 方法二，在函数里面调用全局函数，通过传参实现，见下面代码：

~~~ js
function fn2(){
    var a = '99999999克拉钻石';
    fn3(a);
}
fn2();
function fn3(a){ //注意这个a是fn3里面的，与fn2里面的a毫无关系
    alert(a);
}
~~~

**注意事项**

函数的大括号是作用域；if(){}不是作用域；for(){}也不是作用域。只有作用域是先预解析、再执行。if和for的大括号没有预解析过程。

~~~ js
alert(a); //弹出undefined。这说明if大括号中的a已经在全局就被预解析了，因此if的大括号并不是作用域
if(true){
    var a=1;
}
~~~

但是，需要注意：

~~~ js
alert(fn1); //在火狐浏览器里面会报错说fn1 is not defined。但是在chrome浏览器里可以正常弹出fun1函数。

if(true){
    var a = 1;
    function fn1(){
        alert(123);
    }
}
~~~

只有火狐浏览器预解析时，不能对if或for的括号里括起来的函数进行预解析。因此存在兼容性问题。因此，如果想要定义全局函数或全局变量，尽量不要放到if和for的大括号里面，放到大括号外面。

~~~ js
for(var i=0; i<aBtn.length; i++){
    aBtn[i].onclick = function(){
        alert(i); //弹出3。因为必须for循环全部执行完成之后，aBtn才能够点击。但是for循环执行完了，外面的i已经变成3；但是在function里面又没有i，自然找到了外面的i，也就是3.
    }
}
~~~

~~~ js
for(var i=0; i<aBtn.length; i++){
    aBtn[i].onclick = function(){
        alert(i); //这时候弹出的就不是3了，是undefined
        
        for(var i=0; i<aBtn.legnth; i++){
            aBtn[i].style.background = 'yellow';
        }
    }
}
~~~

~~~ js
for(var i=0; i<aBtn.length; i++){
    aBtn[i].onclick = function(){
        alert(i); //下面for循环的括号中的var删去了，function里面又找不到i了，所以到父级找到了i，又是个3。因此，此处会弹出3。
        
        for (i = 0; i<aBtn.length; i++){
            aBtn[i].style.background = 'yellow';
        }
    }
}
~~~

#运算符

##算术

- \+ 加
- \- 减
- \* 乘
- / 除
- % 取模（求余数）

##赋值

- =
- +=
- -=
- *=
- /=
- %=

##关系

- &lt;
- &gt;
- &lt;=
- &gt;=
- ==
- !=
- ===
- !===

##逻辑

- && 与
- \|\| 或
- ! 否

##运算优先级

- 括号

#程序流程控制

##判断

- if
- switch (case break default)
- ?:

##循环

- while
- for

##跳出、跳过

- break
- continue

##什么是真，什么是假

- 真：非零的数字、字符串、true、函数、object：[] {} 能找到的元素 
- 假：零、NaN、空字符串、false、null、未定义、不能找到的元素

#函数返回值-return详解及应用

- return 返回值：函数名+括号（例如fn1())就相当于得到了该函数里面return后面的值
- 所有函数默认返回值是：undefined
- 可返回：数字、字符串、布尔、函数、对象（元素、[]、{}、null）、未定义
- return后面的任何代码都不执行了


~~~ js
alert fn1();
function fn1(){
    return function(){
        alert(1);
    }
}
~~~ 

此时弹出的是：function(){alert(1);}

~~~ js
alert fn1()();
function fn1(){
    return function(){
        alert(1);
    }
}
~~~ 

此时弹出的是1，也就是return的匿名函数执行的结果。

~~~ js
alert fn1()(10);
function fn1(){
    return function(a){
        alert(a);
    }
}
~~~ 

此时弹出的是10。


~~~ js
alert fn1(20)(10);
function fn1(a){
    return function(b){
        alert(a + b);
    }
}
~~~ 

此时弹出的是30。

##arguments

fn1(1, 2, 3); //实参——实际传递的参数

function fn1(a, b, c) //形参——形式上，a、b、c这些名代表1、2、3

如果不写形参，1、2、3也能够传进来，都存在arguments的肚子里。

function fn1(){
  //arguments => [1, 2, 3] —— 实参的集合（不是数组，但是类似数组，有length，也可以用下标找到其中的数据）
}

当函数参数个数无法确定的时候，用arguments：

~~~ js
alert(sum(1,2,3));
function sum(){
    var n=0;
    for(var i=0; i<arguments.length; i++){
        n += arguments[i];
    }
    return n;
}
~~~

~~~ js
var a=1;
function fn2(a){ //arguments的某个数值就相当于某个形参
    arguments[0]=3;
    alert(a); //弹出3
    var a=2;
    alert(arguments[0]); //弹出2
}
fn2(a);
alert(a); //弹出1
~~~

##currentStyle与getComputedStyle应用

- getComputedStyle获取的是计算机（浏览器）计算后的样式，但是不兼容IE6、7、8
- currentStyle方法兼容IE6、7、8，但是不兼容标准浏览器

属性判断法、版本检测法来解决浏览器间的兼容性问题
~~~ js
function getStyle( obj, attr) {
    return obj.currentStyle ? obj.currentStyle[attr]:getComputedStyle( obj )[attr];
}
~~~

**注意事项：**

- 如果用以上的方法获取某个元素的复合样式，例如background，那么就不要用上面那种方式获取，在不同浏览器间有兼容性问题。用上面的方法获得单一样式，而不要用来获取复合样式。
- 使用以上方法，注意不要多按空格
- 使用以上方法，不要获取未设置后的样式，因为浏览器间不兼容
- 在火狐4.0之前，有个bug，如果getComputedStyle后面不跟参数，会出现问题，所以有些人写成getComputedStyle(obj, false)，那个false就是为了解决这个bug。这里的bug也可以写成0，或者其他任何参数都可以。不过目前火狐的浏览器都比较高，因此这个问题已经不是很常见了。

#定时器

##setInterval

setInterval(函数, 毫秒); 重复执行（发动机）

~~~ js
var i=0;
function fn1(){
    document.title = i;
    i++;
}
setInterval(fn1, 1000);
~~~

**事件调用的方法**

- fn1(); 直接调用
- document.onclick = fn1; 事件调用
- setInterval(fn1, 1000); 函数调用

**clearInterval**

~~~ js
var timer = setInterval(函数, 毫秒); //重复执行
clearInterval(timer); //清除定时器
~~~

~~~ js
var i=0,
    timer = null;
function fn1(){
    i++;    
    document.title = i;
    
    if(i===10){
        clearInterval(timer);
    }
}
timer = setInterval(fn1, 1000);
~~~

**注意**

定时器如果是由事件控制的，比如按钮的onclick控制的，那么一定要遵循一个原则，先关后开。这样可以避免连续点击多次按钮，重复设置定时器。另外，clearInterval()不论里面填的是一个timer，还是null还是未定义，都可以顺利运行。

##setTimeout

var timer = setTimeout(函数, 毫秒); 执行一次（炸弹）

clearTimeout(timer);

##定时器的小应用（函数封装和回调函数）

###doMove的函数封装

~~~ html
<input id="btn1" type="button" value="走" />
<div id="div1"></div>
~~~

~~~ js
var oBtn1 = document.getElementById('btn1');
var oDiv = document.getElementById('div1');

oBtn1.onclick = function () {
	
	doMove ( oDiv, 'left', 12, 900, function () {
		doMove ( oDiv, 'top', 34, 500 );
	});

};

//doMove函数封装

function doMove ( obj, attr, dir, target, endFn ) {
	
	dir = parseInt(getStyle( obj, attr )) < target ? dir : -dir;
	
	clearInterval( obj.timer );
	
	obj.timer = setInterval(function () {
		
		var speed = parseInt(getStyle( obj, attr )) + dir;			// 步长
		
		if ( speed > target && dir > 0 ||  speed < target && dir < 0  ) {
			speed = target;
		}
		
		obj.style[attr] = speed + 'px';
		
		if ( speed == target ) {
			clearInterval( obj.timer );
			
			/*
			if ( endFn ) {
				endFn();
			}
			*/
			endFn && endFn();
		}
		
	}, 30);
}

function getStyle ( obj, attr ) { 
    return obj.currentStyle?obj.currentStyle[attr] : getComputedStyle( obj )[attr]; 
}
~~~

###抖动的函数封装

~~~ html
<img id="img1" src="img/4.jpg" />
<img id="img2" src="img/5.jpg" />
~~~

~~~ js
window.onload = function () {
	var oImg1 = document.getElementById('img1');
	var oImg2 = document.getElementById('img2');
	
	oImg1.onclick = fnShake;
	oImg2.onclick = fnShake;
	
	function fnShake() {
		var _this = this;
		shake( _this, 'left', function(){
			shake( _this, 'top' );
		});
	}

};

function shake ( obj, attr, endFn ) {
	var pos = parseInt( getStyle(obj, attr) ); //有隐患 需要解决
	var arr = [];			// 20, -20, 18, -18 ..... 0
	var num = 0;
	var timer = null;
		
	for ( var i=20; i>0; i-=2 ) {
		arr.push( i, -i );
	}
	arr.push(0);
		
	clearInterval( obj.shake );
	obj.shake = setInterval(function (){
		obj.style[attr] = pos + arr[num] + 'px';
		num++;
		if ( num === arr.length ) {
			clearInterval( obj.shake );
			endFn && endFn();
		}
	}, 50);
}
~~~

# 系统时间对象

new Date(); //当前 系统的时间 对象

~~~ js
var myTime = new Date(); //myTime的类型是object
var iYear = myTime.getFullYear(); //获得年份
~~~

相关方法（以下得到的均为数字类型）：

- getFullYear()
- getMonth()
- getDate()
- getDay()
- getHours()
- getMinutes()
- getSeconds()

注意事项：

- 用getMonth()得到的月份，一月是从0开始计算的。因此，例如当前为5月份，则用getMonth()得到的是4。
- 用getDay()获得的星期几，得到的是一个数值。如果当前时间是星期天，则得到数字0。

##Date对象参数

- 数字形式：new Date(2013, 4 , 1 , 9 , 48 , 12); //年月日时分秒，注意月是从0开始算的。

~~~ js
var iNow = new Date();
var iNew = new Date(2014, 10, 26, 21, 56, 0);
var t = Math.floor((iNew - iNow)/1000); 
var str = Math.floor(t/86400) + '天' +  Math.floor(t%86400/3600) + '时' + Math.floor(t%86400%3600/60) + '分' +  t%60 + '秒';
~~~

- 天：Math.floor(t/86400)
- 时：Math.floor(t%86400/3600)
- 分：Math.floor(t%86400%3600/60)
- 秒：t%60


- 字符串形式：new Date('June 10, 2013 12:12:12');

~~~ js
var iNow = new Date();
var iNew = new Date('November 10, 2013 21:56:0');
var t = Math.floor((iNew - iNow)/1000); 
var str = Math.floor(t/86400) + '天' +  Math.floor(t%86400/3600) + '时' + Math.floor(t%86400%3600/60) + '分' +  t%60 + '秒';
~~~

##时间戳

getTime(); 返回从1970年1月1日0点0分0秒0毫秒到现在的毫秒数

#字符串操作

## 字符串获取类、封装检测数字的方法

- **.length** 空格也算长度
- **.charAt()** 找到子字符串。括号中什么也不写，默认找第0个。如果超过字符串长度减1，则返回空
- **.charCodeAt()** 得到指定子字符的unicode编码。括号中什么也不写，默认找到第0个字符的unicode值，括号中最小为0，最大为字符串长度减1
- **String.fromCharCode();** 根据字符编码，返回一个字符。例如String.fromCharCode(22937);返回的是“妙”字；要得到多个字符，可以用逗号将不同字符编码隔开，例如：String.fromCharCode(22937, 21916);返回的就是“妙味”两个字。0～9 => 48～57；a~z => 97~122；A~Z => 65~90

~~~ js
alert(detectNum(' 1a23d456'));
function detectNum(str){
    var n = 0;
    for(var i=0; i<str.length; i++){
        n = str.charAt(i);
        if( n < 48 || n > 57 ) {
            return false;
        }
    }
    return true;
}
~~~

## indexOf、lastIndexOf

- **.indexOf()** 返回某个字符或字符串在整个字符串中的位置 str.indexOf('m', 5)代表在str字符串中的第5位开始往后找字符m的位置。如果用indexOf()来找，找不到，则返回-1。从左往右找。如果第二个参数为负数，则默认当成0来处理。

~~~ js
var str = '妙味课堂是一支独具特色的IT培训团队，妙味反对传统IT教育枯燥乏味的教学模式，妙味提供一种全新的快乐学习方法！'；
var s = '妙味';
var i = 0;

for ( ; str.indexOf(s, i) != -1; ){
    alert(str.indexOf(s, i));
    i = str.indexOf(s, i) + s.length;
}

或

while(str.indexOf(s, i) != -1) {
    alert(str.indexOf(s, i));
    i = str.indexOf(s, i) + s.length;
}
~~~

- **.lastIndexOf()** 从右往前找，也可以带数字参数，表示从哪里开始往前找。

## 比较类、截取类

- 字符串的大小比较，比较的就是字符串第0位的字符的unicode编码

- **.substring(n, m)** 截取从第n位起，到m位结束的字符。如果没有m，就默认截取到最后一位。str.substring(2, 0);和str.substring(0, 2);的结果是一样的。substring可以检测里面两个参数的大小，如果后面的参数小于前面的参数，它就把这两个参数自动颠倒过来。如果括号里面什么参数都没有，就相当于从0位截取到最后一位，也就是整个字符串。如果参数中有负数的话，就当做0处理。
- **.slice(n, m)** str.slice(0, 2)和str.slide(2, 0)结果不一样。后者找不到结果，因为.slice()方法，不会判断里面参数的大小并交换参数位置。str.slice(-2);截取的是从最后一位截取到倒数第二位。-1代表的是最后一位字符串。str.slice(-4, -2);截取的是倒数第四位到倒数第二位的字符串。 

##大小写转换、split分割字符串

- **.toUpperCase()** 转换成大写
- **.toLowerCase()** 转换成小写
- **.split()** 将字符串分割为数组。var str = 'www.miaov.com'; str.split('.'); => ["www", "miaov", "com"]；var str1 = 'leo'; str1.split(); => ['leo']；str2 = 'leo'; str2.split(''); => ["l", "e", "o"]；var str3 = '/www.miaov.com/'; str3.split('/'); => ["", "www.miaov.com", ""]；var str4 = '2013-11-29-23-07'; str4.split('-', 3); => ["2013", "11", "29"]
 

- **.join()**方法 用来把数组中的各个东西拼到一块儿。var arr = ['aa', 'bb', 'cc]; arr.join(); => 'aa,bb,cc' .join()括号中什么也不写，默认就是用逗号隔开。arr.join(''); => 'aabbcc' ； arr.join('-'); => 'aa-bb-cc'

##字符串操作总结

~~~ js
var str = '妙味课堂-WWW.miaov.com';

str.charAt(1); //味
str.charCodeAt(1); //21619
String.fromCharCode(22937, 21619); //妙味

str.indexOf('m', 3); //9
str.lastIndexOf('o'); //16

'1000' < '2' //true
'1000' > 2 //true

str.substring(0, 4); //妙味课堂
str.slice(-3); //'com'

str.toUpperCase(); //'妙味课堂-WWW.MIAOV.COM'
str.toLowerCase(); //'妙味课堂-www.miaov.com'

str.split('.', 2); //['秒微课堂-www', 'miaov']

var arr = ['www', 'miaov', 'com'];
arr.join('.'); //'www.miaov.com'
~~~

# 数组的操作

## json数据格式及语法

~~~ js
var json = { name: 'leo', age: 32};
alert(json.name);

var imgData = { 
    url: ['img/1.png', 'img/2.png'],
    text: ['图片一', '图片二']
};
alert(imgData.url[1]);

var json2 = { 'name': 'miaov' }; //推荐的安全格式的写法
alert(json2.name);
alert(json2['name']);
json2.name = 'abc';
json2['name'] = '妙味'; //注意中括号里面要用引号

var arr = [{'name': 'TM', 'age': 23}, {'name': 'leo', 'age': 32}];
alert(arr[0].name);
~~~

## for-in循环，遍历json

~~~ js
var json4 = { 'name': 'miaov', 'age': 3, 'fun': '前端开发'};
for(var attr in json4){
    alert(attr);
    alert(json4[attr]);
}

var json5 = { 
    url: ['img/1.png', 'img/2.png'],
    text: ['图片一', '图片二']
};

for(var attr in json5) {
    for(var i=0; i<json5[attr].length; i++){
        alert(json5[attr][i]);
    }
}
~~~

for-in也可以遍历对象属性：

~~~ js
var str = '';
var num = 0;
for(var attr in window){
    str += num + '. ' + attr + ' : ' + window[attr] + '<br/>';
    num ++;
}
document.body.innerHTML = str;
~~~

数组也可以用for-in来遍历：

~~~ js
var arr = ['a', 'b', 'c'];
for(var i in arr){
    alert(arr[i]);
}
~~~

##清空数组和清空数组效率问题

~~~ js
// var arr = [1, 2, 3];
// var arr = new Array(1, 2, 3);

var arr = new Array(4);
alert(arr.length); // 4 在new Array()里面写了一个数字，就是定义了arr的长度
~~~

~~~ js
var arr = [1, 2, 3];
arr.length = 1; //数组的length属性是可写的
alert(arr);
~~~

~~~ js
var arr = [1, 2, 3];
arr.length = 0; //快速清空数组arr
或
arr = []; //通过重新赋值来清空数组，效率更高
~~~

~~~ js
var str = 'aaaaa';
str.length = 1;
alert(str); // 'aaaaa'
//字符串的length属性不可写，但是数组的length属性可写
~~~

##数组的操作

**添加**

- push方法：arr.push(); 往数组最后一位添加内容。.push()方法是有返回值的，返回的是数组新的长度
- unshift方法：arr.unshift(); 往数组的最前面添加内容，返回值为数组新的长度（IE6、7不支持unshift的返回值）

**删除**

- pop方法：arr.pop(); 删除数组的最后一个，返回值是被扔掉的值
- shift方法：arr.shift(); 删除数组的第一个，返回值是被扔掉的值

**小技巧**

~~~ js
var arr = ['TM', '钟毅', '张森', '杜鹏', 'Leo'];
arr.unshift(arr.pop()); //数组变为：['Leo', '钟毅', '张森', '杜鹏', 'TM']
或
arr.push(arr.shift()); //数组变为：['钟毅', '张森', '杜鹏', 'Leo', 'TM']
~~~

**splice方法**

- splice方法有删除、替换、添加三种功能

~~~ js
var arr = ['TM', '钟毅', '张森', '杜鹏', 'Leo'];
//删除
//arr.splice(0, 1); //删掉第0位，删1个。两个参数第一个是从第几位开始，第二个是删掉几个。splice删除的时候有返回值，返回的是被删除的内容
//替换
//arr.splice(0, 1, '莫涛'); //替换第0位，替换1个，替换为'莫涛'。返回的还是删除的东西
//添加
arr.splice(1, 0, '李贤'); //在第1位那里，删除0个，添加了一个'李贤'到了第1位，'钟毅'就变成了arr[2]了。后面也可以添加多个。如果splice删除了0个，那么就没有返回值。
~~~

###数组去重

~~~ js
var arr = [1, 2, 2, 4, 2];
for ( var i=0; i<arr.length; i++ ) {
    for ( var j = i+1; j<arr.length; j++) {
        if( arr[i]==arr[j] ){
            arr.splice( j, 1 );
            j--;
        }
    }
}
~~~

**sort排序**

~~~ js
var arr = ['c', 'd', 'a', 'e'];
arr.sort(); // 'a', 'c', 'd', 'e' 按照unicode编码排序

var arr2 = [4, 3, 5, 76, 2, 0, 8];
// arr2.sort(); // 0, 2, 3, 4, 5, 76, 8 sort默认是将数组中的每一个按照字符串来排序的，因此出现了76排在8前面的情况

// arr2. sort(function( a, b ){
    return a - b; //如果a-b返回正数，就a、b两个数字换个序。如果a-b是负数，就不换序
}) //返回数字从小到大 0, 2, 3, 4, 5, 8, 76

// arr2. sort(function( a, b ){
    return b - a;
}) //返回数字从大到小 76,, 8, 5, 4, 3, 2, 0
~~~

其他排序方法：

- 快速排序法
- 希尔排序法
- 冒泡排序法
- 归并排序法
- 选择排序法
- 插入排序法

~~~ js
var arrWidth = ['345px', '23px', '10px', '1000px'];
arrWidth.sort(function(a, b){
    return parseInt(a) - parseInt(b);
}); // ['10px', '23px', '345px', '1000px']
~~~

**随机排序**

~~~ js
var arr = [1, 2, 3, 4, 5, 6, 7, 8];
arr.sort(function(a, b){
    return Math.random(); - 0.5;
});
~~~

###随机数以及随机公式推理过程

Math.random(); 返回0~1之间随机的一个数

如果想要随机返回0和1之间的一个整数，可以用四舍五入的方法：

Math.round(Math.random()); //注意，这里不能用Math.floor

如果想要返回0~10之间的一个随机数：

Math.round(Math.random() * 10); //返回0~10之间的随机整数

返回从20~100之间的一个随机数：

Math.round( Math.random()*80 + 20 ); //返回5~10之间的随机整数

如果想要返回一个x到y之间的整数，可以写成：

Math.round( Math.random() * (y - x) + x );

返回0~x的整数，可以写成

Math.round( Math.random() * x );

返回1~x的整数，可以写成

Math.ceil( Math.random() * x ); //Math.ceil()是向上取整

**concat方法**

concat方法用于连接数组。

~~~ js
var arr1 = [1, 2, 3];
var arr2 = [4, 5, 6];
var arr3 = [7, 8, 9];

arr1.concat(arr2); //[1, 2, 3, 4, 5, 6] 新数组与原来数组没什么关系。
arr1.concat(arr2, arr3); //[1, 2, 3, 4, 5, 6, 7, 8, 9]
~~~

**reverse方法**

reverse方法是颠倒数组中的位置，会改变原数组

~~~ js
var arr1 = [1, 2, 3];
arr1.reverse();
alert(arr1); // [3, 2, 1]
~~~

~~~ js
var str = 'abcdef';
alert(str.split('').reverse().join('')); //'fedcba'
~~~










