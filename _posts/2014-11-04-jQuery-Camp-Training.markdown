---
layout: post
title: 妙味课堂——jQuery集训营笔记
category: study
tags:
- js
- jQuery
- 妙味课堂
- 前端基础
- 学习笔记
---

在进行了很长时间的自学以后，终于付费买了“妙味课堂”的远程课程。感觉妙味真是良心培训商家。现纪录jQuery集训营的笔记如下

- 目录
{:toc}

# 妙味课堂 - jQuery集训营

## 2014年10月10日第一堂课

- 什么是JQ 
    - JS的升级版，写越少的代码，做越多的事情
- 学习JQ的基础 
    - HTML CSS Javascript 后台（了解）
- JQ官网 
    - http://jquery.com/
- 如何使用JQ 
    - 官网下载jquery.js文件
    - 版本说明

###选择元素

####$() ★★★★★

####css() ★★★★★

**JQ的$()选择符和CSS()**

~~~ js
//document.getElementById('div1').style.background = 'red';
//document.getElementsByTagName('div')[0].style.background = 'red';
//document.getElementsByClassName('box')[0].style.background = 'red';
//JQ选择元素的风格跟CSS风格特别类似
//$('#div1').css('background', 'red');
//$('div').css('background', 'red);
//$('.box').css('background', 'red);
~~~

#### 省略原生的循环操作

**JQ省略循环**

~~~ html
<ul>
    <li>1111</li>
    <li>1111</li>
    <li>1111</li>
    <li>1111</li>
</ul>
~~~

~~~ js
var aLi = document.getElementsByTagName('li');
/*
for(){
    aLi[i].style...
}
*/
//$('li').css('background', 'red'); //JQ省略原生当中的循环的操作
jQuery('li').css('background', 'red'); //$ == jQuery 一个大名一个小名
~~~

####$ == jQuery

###JQ方法函数化

**JQ方法函数化**

~~~ html
<div id="div1" class="box">aaaa</div>
~~~

~~~ js
/*
var oDiv = document.getElementById('div1');
oDiv.onclick = function(){
    alert(oDiv.innerHTML);
};
*/
var oDiv = $('#div1');
oDiv.click(function(){
    alert(oDiv.html());
});
---------
//JQ源码中存在对应函数，面向对象的函数，jQuery对象下面的方法
function $(selector){
}
function click(fn){
}
function html(){
}
~~~

####事件 click()

- click() ★★★★★

####内容 html()

- html() ★★★★★

###JS与JQ的关系

- 之间不能混写
- 函数中返回原生this，$()选择元素
- 例子：选择颜色填充方块

~~~ js
var oDiv = $('#div1');
oDiv.click(function(){
    //alert(oDiv.html()); //纯JQ写法 没有问题
    //alert(document.getElementById('div1').innerHTML); //纯JS写法 没有问题
    //alert(oDiv.innerHTML); //错误写法，无法执行，因为JS和JQ混写了
    //alert(document.getElementById('div1').html()); //错误写法，无法执行，因为混写了
    //this ？ 原生还是JQ的？ //函数中返回的this都是原生的
    alert(this.innerHTML); //可以这样写
    alert($(this).html()); //也可以这样写 要获得jq对象的this，要用$()括起来
})
~~~

**例子：选择颜色填充方块**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>选择颜色填充方块</title>
    <style>
        div { width: 100px; height: 100px; border: 1px solid #000; float: left; margin: 10px; }
    </style>
    <script src="jquery-1.11.1.js"></script>
</head>
<body>
    <span>red</span>
    <span>yellow</span>
    <span>green</span>
    <span>blue</span>
    <br>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <script>
        var color = '';
        $('span').click(function(){
            color = $(this).html()
        });
        $('div').click(function(){
            $(this).css('background', color);
        });
    </script>
</body>
</html>
~~~

###取值与赋值的关系

- 通过参数决定

**取值与赋值的关系**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>取值与赋值的关系</title>
    <script src="jquery-1.11.1.js"></script>
</head>
<body>
    <div id="div1" class="box">aaaaa</div>
    <script>
        // oDiv.innerHTML; //获取
        // oDiv.innerHTML = 'bbbbb'; //赋值
        //$('#div1').html(); //获取
        //$('#div1').html('bbbbbb'); //赋值
        $('#div1').css('color', 'red'); //赋值
        alert($('#div1').css('color')); //获取div的color属性的属性值
    </script>
</body>
</html>
~~~

####属性 attr()

- attr() ★★★★★

####值 val()

- val() ★★★

**attr()和val()**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>取值与赋值的关系</title>
    <script src="jquery-1.11.1.js"></script>
</head>
<body>
    <div id="div1" class="box" miaov="miaov">aaaaa</div>
    <input type="text" value="123">
    <input type="text" value="456">
    <script>
        //操作属性attr()
        $('#div1').attr('class', 'box2'); //用attr改class属性
        $('#div1').attr('title', 'hello'); //添加原本没有的属性
        alert($('#div1').attr('class')); //获取属性值
        alert($('#div1').attr('miaov')); //也可以获取自定义的属性
        //val()
        //alert($('input').val()); //获取
        //$('input').val('7777'); //针对多个input的value值进行设置
        alert($('input').val()); // 针对集合进行获取操作，只获取第一个
    </script>
</body>
</html>
~~~

####多元素取值

- 第一个元素

###强大的$()

####加载

- $(function(){}); ★★★★★

####属性选择

- [=] ★★★★★
- [^=] 以……起始 ★★★★★
- [$=] 以……结束 ★★★★★
- [*=] 包含……的 ★★★★★
- 引号的问题

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>加载和通配符选择</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //$('input[value]').css('background', 'red'); //input有value属性的才背景变红
            //$('input[value=123]').css('background', 'red'); //value必须等于123的input才背景变红
            //$('input[value^=123]').css('background', 'red'); //value以123为起始的input元素
            //$('input[value$=444]').css('background', 'red'); //value以123为结束的input元素
            //$('input[value*=3]').css('background', 'red'); //value中有3的input元素
            $('div[class="box box2"]).css('color', 'red'); //这种情况下，box box2必须要用引号引起来
        });
    </script>
</head>
<body>
    <div id="div1" class="box box2" miaov="妙味">aaaaaa</div>
    <input type="text" value="123_444">
    <input type="text" value="123_555">
    <input type="text" value="777_888">
</body>
</html>
~~~

**用$(function(){});来加载**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>加载</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        /*
        window.onload = function(){
        };
        */
        $(function(){
        });
    </script>
</head>
<body>
    ...
</body>
</html>
~~~

###JQ的链式操作

- $().css().html().click()
- 针对设置的时候

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>链式操作</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            /*
            var oDiv = $('#div1');
            oDiv.html('bbbbb');
            oDiv.css('color', 'red');
            oDiv.click(function(){
                alert(123);
            });
            */
            $('#div1').html('bbbbb').css('color', 'red').click(function(){alert(123)});
        })
    </script>
</head>
<body>
    <div id="div1">aaaaaaa</div>
</body>
</html>
~~~

###JQ实战小技巧

- 命名的规范 
    - $div $span
- 容错处理 
    - $()

**命名规范**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>链式操作</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            var $div = $('#div1');
            var oSpan = document.getElementById('span1');
            $div.html('bbbbb');
            $div.css('color', 'red');
            $div.click(function(){
                alert(123);
            });
        })
    </script>
</head>
<body>
    <div id="div1">aaaaaaa</div>
</body>
</html>
~~~

**容错处理**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>容错处理</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //var oSpan = document.getElementById('span1');
            //oSpan.innerHTML = 'bbbbb'; //这个oSpan在页面中不存在，原生的js会报错
            var $span = $('#span1'); //这个span并不存在
            $span.html('bbbbb'); //但是如果用JQ写就不会报错
        })
    </script>
</head>
<body>
    <div id="div1">aaaaaaa</div>
</body>
</html>
~~~

###集合的长度

####size() ★

####length ★★★★★

- $()获取到的都是一个集合

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>集合的长度</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //alert($('div').size()); //3 用size()获取集合的长度
            //alert($('div').length); //3 注意没有括号，获得集合的长度
            alert($('#div1').length); //1 用$()获取到的都是元素的集合
        })
    </script>
</head>
<body>
    <div id="div1" class="box box2" miaov="妙味">aaaaaaa</div>
    <div></div>
    <div></div>
</body>
</html>
~~~

###JQ实战小技巧

- 利用length判断元素是否存在
- 例子：删除指定颜色的方块

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>通过length来纠错，发现页面中没有的元素</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            var $span = $('#span1'); //这个span并不存在
            console.log($span.length); //0 说明页面中没有$span这个元素
            $span.html('bbbbb'); 
        })
    </script>
</head>
<body>
    <div id="div1">aaaaaaa</div>
</body>
</html>
~~~

**删除指定颜色方块的背景颜色**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>删除指定颜色的方块</title>
    <style>
        div { width: 100px; height: 100px; border: 1px solid #000; float: left; margin: 10px; }
    </style>
    <script src="jquery-1.11.1.js"></script>
</head>
<body>
    <span>red</span>
    <span>yellow</span>
    <span>green</span>
    <span>blue</span>
    <br>
    <input type="button" value="清空红色">
    <br>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <script>
        var color = '';
        $('span').click(function(){
            color = $(this).html();
        });
        $('div').click(function(){
            $(this).css('background', color);
        });
        $('input').click(function(){
            $('div[style*=red]').css('background', '');
        });
    </script>
</body>
</html>
~~~

###class的操作

####addClass() ★★★

####removeClass() ★★★

####toggleClass() ★★★

**class操作**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>class的操作</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            $('#div1').addClass('box2 box4'); //添加多个class，可以用空格隔开；重复的class不会添加进去（JQ自动去重了）
            $('#div1').removeClass('box2 box4'); //找到的class会被删掉，没有找到的class被JQ自动忽略了
            $('#div1').toggleClass('box3'); //如果没有该class，就自动加上；如果有了，就自动删去
        })
    </script>
</head>
<body>
    <div id="div1" class="box box2" miaov="妙味">aaaaaa</div>
</body>
</html>
~~~

###显示隐藏

####show() / hide() ★★★★★

- 与CSS()的区别
- 例子：点击弹出菜单（1）

**show()、hide()方法**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>class的操作</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            var bBtn = true;
            $('input').click(function(){
                if(bBtn){
                    $('div').hide();
                } else {
                    $('div').show();
                }
                bBtn = !bBtn;
            });
        })
    </script>
</head>
<body>
    <input type="button" value="点击">
    <div>div</div>
</body>
</html>
~~~

**show()、hide()方法与css()的区别**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>class的操作</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            var bBtn = true;
            $('input').click(function(){
                if(bBtn){
                    //$('div').hide();
                    $('span').css('display', 'none');
                } else {
                    //$('div').show();
                    $('span').css('display', 'block'); //这里会出现问题，面对行内元素，应将block改为inline。但是如果用show()和hide()，则不需要进行这方面的相应更改
                }
                bBtn = !bBtn;
            });
        })
    </script>
</head>
<body>
    <input type="button" value="点击">
    <br>
    <span>span</span>
    <span>span</span>
    <span>span</span>
</body>
</html>
~~~

**点击弹出菜单**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>点击弹出菜单</title>
    <style>
        ul { display: none; }
        .box { display: block; }
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            $('input').click(function(){
                $('ul').toggleClass('box');
            });
        })
    </script>
</head>
<body>
    <input type="button" value="点击">
    <ul>
        <li>1111</li>
        <li>2222</li>
        <li>3333</li>
        <li>4444</li>
    </ul>
</body>
</html>
~~~

###节点的选择

####prev() next() ★★★★★

####prevAll() nextAll() ★★★

####siblings() ★★★

- 参数的筛选功能

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>节点的选择</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //$('span').next().css('background', 'red'); //p, h1
            //$('span').prev().css('background', 'red'); //div, p
            //$('p').nextAll().css('background', 'red'); //p标签下面的所有标签
            //$('p').prevAll().css('background', 'red'); //p标签之前的所有标签
            //$('p').siblings().css('background', 'red'); //找p标签所有的兄弟节点
            //参数筛选功能
            //$('p').siblings('h2').css('background', 'red'); //找p标签所有的兄弟节点中的h2节点
            //$('span').next('h1').css('background', 'red'); 
            //$('span').next('h2').css('background', 'red'); //两个span的下一个都没有h2的，所以就没有
        });
    </script>
</head>
<body>
    <div>div</div>
    <span>span</span>
    <p>p</p>
    <span>span</span>
    <h1>h1</h1>
    <h2>h2</h2>
    <h2>h2</h2>
    <h3>h3</h3>
    <em>em</em>
</body>
</html>
~~~

###JQ实战小技巧

- 利用参数修复查找节点问题
- 例子：点击弹出菜单（2）

**点击弹出菜单（2）**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>点击弹出菜单</title>
    <style>
        ul { display: none; }
        .box { display: block; }
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            $('input[type=button]').click(function(){
                //$(this).next().toggleClass('box');
                $(this).nextAll('ul').toggleClass('box');
            });
        })
    </script>
</head>
<body>
    <input type="button" value="点击">
    <input type="hidden">
    <ul>
        <li>1111</li>
        <li>2222</li>
        <li>3333</li>
        <li>4444</li>
    </ul>
</body>
</html>
~~~

###下标

####eq() ★★★★★

**eq()的操作**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>下标eq()的操作</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            $('li').eq(1).css('background', 'red'); 
        })
    </script>
</head>
<body>
    <ul>
        <li>1111</li>
        <li>2222</li>
        <li>3333</li>
        <li>4444</li>
    </ul>
</body>
</html>
~~~

- 本课练习 
    - 抽奖效果

##2014年10月12日第二堂课

###节点的选择

####first() ★★★

####last() ★★★

####slice() ★

####children() ★★★

####find() ★★★★★

- children和find区别

**节点的选择**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>节点的选择</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        // eq(0) == first();
        $(function(){
            // $('li').first().css('background', 'red'); //选择第一个
            // $('li').last().css('background', 'red'); //选择最后一个
            // $('li').slice(1, 3).css('background', 'red'); //得到的其实是从eq(1)开始到eq(2)结束
            // $('li').slice(1).css('background', 'red'); //如果在slice里面只写起始位置不写结束位置，那么就是从起始位置开始，一直到最后一个元素
            //$('ul').children().css('background', 'red'); //找到ul的所有子节点，但是孙子节点是找不到的
            // $('ul').children('div').css('background', 'red'); //children()可以过滤筛选
            // $('ul').find('p').css('background', 'red'); //可以用find找ul之下的所有节点中匹配的节点，find查找的范围比children更加广泛
        })
    </script>
</head>
<body>
    <ul>
        <li>
            1111
            <p>pppp</p>
        </li>
        <li>1111</li>
        <li>1111</li>
        <li>1111</li>
        <div>div</div>
    </ul>
</body>
</html>
~~~

###JQ实战小技巧

- 避免复杂的选择器操作，而采用find操作

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>节点的选择</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            // $('ul p').css('background', 'red');
            $('ul').find('p').css('background', 'red'); //用下面这种find的方式性能会更高一些
        })
    </script>
</head>
<body>
    <ul>
        <li>
            1111
            <p>pppp</p>
        </li>
        <li>1111</li>
        <li>1111</li>
        <li>1111</li>
        <div>div</div>
    </ul>
</body>
</html>
~~~

###节点的选择

####parent() ★★★

####parents() ★

####closest() ★★★★★

- 精准的查找能力，实战开发之王
- 找的是最近的唯一一个元素
- 例子：点击查找指定节点

**parent()和parents()**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>节点的选择</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            // $('#div2').parent().css('border', '1px solid red'); //parent()找父级
            //parents() 获取当前元素的所有祖先节点
            // $('#div2').parents().css('border', '1px solid red'); //div1, body, html都加上了边框
            // $('#div2').parents('body').css('border', '1px solid red'); //parents()也有筛选的功能
        })
    </script>
</head>
<body>
    <div id="div1">aaa
        <div id="div2">bbb</div>
    </div>
</body>
</html>
~~~

**closest()**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>节点的选择</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
    //closest()：找指定的一个最近的祖先元素（包括自身）（该函数必须加参数）；它只能选择到一个唯一的元素
        $(function(){
            // $('#div2').closest().css('border', '1px solid red'); //这样写不对，因为closest函数没有参数
            $('#div2').closest('.box').css('border', '1px solid red'); //只加在了div1上
            //如果给div2添加上class为box，那么上面的语句找到的就是div2了
        })
    </script>
</head>
<body class="box">
    <div id="div1" class="box">aaa
        <div id="div2">bbb</div>
    </div>
</body>
</html>
~~~

**点击查找指定节点**

~~~
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>节点的选择</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //点击span，让其对应的li变红
            $('span').click(function(){
                $(this).closest('li').css('background', 'red');
            });
        })
    </script>
</head>
<body>
    <ul>
        <li><div>aaa <span>span</span><div></li>
        <li><div>aaa <span>span</span><div></li>
        <li><div>aaa <span>span</span><div></li>
        <li><div>aaa <span>span</span><div></li>
    </ul>
</body>
</html>
~~~

###节点的操作

####创建节点

- $(<>) ★★★★★
- 比原生JS更强大的创建方式

####添加节点

- insertBefore() before() ★★★★★
- insertAfter() after() ★★★★★
- appendTo() append() ★★★★★
- prependTo() prepend() ★★★★★
- 两种写法的区别

**创建节点**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>节点的操作</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            // document.createElement('div');
            // $('<div>'); //这样就创建了一个div标签
            /*
            var oDiv = document.createElemenet('div');
            oDiv.innerHTML = 'hello';
            oDiv.id = 'div1';
            */
            // $('<div id="div1">hello</div>'); //直接创建了一个具备多种设置的div标签
        })
    </script>
</head>
<body>  
</body>
</html>
~~~

**append()、prepend()、before()、after()**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>节点的操作</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //append()：把元素添加到指定的节点的里面的最后
            var $li = $('<li>hello</li>');
            // $('ul').append($li);
            //prepend()：把元素添加到指定的节点的里面的最前面  
            // $('ul').prepend($li);
            //before()：把元素添加到指定的节点的前面
            // $('ul').before($li);
            //after()：把元素添加到指定的节点的后面
            $('ul').after($li);
        })
    </script>
</head>
<body>
    <ul>
        <li><div>aaa <span>span</span></div></li>
        <li><div>aaa <span>span</span></div></li>
        <li><div>aaa <span>span</span></div></li>
    </ul>   
</body>
</html>
~~~

**appendTo()、prependTo()、insertBefore()、insertAfter()**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>节点的操作</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            var $li = $('<li>hello</li>')
            //$('ul').append($li);
            //$li.appendTo($('ul'));
            $li.prependTo($('ul'));
        })
    </script>
</head>
<body>
    <ul>
        <li><div>aaa <span>span</span></div></li>
        <li><div>aaa <span>span</span></div></li>
        <li><div>aaa <span>span</span></div></li>
    </ul>   
</body>
</html>
~~~

**两种写法的区别，会影响到链式操作**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>节点的操作</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            var $li = $('<li>hello</li>')
            //$('ul').append($li).css('background', 'red'); //整个ul背景变红
            $li.appendTo($('ul')).css('background', 'red'); //仅指定li背景变红
        })
    </script>
</head>
<body>
    <ul>
        <li><div>aaa <span>span</span></div></li>
        <li><div>aaa <span>span</span></div></li>
        <li><div>aaa <span>span</span></div></li>
    </ul>   
</body>
</html>
~~~

- JQ实战小技巧 
    - 添加html形式的操作与元素形式的操作

###节点的操作

####remove() ★★★★★

**remove()操作**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>删除元素</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //原生的删除元素的方式
            //document.body.removeChild(oDiv);
            //jQuery的方法
            $('div').remove();
        })
    </script>
</head>
<body>
    <div>div</div>
</body>
</html>
~~~

####clone() ★★★

- 默认的剪切操作
- 如何克隆事件(clone函数添加参数true)
- 例子：节点上移下移

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>删除元素</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //$('div').appendTo($('span')); //默认是剪切操作
            $('div').click(function(){
                alert(123);
            });
            var $div = $('div').clone();
            $div.appendTo($('span')); //克隆过来的div默认没有原来div的click事件。
            //clone()默认是克隆元素结构，而不克隆行为事件。
            //clone(true)，参数true就是可以复制之前的操作行为
        })
    </script>
</head>
<body>
    <div>div</div>
    <span>span</span>
</body>
</html>
~~~

**例子：节点的上移下移**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>删除元素</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            $('input[value="上移"]').click(function(){
                var $nowLi = $(this).closest('li');
                var $prevLi = $nowLi.prev();
                if($prevLi.length == 0){
                    alert('到头了');
                } else {
                    $nowLi.insertBefore($prevLi);
                }
            });
            $('input[value="下移"]').click(function(){
                var $nowLi = $(this).closest('li');
                var $nextLi = $nowLi.next();
                if($nextLi.length == 0){
                    alert('到尾了');
                } else {
                    $nowLi.insertAfter($nextLi);
                }
            });
        })
    </script>
</head>
<body>
    <ul>
        <li>1.<input type="button" value="上移"><input type="button" value="下移"></li>
        <li>2.<input type="button" value="上移"><input type="button" value="下移"></li>
        <li>3.<input type="button" value="上移"><input type="button" value="下移"></li>
        <li>4.<input type="button" value="上移"><input type="button" value="下移"></li>
        <li>5.<input type="button" value="上移"><input type="button" value="下移"></li> 
    </ul>
</body>
</html>
~~~

###JQ中的索引

####index() ★★★★★

- 第一种用法，兄弟中的排行
- 第二种用法，筛选后的排行
- 善于利用索引做实际开发
- 例子：选项卡

**兄弟中的排行**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>删除元素</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            alert($('#div1').index());
            //index()：索引值，代表的就是当前元素在所有兄弟节点中排第几。如果不添加参数，索引值与标签类型是无关的。
        })
    </script>
</head>
<body>
    <div></div>
    <p>p</p>
    <div id="div1">div</div>
    <div>div</div>
</body>
</html>
~~~

**注意事项**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>索引</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            alert($('#span1').index()); //弹出0
        })
    </script>
</head>
<body>
    <div><span>span</span></div>
    <div><span id="span1">span</span></div>
    <div><span>span</span></div>
</body>
</html>
~~~

**筛选后的排行**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>索引</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            alert($('#span1').index('span')); //2 
            //添加了参数span，现在的index就与div没有关系了，而是看#span1在所有span中的排行
            //第二种写法也可以
            alert($('span').index($('#span1')));
            //代表在所有span获取之后进行排行，看#span1排行老几
        })
    </script>
</head>
<body>
    <div><span>span</span></div>
    <span>span</span>
    <div><span id="span1">span</span></div>
    <div><span>span</span></div>
</body>
</html>
~~~

**选项卡**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>删除元素</title>
    <style>
        #div1 div {width: 200px; height: 200px; border: 1px #000 solid; display: none;}
        .active {background: red;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            $('#div1').find('input').click(function(){
                /*
                $('#div1').find('input').attr('class', '');
                $(this).attr('class', 'active');
                $('#div1').find('div').css('display', 'none');
                $('#div1').find('div').eq($(this).index('input')).css('display', 'block');
                */
                $(this).attr('class', 'active').siblings('input').attr('class', '');
                $('#div1').find('div').eq($(this).index('input')).css('display', 'block').siblings('div').css('display', 'none');
            })
        })
    </script>
</head>
<body>
    <div id="div1">
        <input type="button" value="1" class="active">
        <input type="button" value="2">
        <input type="button" value="3">
        <div style="display: block;">111</div>
        <div>222</div>
        <div>333</div>
    </div>
</body>
</html>
~~~

###JQ中的遍历

####each() ★★★★★

- 回调函数的两个参数
- this指向
- 用return false跳出each()循环;

**回调函数的两个参数**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>删除元素</title>
    <style>
        #div1 div {width: 200px; height: 200px; border: 1px #000 solid; display: none;}
        .active {background: red;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //each() => for
            //$('li').html('hello'); //相同操作的，不用each就可以
            /*
            $('li').each(function(i, elem){
                alert(i);
            });
            //each中的第一个形参i就是for循环中的i
            */
            /*
            $('li').each(function(i, elem){
                //elem.style.background = 'red'; 
                $(elem).css('background', 'red');
            });
            //each中的第二个参数elem就是每个元素
            //elem返回的是原生的元素，要转成jQuery对象要用$()括起来
            */
        })
    </script>
</head>
<body>
    <ul>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
    </ul>
</body>
</html>
~~~

**each的回调函数中this的指向**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>删除元素</title>
    <style>
        #div1 div {width: 200px; height: 200px; border: 1px #000 solid; display: none;}
        .active {background: red;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            $('li').each(function(i, elem){
                //this == elem jQuery中的each循环中的this与elem是一回事；而且这个this也是原生的
                $(this).html(i);
            });
        })
    </script>
</head>
<body>
    <ul>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
    </ul>
</body>
</html>
~~~

**each()循环中用return false跳出循环**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>删除元素</title>
    <style>
        #div1 div {width: 200px; height: 200px; border: 1px #000 solid; display: none;}
        .active {background: red;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            $('li').each(function(i, elem){
                //原生跳出循环用break
                //jQuery中跳出循环用return false;
                $(this).html(i);
                if(i == 2){
                    return false;
                }
            });
        })
    </script>
</head>
<body>
    <ul>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
    </ul>
</body>
</html>
~~~

###JQ包装对象

####wrap() ★★★

####wrapAll() ★

####wrapInner() ★

####unwrap() ★

- 例子：管理员与普通用户状态控制

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>删除元素</title>
    <style>
        #div1 div {width: 200px; height: 200px; border: 1px #000 solid; display: none;}
        .active {background: red;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        //wrap(): 包装
        //wrapAll(): 整体包装
        //wrapInner(): 内部包装
        //unwrap(): 删除包装，相当于删除父节点   
        $(function(){
           //$('span').wrap('<div>'); //注意这里要加尖括号
           // $('span').wrapAll('<div>'); //如果span之间夹着其他标签，用wrapAll()方法，就会把这些杂的标签挑到外面来，把剩下的span标签都给包起来
            // $('span').wrapInner('<div>'); //在span标签里面去包
            //$('span').unwrap(); 删除父级指的是父级标签，但body是不能删掉的
        })
    </script>
</head>
<body>
    <span>span</span>
    <p>p</p>
    <span>span</span>
    <span>span</span>
    <div><span>span</span></div>
</body>
</html>
~~~

**例子：管理员与普通用户状态控制**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>删除元素</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            $('input').click(function(){
                if($(this).val()=='管理员'){
                    $('#span1').wrap('<a href="#"></a>')
                } else if($(this).val()=='普通用户') {
                    $('#span1').unwrap();
                }
            })         
        })
    </script>
</head>
<body>
    <input type="radio" value="管理员" name="user" checked>管理员
    <input type="radio" value="普通用户" name="user">普通用户
    <br>
    <a href="#"><span id="span1">编辑此处</span></a>
</body>
</html>
~~~

###JQ转原生JS

####get() ★★★★★

- 与eq的区别
- 为什么要转，比如： 
    - 获取内容的高度
    - 元素之间的比较

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>删除元素</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        //get(): 把JQ转成原生JS，默认情况获取的是一个原生的集合，那么可以通过参数来找到集合中的指定项
        $(function(){
            alert($('div').eq(0).html()); //eq()后面接的是jQuery的写法
            alert($('div').get(0).innerHTML); // get()后面跟的是原生的写法。注意要给get()里面加参数           
        })
    </script>
</head>
<body>
    <div>aaaaa</div>
</body>
</html>
~~~

**获取内容的高度**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>获取内容的高度</title>
    <style>
        * {margin: 0; padding: 0;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //获取内容的高度
            //alert($('#t1').height()); //100 获取到的是textarea的高度
            alert($('#t1').get(0).scrollHeight); //获取内部内容高度：jQuery没有提供方法，因此只能转成原生后用scrollHeight来获取
        })         
    </script>
</head>
<body>
    <textarea id="t1" style="height: 100px;">
        adlfj
        adf
        adf
        ga
        eg
        d
        gbsh
        fdg
        fgzfbh
        g
        hdgh\x\gn\fgh\
        df
        fb
        xcb
        sfh
    </textarea>
</body>
</html>
~~~

**元素之间的比较**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>删除元素</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            $('input[value="上移"]').click(function(){
                var $nowLi = $(this).closest('li');
                var $prevLi = $nowLi.prev();
                //if($nowLi == $nowLi.parent().children().eq(0)){ //元素之间的比较不能用两个JQ对象进行
                //console.log([] == []); //false
                //console.log({} == {}); //false
                if($nowLi.get(0) == $nowLi.parent().children().eq(0).get(0)){
                //if($prevLi.length == 0){
                    alert('到头了');
                } else {
                    $nowLi.insertBefore($prevLi);
                }
            });
            $('input[value="下移"]').click(function(){
                var $nowLi = $(this).closest('li');
                var $nextLi = $nowLi.next();
                if($nextLi.length == 0){
                    alert('到尾了');
                } else {
                    $nowLi.insertAfter($nextLi);
                }
            });
        })
    </script>
</head>
<body>
    <ul>
        <li>1.<input type="button" value="上移"><input type="button" value="下移"></li>
        <li>2.<input type="button" value="上移"><input type="button" value="下移"></li>
        <li>3.<input type="button" value="上移"><input type="button" value="下移"></li>
        <li>4.<input type="button" value="上移"><input type="button" value="下移"></li>
        <li>5.<input type="button" value="上移"><input type="button" value="下移"></li> 
    </ul>
</body>
</html>
~~~

###本课练习

- 左右切换数据
- 评分效果

##2014年10月16日第三堂课

###元素的尺寸

####width() height() ★★★★★

####innerWidth() innerHeight() ★★★★★

####outerWidth() outerHeight() ★★★★★

- 参数的作用
- 与原生JS的区别

**元素尺寸的获取**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>元素的尺寸的获取</title>
    <style>
        #div1 {width: 100px; height: 100px; background: red; padding: 10px; border: 1px solid #000;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            alert($('#div1').width()); //100 不带单位
            //width() => width
            alert($('#div1').innerWidth()); //120
            //innerWidth() => width + padding 
            alert($('#div1').outerWidth()); //122
            //outerWidth() => width + padding + border
            alert($('#div1').outerWidth(true)); //132
            //outerWidth(true) => width + padding + border + margin
        })
    </script>
</head>
<body>
    <div id="div1">div</div>
</body>
</html>
``

**元素尺寸的设置**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>元素的尺寸的设置</title>
    <style>
        #div1 {width: 100px; height: 100px; background: red; padding: 10px; border: 1px solid #000; margin: 5px;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //$('#div1').width(200); //设置了style中的width
            //$('#div1').innerWidth(200); //padding左右是20；然后总共是200，那么style中的width就是180 => width: 200 - padding
            //$('#div1').outerWidth(200); //padding左右是20；border左右是2；总共200，那么width就是178 => width: 200 - padding - border
            $('#div1').outerWidth(200, true);
            //width: 200 - padding - border - margin为168
        })
    </script>
</head>
<body>
    <div id="div1">div</div>
</body>
</html>
~~~

**与原生JS获取尺寸的区别**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>元素的尺寸的设置</title>
    <style>
        #div1 {width: 100px; height: 100px; background: red; display: none; }
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            alert($('#div1').get(0).offsetWidth); //0 原生的JS是获取不到隐藏元素的尺寸的
            alert($('#div1').width()); //100 JQ是可以获取隐藏元素的尺寸的
        })
    </script>
</head>
<body>
    <div id="div1">div</div>
</body>
</html>
~~~

###实战小技巧

- 可视区的尺寸
- 页面的尺寸

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>可视区的尺寸</title>
    <style>
        body {margin: 0; padding: 0;}
        #div1 {width: 100px; height: 100px; background: red; display: none; }
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            alert($(window).height()); //可视区的高
            alert($(document).height()); //页面的高 
            //如果没有给body清margin和padding，得到的是2016；如果清掉了，得到的就是2000
        })
    </script>
</head>
<body style="height: 2000px;">
    <div id="div1">div</div>
</body>
</html>
~~~

###滚动距离

####scrollTop() ★★★★★

####scrollLeft() ★

**滚动距离**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>可视区的尺寸</title>
    <style>
        body {margin: 0; padding: 0;}
        #div1 {width: 100px; height: 100px; background: red; display: none; }
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            $(document).click(function(){
                //alert($(document).scrollTop()); //获取滚动距离
                //当滚动条滚到最底部的时候 $(document).scrollTop() == $(document).height() - $(window).height()
                $(document).scrollTop(300); //设置滚动距离
            })
        })
    </script>
</head>
<body style="height: 2000px;">
    <div id="div1">div</div>
</body>
</html>
~~~

###元素距离

####offset() ★★★★★

- left top

####position() ★★★

- left top
- 不认margin值

**offset()**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>到达页面的距离：offset()</title>
    <style>
        body {margin: 0; padding: 0;}
        #div1 {width: 200px; height: 200px; background: red; margin: 200px; position: relative; }
        #div2 {width: 100px; height: 100px; margin: 50px; background: yellow;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //offset()的距离值都是相对于整个页面的
            alert($('#div1').offset().left); //元素距离整个页面左边的距离是offset().left，top就是距离整个页面上边的距离。注意left和top后面都不加括号。
            alert($('#div2').offset().left); //不论怎样嵌套，定位父级是谁，都是到达页面边缘的距离。这个与原生的offsetLeft和offsetTop不同。原生的相对于定位的祖先节点的距离。
        })
    </script>
</head>
<body style="height: 2000px;">
    <div id="div1">
        <div id="div2"></div>
    </div>
</body>
</html>
~~~

**position**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>到达页面的距离：offset()</title>
    <style>
        body {margin: 0; padding: 0;}
        #div1 {width: 200px; height: 200px; background: red; margin: 200px; position: relative; }
        #div2 {width: 100px; height: 100px; margin: 50px; background: yellow;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            alert($('#div2').position().left); //0
            //position()就是到有定位的祖先节点的距离
            //position()方法默认是不认margin值的。所以上面的代码弹出0
        })
    </script>
</head>
<body style="height: 2000px;">
    <div id="div1">
        <div id="div2"></div>
    </div>
</body>
</html>
~~~

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>到达定位祖先元素的距离position()</title>
    <style>
        body {margin: 0; padding: 0;}
        #div1 {width: 200px; height: 200px; background: red; margin: 200px; position: relative; }
        #div2 {width: 100px; height: 100px; position: relative; left: 50px; background: yellow;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            alert($('#div2').position().left); //50
            //position()就是到有定位的祖先节点的距离
        })
    </script>
</head>
<body style="height: 2000px;">
    <div id="div1">
        <div id="div2"></div>
    </div>
</body>
</html>
~~~

###实战小技巧

- 利用计算原理，得到相应值 
    - offsetParent() ★
- 例子：懒加载页面中的图片

**计算出到有定位的祖先节点的距离**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        body {margin: 0; padding: 0;}
        #div1 {width: 200px; height: 200px; background: red; margin: 200px; position: relative; }
        #div2 {width: 100px; height: 100px; margin: 50px; background: yellow;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            alert($('#div2').offset().left - $('#div2').offsetParent().offset().left); //50
            //通过计算的方法获得到达有定位的祖先元素的距离，不管是不是由margin产生的，因此规避了position()不认margin的问题                 
        })
    </script>
</head>
<body style="height: 2000px;">
    <div id="div1">
        <div id="div2"></div>
    </div>
</body>
</html>
~~~

**懒加载图片**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        body {margin: 0; padding: 0;}
        div {margin-top: 300px; width: 470px; height: 150px; border: 1px #000 solid;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            toChange();
            $(window).scroll(toChange);
            function toChange(){
                $('img').each(function(i, elem){
                    if($(elem).offset().top < $(window).height() + $(document).scrollTop()){ //如果图片进入了可视区
                        $(elem).attr('src', $(elem).attr('_src'));
                    }
                });
            }       
        })
    </script>
</head>
<body>
    <div><img _src="img/1.jpg" alt=""></div>
    <div><img _src="img/2.jpg" alt=""></div>
    <div><img _src="img/3.jpg" alt=""></div>
    <div><img _src="img/4.jpg" alt=""></div>
    <div><img _src="img/5.jpg" alt=""></div>
    <div><img _src="img/6.jpg" alt=""></div>
</body>
</html>
~~~

###JQ的事件

####on() ★★★★★

####off() ★★★★★

- JQ中都是绑定的形式
- 支持多事件写法
- click()写法，也是采用off()取消

**用on()的形式绑定事件**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery中的事件</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
    //在JQ中的事件操作都是绑定的形式
        $(function(){
            //原生中有的事件都可以像下面这么用（去掉on）
            //$('#div1').click(function(){alert(123);});
            //$('#div1').mouseover(function(){alert(123);});
            //$('#div1').mousedown(function(){alert(123);});
            //$('#div1').scroll(function(){alert(123);})
            //$('#div1').on('click', function(){alert(123);}) //这就相当于$('#div1').click(function(){alert(123);})
            //$('#div1').on('click mouseover', function(){alert(123);}); //通过空格分隔多个事件名称，可以同时绑定
        })
    </script>
</head>
<body style="height: 2000px;">
    <div id="div1">aaaaaa</div>
</body>
</html>
~~~

**用off()取消事件**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery中的事件</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
    //无论是用on()还是用click()形式绑定的事件，都是用off()取消的
        $(function(){
            /*
            $('#div1').on('click mouseover', function(){
                alert(123);
                $(this).off(); //删除所有的事件操作
            })
            */
            $('#div1').on('click mouseover', function(){
                alert(123);
                $(this).off('mouseover'); //取消指定的事件
            })
        })
    </script>
</head>
<body style="height: 2000px;">
    <div id="div1">aaaaaa</div>
</body>
</html>
~~~

###Event对象 ★★★★★

####pageX, pageY

- 与cient的区别

####which

####target

####stopPropagation()

####preventDefault()

####return false

**pageX和pageY；clientX和clientY**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery中的event事件对象</title>
    <style>
        #div1 {margin: 200px;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            $('#div1').click(function(ev){
                alert(ev.pageY); //鼠标的y坐标
                //ev.pageX和ev.pageY始终是相对于整个页面的
                alert(ev.clientY); //鼠标的y坐标
                //ev.clientX和ev.clientY始终是相对于可视区的
            })
        })
    </script>
</head>
<body style="height: 2000px;">
    <div id="div1">aaaaaa</div>
</body>
</html>
~~~

**which键盘键值**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery中的event事件对象</title>
    <style>
        #div1 {margin: 200px;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        //ev.which是键盘的键值
        $(function(){
            $(document).keydown(function(ev){
                alert(ev.which); //页面上按下按键，弹出键盘键值
                //alert(ev.keyCode); //也可以弹出键盘键值
                //alert(ev.ctrlKey); //可以检测是否ctrl键是按下的
            })
        })
    </script>
</head>
<body style="height: 2000px;">
    <div id="div1">aaaaaa</div>
</body>
</html>
~~~

**ev.target事件源**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery中的event事件对象</title>
    <style>
        #div1 {margin: 200px;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        //ev.target 当前目标元素，也就是事件源
        $(function(){
            $(document).click(function(ev){
                //alert(this); //这个this总是指向document
                alert(ev.target); //如果点击到a上，那么弹出的就是#div1这个元素
            })
        })
    </script>
</head>
<body style="height: 2000px;">
    <div id="div1">aaaaaa</div>
</body>
</html>
~~~

**ev.stopPropagation() 阻止冒泡**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery中的event事件对象</title>
    <style>
        #div1 {margin: 200px;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        //stopPropagation()：阻止冒泡
        $(function(){
            $(document).click(function(){
                alert(123);
            })
            $('#div1').click(function(ev){
                ev.stopPropagation(); //阻止了#div1的事件冒泡，那么点击#div1就不会再弹出123了
            })
        })
    </script>
</head>
<body style="height: 2000px;">
    <div id="div1">aaaaaa</div>
</body>
</html>
~~~

**ev.preventDefault() 阻止默认事件**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery中的event事件对象</title>
    <style>
        #div1 {margin: 200px;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        //ev.preventDefault()：阻止默认事件
        $(function(){
            $(document).contextmenu(function(ev){ //点击右键就不会弹出默认右键菜单了
                ev.preventDefault();
            })
        })
    </script>
</head>
<body style="height: 2000px;">
    <div id="div1">aaaaaa</div>
</body>
</html>
~~~

**return false 既阻止默认事件又阻止冒泡**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery中的event事件对象</title>
    <style>
        #div1 {margin: 200px;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        //在事件函数中写return false代表：既阻止默认事件又阻止冒泡
        $(function(){
            $(document).contextmenu(function(ev){
                //代码
                return false;
            })
        })
    </script>
</head>
<body style="height: 2000px;">
    <div id="div1">aaaaaa</div>
</body>
</html>
~~~

###JQ实战小技巧

- 多次添加on的处理方式
- 例子：拖拽效果

**多次添加on的处理方式**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>多次添加on的处理方式</title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            /*
            //以下这种形式，如果多次点击#div1后再点击#span1，会发现1会弹出多次，这是因为通过多次点击#div1，使得#span1多次调用了click事件
            $('#div1').click(function(){
                $('#span1').click(function(){
                    alert(1);
                })
            })
            */
            //解决以上问题的方法
            $('#div1').click(function(){
                $('#span1').off('click').click(function(){
                    alert(1);
                })
            })
        })
    </script>
</head>
<body style="height: 2000px;">
    <div id="div1">aaaaaa</div>
    <span id="span1">span</span>
</body>
</html>
~~~

**用jQuery实现拖拽效果**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>用JQ实现拖拽</title>
    <style>
        * {margin: 0; padding: 0;}
        #div1 {width: 100px; height: 100px; background: red; position: absolute; left: 100px; top: 100px;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            var disX = 0;
            var disY = 0;
            var $div = $('#div1');
            $div.on('mousedown', function(ev){
                disX = ev.pageX - $(this).offset().left;
                disY = ev.pageY - $(this).offset().top;
                $(document).on('mousemove', function(ev){
                    $div.css('left', ev.pageX - disX);
                    $div.css('top', ev.pageY - disY);
                })
                $(document).on('mouseup', function(){
                    $(this).off();
                })
                return false;
            })      
        })
    </script>
</head>
<body style="height: 2000px;">
    <div id="div1">div</div>
</body>
</html>
~~~

###delegate() ★★★★★

- 委托的好处
- ev.delegateTarget

**事件委托**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>事件委托</title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            /* 普通写法，click加到li身上
            $('li').on('click', function(){
                $(this).css('background', 'red');
            })
            */
            //事件委托的写法
            //click加到了ul身上
            $('ul').delegate('li', 'click', function(ev){
                $(this).css('background', 'red'); //this指向触发的li
                $(ev.delegateTarget).css('background', 'green'); //这时候的ev.delegateTarget指向的就是$('ul')
            })
            //事件委托的好处：
            //1. 性能更好
            //2. 对后续添加的元素，可以直接拥有一些操作行为
            //3. 事件委托的时间函数中的this指向的是委托的元素 要想找到是谁进行委托的，那个元素是哪个，可以用ev.delegateTarget来找到。
            $('#input1').click(function(){
                var $li = $('<li>hello</li>');
                $('ul').append($li);
            })
            //后来添加的li照样有click事件，这是通过事件委托实现的。如果用普通写法，新添加的li是没有click事件的。
        })
    </script>
</head>
<body style="height: 2000px;">
    <input id="input1" type="button" value="添加">
    <ul>
        <li>11111</li>
        <li>11111</li>
        <li>11111</li>
        <li>11111</li>
        <li>11111</li>
    </ul>
</body>
</html>
~~~

###undelegate() ★★★

**undelegate() 取消委托**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>取消委托</title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            $('ul').delegate('li', 'click', function(ev){
                $(this).css('background', 'red'); //this指向触发的li
                $(ev.delegateTarget).undelegate(); //注意取消委托的时候，是要在delegateTarget上取消，而不是在this上取消
            })
            $('#input1').click(function(){
                var $li = $('<li>hello</li>');
                $('ul').append($li);
            })
        })
    </script>
</head>
<body style="height: 2000px;">
    <input id="input1" type="button" value="添加">
    <ul>
        <li>11111</li>
        <li>11111</li>
        <li>11111</li>
        <li>11111</li>
        <li>11111</li>
    </ul>
</body>
</html>
~~~

###trigger() ★★★★★

- 比click()形式更强大
- 事件的命名空间
- 例子：主动触发的添加内容

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>事件的命名空间</title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        // trigger(): 主动触发
        $(function(){
            $('ul').delegate('li', 'click', function(){
                $(this).css('background', 'red'); //this指向触发的li
            })
            $('#input1').click(function(){
                var $li = $('<li>'+ $('#input2').val() +'</li>');
                $('ul').append($li);
            })
            $('#input2').keydown(function(ev){
                if(ev.which == 13){
                    $('#input1').trigger('click'); //点击回车的时候，就主动触发#input1的click事件
                    //$('#input1').click();  这种写法就相当于上面的那种写法
                }
            })
        })
    </script>
</head>
<body style="height: 2000px;">
    <input id="input1" type="button" value="添加"><input id="input2" type="text">
    <ul>
        <li>11111</li>
        <li>11111</li>
        <li>11111</li>
        <li>11111</li>
        <li>11111</li>
    </ul>
</body>
</html>
~~~

**事件的命名空间**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>事件的命名空间</title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            $('div').on('click', function(){
                alert(1);
            })
            $('div').on('click.abc', function(){ //注意，这里click后面有个.abc 这就是命名空间
                alert(2);
            })
            $('div').trigger('click.abc'); //只主动触发div上命名空间为abc的click事件
        })
    </script>
</head>
<body style="height: 2000px;">
    <div>div</div>
</body>
</html>
~~~

**事件的命名空间2**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>事件的命名空间</title>
    <style>
        * {margin: 0; padding: 0;}
        #div1 {width: 100px; height: 100px; background: red; position: absolute; left: 100px; top: 100px;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            var disX = 0;
            var disY = 0;
            var $div = $('#div1');
            $div.on('mousedown', function(ev){
                disX = ev.pageX - $(this).offset().left;
                disY = ev.pageY - $(this).offset().top;
                $(document).on('mousemove.drag', function(ev){
                    $div.css('left', ev.pageX - disX);
                    $div.css('top', ev.pageY - disY);
                })
                $(document).on('mouseup.drag', function(){
                    //$(this).off('mousemove.drag').off('mouseup.drag'); //这种写法和下面的写法都可以
                    $(this).off('.drag');
                    //注意：off()中可以只添加命名空间，但是trigger()中的命名空间前面必须要添加事件名才行
                })
                return false;
            })      
        })
    </script>
</head>
<body style="height: 2000px;">
    <div id="div1">div</div>
</body>
</html>
~~~

###工具方法

####$.type() ★★★★★

- 比原生typeof更强大

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>$.type()</title>
    <style>
        * {margin: 0; padding: 0;}
        #div1 {width: 100px; height: 100px; background: red; position: absolute; left: 100px; top: 100px;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
    //$().css() $().html() $().click(); //这些方法都是针对JQ对象的，针对原生是不能调用这些方法的
    //$.XXX() $.YYY() $.ZZZ(); //这些方法前面只有一个$ 这些就是工具方法：既可以给JQ对象用，也可以给原生JS用
    //比如：$.XXX($('div'))和$.XXX(oDiv) 这两种写法都可以
        $(function(){
            // $.type(): 查看变量的类型
            /*
            var a = 'hello';
            alert(typeof a); //string
            alert($.type(a)); //string
            */
            /*
            var a = [1, 2, 3];
            alert(typeof a); //object
            alert($.type(a)); //array
            */
            /*
            var a = new Date;
            alert(typeof a); //object
            alert($.type(a)); //date
            */
            /*
            var a = null;
            alert(typeof a); //object
            alert($.type(a)); //null
            */
            var a = {};
            alert(typeof a); //object
            alert($.type(a)); //object
        })
    </script>
</head>
<body style="height: 2000px;">
    <div id="div1">div</div>
</body>
</html>
~~~

####$.isFunction() ★★★

####$.isNumeric() ★★★

####$.isArray() ★★★

####$.isWindow() ★★★

####$.isEmptyObject() ★★★

####$.isPlainObject() ★★★

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        * {margin: 0; padding: 0;}
        #div1 {width: 100px; height: 100px; background: red; position: absolute; left: 100px; top: 100px;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            /*
            var a = function(){};
            alert($.isFunction(a)); //true
            */
            /*
            var a = 123;
            alert($.isNumeric(a)); //true
            var b = '123';
            alert($.isNumeric(b)); //true
            */
            /*
            var a = [];
            alert($.isArray(a)); //true
            */
            /*
            var a = window;
            alert($.isWindow(a)); //true
            */
            /*
            var a = {};
            alert($.isEmptyObject(a)); //true
            var b = {'a': '1'};
            alert($.isEmptyObject(b)); //false
            var c = [];
            alert($.isEmptyObject(c)); //true
            */
            //plain object 对象自变量：{}或new Object出来的
            var a = {};
            alert($.isPlainObject(a)); //true
            var b = {'a': '1'};
            alert($.isPlainObject(b)); //true
            var c = new Object;
            alert($.isPlainObject(c)); //true
            var d = new Date;
            alert($.isPlainObject(d)); //false
            var e = [];
            alert($.isPlainObject(e)); //false
        })
    </script>
</head>
<body style="height: 2000px;">
    <div id="div1">div</div>
</body>
</html>
~~~

####$.extend() ★★★★★

- 对象继承操作
- 深拷贝操作

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>$.extend() 对象的拷贝</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            /*
            var a = {
                name: 'hello'
            };
            var b = a;
            b.name = 'hi';
            alert(a.name); //hi 对象引用，b.name更改后，a也收到了影响。因为a、b在同一个指针上
            */
            /* $.extend进行浅拷贝
            var a = {
                name: 'hello'
            };
            var b = {};
            $.extend(b, a, {age: 20}); //把从第二个参数开始，把后面所有的都像第一个参数进行拷贝
            console.log(b);
            b.name = 'hi';
            alert(a.name); //a没有受到影响
            */
            /* $.extend默认是浅拷贝
            var a = {
                name: {age: 20}
            };
            var b = {};
            $.extend(b, a); 
            b.name.age = 30;
            alert(a.name.age); //30 a又受到了影响，因为$.extend()默认为浅拷贝，就是指拷贝一层
            */
            //通过添加参数true实现$.extend的深拷贝
            var a = {
                name: {age: 20}
            };
            var b = {};
            $.extend(true, b, a); //通过添加参数true实现深拷贝
            b.name.age = 30;
            alert(a.name.age); //20 深拷贝就是指不管多少层，都不会影响到之前的对象
        });
    </script>
</head>
<body>
</body>
</html>
~~~

####$.proxy() ★★★

- 两处传参的的区别

**$.proxy()改变this指向的用法**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>$.proxy改变this指向</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            // $.proxy(): 改this指向
            function show(){
                alert(this);
            }
            //show(); //this是指向window的
            //show.call(document); //让this指向document
            //以下是通过$.proxy()方法来改变this指向
            $.proxy(show, document); //让show函数中的this指向document，只改变指向，并没有调用
            $.proxy(show, document)(); //后面加一对小括号才算是调用了，这时候弹出的就是document
        });
    </script>
</head>
<body>
</body>
</html>
~~~

**用$.proxy()传参的用法**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>$.proxy改变this指向</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            function show(n1, n2){
                alert(n1);
                alert(n2);
                alert(this);
            }
            $.proxy(show, document)(3, 4); //后面加一对小括号才算是调用了，这时候弹出的就是document
            //也可以写成如下形式：
            $.proxy(show, document, 3, 4)();
            //也可以写成如下形式：
            $.proxy(show, document, 3)(4);
        });
    </script>
</head>
<body>
</body>
</html>
~~~

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>$.proxy改变this指向</title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            function show(n1, n2){
                alert(n1);
                alert(n2);
                alert(this);
            }
            //$(document).on('click', $.proxy(show, window)(3,4)); //这样写show函数就直接调用了，所以要写成下面的形式
            $(document).on('click', $.proxy(show, window, 3, 4));
        });
    </script>
</head>
<body>
</body>
</html>
~~~

###JQ实战小技巧

- 利用This改指向，更加方便

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>$.proxy改变this指向</title>
    <style>
        #div1 {width: 100px; height: 100px; border: 1px solid #000; }
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            $('#div1').on('click', function(){
                /*
                setTimeout(function(){
                    //$(this).css('background', 'red'); 这样写肯定是有错误的，因为this指向的是window
                }, 1000);
                */
                //以下是一种比较简单的改变this指向的方法
                 var This = this;
                 setTimeout(function(){
                    $(This).css('background', 'red');
                 }, 1000);
            })
        });
    </script>
</head>
<body>
    <div id="div1"></div>
</body>
</html>
~~~

###本课练习

- 登录弹窗效果

##2014年10月19日第四堂课

###JQ中的运动

- 时间的概念

####show(), hide(), toggle() ★★★

- fast normal slow

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        #div1 {width: 200px; height: 200px; background: red;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        //normal: 400毫秒
        //fast：200
        //slow: 600
        //也可以写成事件形式（默认单位是毫秒）
        //不写参数没有动画效果
        $(function(){
            var bBtn = true;
            $('#input1').click(function(){
                /*
                if(bBtn){
                    $('#div1').hide('fast');
                } else {
                    $('#div1').show(1000);
                }
                bBtn = !bBtn;
                */
                $('#div1').toggle('normal'); //toggle是show和hide的合体操作，不写参数就没有动画效果
            })
        });
    </script>
</head>
<body>
    <input type="button" value="点击" id="input1">
    <div id="div1"></div>
</body>
</html>
~~~

####fadeIn(), fadeOut(), fadeToggle() ★★★

- 有默认的时间normal

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        #div1 {width: 200px; height: 200px; background: red;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        //fadeIn和fadeOut有默认时间：400毫秒
        $(function(){
            var bBtn = true;
            $('#input1').click(function(){
                /*
                if(bBtn){
                    $('#div1').fadeOut('fast');
                } else {
                    $('#div1').fadeIn(1000);
                }
                bBtn = !bBtn;
                */
                $('#div1').fadeToggle('normal');
            })
        });
    </script>
</head>
<body>
    <input type="button" value="点击" id="input1">
    <div id="div1"></div>
</body>
</html>
~~~

####slideDown(), slideUp(), slideToggle() ★★★

- 有默认的时间normal

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        #div1 {width: 200px; height: 200px; background: red;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        //slideIn和slideOut有默认时间：400毫秒
        $(function(){
            var bBtn = true;
            $('#input1').click(function(){
                if(bBtn){
                    $('#div1').slideUp('fast');
                } else {
                    $('#div1').slideDown(1000);
                }
                bBtn = !bBtn;
                //$('#div1').slideToggle('normal'); 
            })
        });
    </script>
</head>
<body>
    <input type="button" value="点击" id="input1">
    <div id="div1"></div>
</body>
</html>
~~~

####animate() ★★★★★

- 参数的作用
- 数值的运算操作
- 配置参数step的作用 
    - duration easing complete
- 队列的概念 
    - 其他元素不会存入队列
- 链式运动
- delay() ★
- stop() ★★★★★ 
    - 参数的作用
- finish() ★
- JQ实战小技巧 
    - 运动的队列问题
    - 例子：淘宝轮播图

**参数的作用**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>animate()方法</title>
    <style>
        #div1, #div2 {width: 200px; height: 200px; background: red; margin-bottom: 20px;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        //animate:
        //第一个参数：对象 {} 设置样式属性和值（目标点）
        //第二个参数：时间（毫秒）默认是400毫秒
        //第三个参数：运动形式 只有两种 swing(默认：缓冲 慢-快-慢)和linear(匀速的)
        //第四个参数：结束运动时候的回调函数
        $(function(){
            $('#input1').click(function(){
                $('#div1').animate({
                    width: 400, //数值和带单位的字符串都可以
                }, 1000, 'swing', function(){
                    alert(123);
                });
                $('#div2').animate({
                    width: 400, //数值和带单位的字符串都可以
                }, 1000, 'linear');
            });
        });
    </script>
</head>
<body>
    <input type="button" value="点击" id="input1">
    <div id="div1"></div>
    <div id="div2"></div>
</body>
</html>
~~~

**数值的运算操作**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>animate()方法</title>
    <style>
        #div1, #div2 {width: 200px; height: 200px; background: red; margin-bottom: 20px;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            $('#input1').click(function(){
                $('#div1').animate({
                    width: '+=100' //每次的初始值加上100 
                }, 1000, 'swing');
            });
        });
    </script>
</head>
<body>
    <input type="button" value="点击" id="input1">
    <div id="div1"></div>
</body>
</html>
~~~

**配置参数step的作用**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>animate()方法</title>
    <style>
        #div1, #div2 {width: 200px; height: 200px; background: red; margin-bottom: 20px;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        //配置参数，在animate函数中写两个json
        //第一个json中配置原来的第一个参数：设置样式属性和目标值
        //第二个json是配置原来的第二到第四个参数：时间(duration)、运动形式(easing)和回调函数(complete)，还有一个比较有用的就是step
        $(function(){
            $('#input1').click(function(){
                $('#div1').animate({
                    width: 300
                }, {
                    duration: 1000, 
                    easing: 'linear',
                    complete: function(){
                        //alert(123);
                    },
                    step: function(a, b){ //能够监测定时器的每一次变化
                        //console.log(a);
                        //console.log(b);
                        console.log(b.pos); //b.pos就是运动过程当中的比例值（0~1）
                    }
                });
            });
        });
    </script>
</head>
<body>
    <input type="button" value="点击" id="input1">
    <div id="div1"></div>
</body>
</html>
~~~

**巧用配置参数step**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>animate()方法</title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            $('#input1').click(function(){
                $('#div1').animate({
                    num: "move" //只要这里面有设置的东西，就可以利用后面的step，这里只是用来占位的，可以不起作用
                }, {
                    duration: 2000, 
                    easing: 'linear',
                    complete: function(){
                        //alert(123);
                    },
                    step: function(a, b){ 
                        $('#div1').html(parseInt(b.pos * 27382667));
                    }
                });
            });
        });
    </script>
</head>
<body>
    <input type="button" value="点击" id="input1">
    <div id="div1">0</div> //用2秒让div中从数字0运动到27382667
</body>
</html>
~~~

**animate()中的队列**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>运动的队列概念</title>
    <style>
        #div1 {width: 200px; height: 200px; background: red; position: absolute;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            $('#input1').click(function(){
                /*              
                $('#div1').animate({width: 300}, 1000);
                $('#div1').animate({height: 300}, 1000);
                $('#div1').animate({left: 300}, 1000);
                //上面三句话并不是同时运行的，而是第一个运动完成之后进行下一个运动 它们构成一个队列
                alert(123); //这一句在一开始就会执行
                */
                //链式调用
                $('#div1').animate({width: 300}, 1000).animate({height: 300}, 1000).animate({left: 300}, 1000);
            });
        });
    </script>
</head>
<body>
    <input type="button" value="点击" id="input1">
    <div id="div1"></div>
</body>
</html>
~~~

**delay()**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>delay()延迟运动</title>
    <style>
        #div1 {width: 200px; height: 200px; background: red; position: absolute;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            $('#input1').click(function(){
                $('#div1').animate({width: 300}, 1000).delay(1000).animate({height: 300}, 1000).delay(1000).animate({left: 300}, 1000);
            });
        });
    </script>
</head>
<body>
    <input type="button" value="点击" id="input1">
    <div id="div1"></div>
</body>
</html>
~~~

**stop()和finish()**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>delay()延迟运动</title>
    <style>
        #div1 {width: 200px; height: 200px; background: red; position: absolute;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            $('#input1').click(function(){
                $('#div1').animate({width: 300}, 1000).animate({height: 300}, 1000);
            });
            $('#input2').click(function(){
                //$('#div1').stop(); //默认情况下只会停止当前运动，对后续运动没有影响
                //$('#div1').stop(true); //添第一个参数true，可以停止所有运动
                //$('#div1').stop(true, true); //添加第二个参数：可以停止到当前运动指定的目标点
                $('#div1').finish(); //让这个对象的所有运动全部立即完成
            })
        });
    </script>
</head>
<body>
    <input type="button" value="点击" id="input1">
    <input type="button" value="停止运动" id="input2">
    <div id="div1"></div>
</body>
</html>
~~~

**运动的队列问题**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>运动的队列问题</title>
    <style>
        #div1 {width: 100px; height: 100px; background: red; position: absolute;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //stop(): 清空队列的行为
            /*
            //下面代码问题，鼠标快速移入移出，会出现问题，队列变得很长
            $('#div1').mouseover(function(){
                $(this).animate({width: 200, height: 200})
            }).mouseout(function(){
                $(this).animate({width: 100, height: 100})
            });
            */
            //可以利用stop()来在往队列里添加运动之前，先清空一下队列
            $('#div1').mouseover(function(){
                $(this).stop().animate({width: 200, height: 200})
            }).mouseout(function(){
                $(this).stop().animate({width: 100, height: 100})
            });
        });
    </script>
</head>
<body>
    <input type="button" value="点击" id="input1">
    <input type="button" value="停止运动" id="input2">
    <div id="div1"></div>
</body>
</html>
~~~

###工具方法

####$.parseJSON() ★★★★★

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //$.parseJSON: 把JSON类型的字符串转换成真正的JSON数据
            var a = '{"name":"hello", "age": "20"}';
            var json = $.parseJSON(a); //只能针对JSON类型的字符串（安全性比较好），必须是严格的JSON（都要写双引号，不加双引号解析不了）
            console.log(json);
            console.log(json.name);
        });
    </script>
</head>
<body>
</body>
</html>
~~~

####$.parseHTML() ★

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //$.parseHTML：转化html形式的字符串，转成DOM节点，然后把这些DOM节点放到数组当中
            var a = '<div>div</div><span>span</span>';
            var arr = $.parseHTML(a); 
            console.log(arr);
            arr[1].innerHTML = 'hello';
            $('body').append(arr[1]);
        });
    </script>
</head>
<body>
</body>
</html>
~~~

####$.parseXML() ★

####$.isXMLDoc() ★

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //$.parseXML:　把XML形式的字符串转成真正的XML节点
            //$.isXMLDoc: 判断是否是xml document
            var a = '<?xml version="1.0" encoding="utf-8"?><hello>nihao</hello>'; //注意这里一定要写xml的头信息
            var xmlDoc = $.parseXML(a); //返回的就是xml的document元素
            console.log(xmlDoc);
            console.log($(xmlDoc).find('hello').html());
            console.log($.isXMLDoc(xmlDoc));
            var b = document;
            console.log($.isXMLDoc(b));
        });
    </script>
</head>
<body>
</body>
</html>
~~~

####$.ajax() ★★★★★

- 什么是ajax 
    - 提交数据、查询数据
    - url
    - success
    - type
    - data
    - error
    - dataType
    - async
    - 例子：ajax版本的选项卡

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>ajax</title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            $('#input1').on('input', function(){
                //console.log(1);
                $.ajax({
                    url: 'user.php', //不写data数据，通过在url中添加'user.php?user='+ $(this).val() 也可以以get的方式传输数据
                    type: 'post', //默认的type为get方式，还有一种提交方式是post方式
                    data: {user: $(this).val()}, //可以写成json，也可以写成拼接字符串 'user='+ $(this).val()
                    dataType: 'json', //这里可以设置返回数据转化成什么类型。这里写了类型，在success里面就不需要再解析。有json、html和xml
                    success: function(data){ //返回1的时候可以注册；返回0的时候不可以注册
                        //var dataJson = $.parseJSON(data); //如果没有写dataType的话，这里要把返回的data先解析成想要的形式
                        if(data == 1){
                            $('#div1').html('可以注册');
                        } else if(data == 0){
                            $('#div1').html('已经注册过了，不能注册');
                        }
                    },
                    error: function(err){ //请求不成功的时候走error这里
                        console.log(err); //404 500以上服务器错误
                    }
                    async: false//操作是否异步。默认情况下ajax都是异步操作。如果async为false，即为同步的。同步形势下，ajax执行完毕之后，ajax后面的console.log(123);才会执行
                });
                console.log(123);
            })
        });
    </script>
</head>
<form action="reg.php">
    <input type="text" name="user" id="input1">
    <input type="submit" value="注册">
</form>
<div id="div1"></div>
<body>
</body>
</html>
~~~

**用ajax实现选项卡-简略版不安全**

~~~ html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>无标题文档</title>
<style>
#div1 div{ width:200px; height:200px; border:1px #000 solid; display:none;}
.active{ background:red;}
</style>
<script src="jquery-1.11.1.js"></script>
<script>
$(function(){
    $('#div1').find('input').click(function(){
        var index = $(this).index();
        $('#div1').find('input').attr('class','');
        $('#div1').find('div').css('display','none');
        $(this).attr('class','active');
        $('#div1').find('div').eq( index ).css('display','block');
        loadData(index,function(data){
            $('#div1').find('div').eq(index).html(data);   
        });
    });
    loadData(0,function(data){
        $('#div1').find('div').eq(0).html(data);   
    });
    function loadData(num,fn){
        $.ajax({
            url : 'data.php?num=' + num,
            success : function(data){
                fn(data);
            }
        });
    }
});
</script>
</head>
<body>
<div id="div1">
    <input class="active" type="button" value="1" />
    <input type="button" value="2" />
    <input type="button" value="3" />
    <div style="display:block">正在加载...</div>
    <div>正在加载...</div>
    <div>正在加载...</div>
</div>
</body>
</html>
~~~

####$.get() ★★★★★

- 参数的作用

####$.post() ★★★★★

- 参数的作用

~~~ js
//第一个参数url，第二个是data，第三个是回调函数，第四个函数是datatype。基本上$.post()也是这种写法。如果获取失败了，可以调用error()这个方法。
$.get('user3.php', {name: "hello"}, function(data){
    console.log(data);
}, 'json').error(function(err){
    console.log(err);
});
~~~

###JQ插件

####$.browser()

- http://jquery.thewikies.com/browser/

~~~ html
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>用$.browser()插件判断浏览器地址</title>
    <script src="jquery-1.11.1.js"></script>
    <script src="http://jquery.thewikies.com/browser/jquery.browser.min.js"></script>
    <script>
        alert($.browser.name); //浏览器名称
        alert($.browser.version); //浏览器版本
        alert($.layout.name); //浏览器内核
        alert($.os.name); //操作系统
    </script>
</head>
<body>
</body>
</html>
~~~

####$.cookie()

- https://github.com/carhartl/jquery-cookie#readme

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>用$.browser()插件判断浏览器地址</title>
    <script src="jquery-1.11.1.js"></script>
    <script src="jquery.cookie.js"></script>
    <script>
        //$.cookie('name', 'hello'); //不设置过期时间的话，cookie都是临时存储的
        $.cookie('name', 'hello', {expires: 7}); //设置了cookie的过期时间为7天
        alert($.cookie('name'));
    </script>
</head>
<body>
</body>
</html>
~~~

####e-calendar

- http://www.jq22.com/jquery-info541
- 用法和JQ是相同的

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>用$.browser()插件判断浏览器地址</title>
    <script src="jquery-1.11.1.js"></script>
    <script src="http://demo.jq22.com/e-calendar-master/js/jquery.e-calendar.js"></script>
    <link rel="stylesheet" href="http://demo.jq22.com/e-calendar-master/css/jquery.e-calendar.css">
    <script>
        $(document).ready(function(){
            $('#calendar').eCalendar({
                weekDays: ['日', '一', '二', '三', '四', '五', '六'],
                textArrows: {previous: '-', next: '+'}
            });
        })
    </script>
</head>
<body>
    <h3>Hello World e-calendar!</h3>
    <div id="calendar"></div>
</body>
</html>
~~~

###UI组件

####jQuery UI

- http://jqueryui.com
- 交互、部件、特效、工具 
    - 配置参数、方法、自定义事件
    - css主题

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>jQuery UI</title>
    <script src="jquery-1.11.1.js"></script>
    <script src="jquery-ui.min.js"></script>
    <link rel="stylesheet" href="jquery-ui.min.css">
    <style>
        #div1 { width: 100px; height: 100px; background: red; position: absolute;}
    </style>
    <script>
        $(function(){
            #('#div1').draggable({ //配置参数
                cursor: 'move',
                axis: 'x',
                handle: 'p',
                start: function(){ //设置自定义事件
                    $(this).css('background', 'blue')
                }
            });
            $('input').click(function(){
                $('#div1').draggable('destroy'); //destroy方法，点击input之后，就不能拖拽了
            })
            //自定义事件还可以这样调用：
            /*
            $('#div1').on('dragstart', function(){ //这样写一般自定义事件前面要加上名字，这里不只写start，而是写个dragstart
                $(this).css('background', 'blue');
            })
            */
            $('#div1').find('p').addClass('active', 1000); //这个addClass也是jQuery UI中的特效
        })
    </script>
</head>
<body>
    <div id="div1">
        <p>aaaaaaa</p>
    </div>
    <input type="button" value="点击">
</body>
</html>
~~~

####jQuery EasyUI

- http://www.jeasyui.com
- 更强大的后台交互空间 
    - datagrid操作

###本课练习

- 优酷电影频道轮播图
- 评论载入数据（三个ajax的应用）

##2014年10月24日第五堂课 课后练习讲解（略）

##2014年10月26日第六堂课

###清空内容

####html("")

####empty() ★

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            $('#div1').empty();
        })
    </script>
</head>
<body>
    <div id="div1">div<span>span</span></div>
</body>
</html>
~~~

###删除节点

####remove()

####detach() ★

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            $('#div1').click(function(){
                alert(123);
            })
            /*
            var $div = $('#div1').remove(); //remove()函数返回的就是被删的元素
            $('body').append($div);
            //通过remove()删除再添加回来，只保留结构不保留操作行为
            */
            //detach()删除元素，但是保留之前元素的操作行为
            var $div = $('#div1').detach();
            $('body').append($div);
        })
    </script>
</head>
<body>
    <div id="div1">div</div>
    <hr>
</body>
</html>
~~~`

###获取文本

####text() ★

- 获取文本的特点

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            /*
            alert($('#div1').html()); //div<span>span</span>
            alert($('#div1').text()); //divspan text()只获取文本
            */
            //$('#div1').html('<h1>标题</h1>');
            //$('#div1').text('<h1>标题</h1>'); <h1>会当成文本打印在页面上
            alert($('div').text()); //text()可以获取一个集合所有文本节点的内容，这是与其他方法不同的
        })
    </script>
</head>
<body>
    <div id="div1">div<span>span</span></div>
    <div>div2</div>
    <div>div3</div>
    <hr>
</body>
</html>
~~~

###替换节点

####replaceWith() ★

####replaceAll() ★

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //用div替换span
            $('#span1').replaceWith($('#div1')); //原本的div1移到了span1的位置，而原本的span1不存在了
            //与replaceWith()对应的是replaceAll()。上面的写法也相当于如下：
            //$('#div1').replaceAll($('#span1'))
        })
    </script>
</head>
<body>
    <div id="div1">div</div>
    <hr>
    <span id="span1">span</span>
</body>
</html>
~~~

###事件扩展

####hover() ★★★

- mouseenter, mouseleave
- 与over, out的区别

**hover()方法**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        #div1 {width: 100px; height: 100px; background: red;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //hover()方法的两个参数是两个函数，第一个是mouseenter的操作；第二个是mouseleave的操作
            $('#div1').hover(function(){
                $(this).css('background', 'blue');
            }, function(){
                $(this).css('background', 'red');
            });
        })
    </script>
</head>
<body>
    <div id="div1">div</div>
</body>
</html>
~~~

**over和enter、out和leave的区别**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        #div1 {width: 200px; height: 200px; background: red; position: relative;}
        #div2 {width: 100px; height: 100px; background: blue; position: absolute; top: -100px; left: 0;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            /*
            //以下这种写法，鼠标移到蓝方块上再离开，会造成多次运动
            $('#div1').mouseover(function(){
                $('#div2').animate({top: 0});
            });
            $('#div1').mouseout(function(){
                $('#div2').animate({top: -100});
            });
            */
            /*
            //每次先清掉队列的处理方式也不是很理想
            $('#div1').mouseover(function(){
                $('#div2').stop().animate({top: 0});
            });
            $('#div1').mouseout(function(){
                $('#div2').stop().animate({top: -100});
            });
            */
            //mouseenter和mouseleave会让子元素不影响父元素
            $('#div1').mouseenter(function(){
                $('#div2').animate({top: 0});
            });
            $('#div1').mouseleave(function(){
                $('#div2').animate({top: -100});
            });
        })
    </script>
</head>
<body>
    <div id="div1">
        <div id="div2"></div>
    </div>
</body>
</html>
~~~

####focusin() ★

####focusout() ★

- 与focus, blur区别

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        #div1 {width: 200px; height: 200px; background: red; position: relative;}
        #div2 {width: 100px; height: 100px; background: blue; position: absolute; top: -100px; left: 0;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //focus和blur不支持冒泡，只能加给能够获取光标的元素
            /* div是没有focus事件的，点击input也不可能冒泡到div上来
            $('#div1').on('focus', function(){
                alert(123);
            })
            */
            //focusin和focusout这两个事件支持冒泡
            //下面代码，点击input的时候，就会冒泡到div上执行代码
            $('#div1').on('focusin', function(){
                alert(123);
            })
        })
    </script>
</head>
<body>
    <div id="div1">
        <input type="text">
    </div>
</body>
</html>
~~~

####one() ★

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        #div1 {width: 200px; height: 200px; background: red; position: relative;}
        #div2 {width: 100px; height: 100px; background: blue; position: absolute; top: -100px; left: 0;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //one()事件，只能触发一次
            $('#div1').one('focusin', function(){
                alert(123);
            })
            /*
            //如果不用one，也可以实现只触发一次，可以写成下面的形式：
            $('#div1').on('focusin', function(){
                alert(123);
                $('#div1').off('focusin');
            })
            */
        })
    </script>
</head>
<body>
    <div id="div1">
        <input type="text">
    </div>
</body>
</html>
~~~

####on() ★★★★★

- 源码分析几大参数
- 获取原生event 
    - originalEvent
    - changedTouches
- 自定义事件

**源码分析几大参数**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        #div1 {width: 200px; height: 200px; background: red; position: relative;}
        #div2 {width: 100px; height: 100px; background: blue; position: absolute; top: -100px; left: 0;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //on()有五个参数，有一个是专门针对one()方法内部使用的
            $('#div1').on('click', {name: 'hello'}, function(ev){
                console.log(ev.data.name); //ev.data就对应着on()的json参数
            })
            $('#div1').on('click', 'span', {name: 'hello'}, function(){
                alert(123); //在on()中添加了一个元素的话，就与事件委托是一样的，相当于筛选条件。
            })
            /*
            //上面那种写法就相当于：
            $('#div1').delegate('span', 'click', function(){
                alert(123);
            })
            */
        })
    </script>
</head>
<body>
    <div id="div1">
        <span>span</span>
    </div>
</body>
</html>
~~~

**转成原生的event对象**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        #div1 {width: 200px; height: 200px; background: red; position: relative;}
        #div2 {width: 100px; height: 100px; background: blue; position: absolute; top: -100px; left: 0;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //jQuery中的ev不是原生的event对象
            //要获得原生的event对象用originalEvent
            $('#div1').on('touchstart', function(ev){ //touchstart是移动端的触摸的一个事件
                 alert(ev.changedTouches); //jQuery中这样写，弹出的是undefined，因为jQuery中的event对象是找不到这个事件对象的属性的
                 alert(ev.originalEvent.changedTouches); //转换成原生的event对象就可以找到这个值了
            })
        })
    </script>
</head>
<body>
    <div id="div1">
        <span>span</span>
    </div>
</body>
</html>
~~~

**自定义事件**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>自定义事件</title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //实现在图片上滚轮向下，图片缩小；滚轮向上，图片放大
            $('#img1').on('zoomIn', function(){ //缩小
                $(this).css('width', '100');
            });
            $('#img1').on('zoomOut', function(){ //放大
                $(this).css('width', '500');
            });
            //$('#img1').trigger('zoomIn'); //自定义事件的触发是通过trigger来做
            $('#img1').on('DOMMouseScroll',function(ev){
                //alert(ev.originalEvent.detail); //向下滚大于0；向上滚小于0
                if(ev.originalEvent.detail > 0){
                    $(this).trigger('zoomIn');
                }
                else{
                    $(this).trigger('zoomOut');
                }
            });
        })
    </script>
</head>
<body>
    <img src="001.jpg" id="img1">
</body>
</html>
~~~

####triggerHandler() ★

- 与trigger()的区别

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>自定义事件</title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //trigger() 可以触发事件的默认行为
            //triggerHandler() 不会触发事件自带的默认行为，只会出发自定义的操作
            $('#input1').on('focus', function(){
                this.style.background = 'red';
            })
            $('#input2').on('click', function(){
                //$('#input1').trigger('focus'); //#input1自动获取光标
                $('#input1').triggerHandler('focus'); //#input1没有自动获取光标
            })
        })
    </script>
</head>
<body>
    <input type="text" id="input1">
    <input type="button" id="input2" value="点击">
</body>
</html>
~~~

####event对象

- stopImmediatePropagation() ★ 
    - 与stopPropagation()的区别
    - 注意顺序的问题
- which的鼠标值 
    - 注意加到mousedown上

**stopImmediatePropagation()**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>自定义事件</title>
    <style>
        #div1 {width: 100px; height: 100px; background: red;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            $('#div1').on('click', function(){
                alert(123);
            })
            $('#span1').on('click', function(ev){
                //ev.stopPropagation(); //只会阻止父级
                ev.stopImmediatePropagation(); //除了阻止父级，还会阻止本身的事件操作
                //注意，要阻止的本身的事件操作要写到这句话下面才可以
            })
            $('#span1').on('click', function(){
                alert(456);
            })
        })
    </script>
</head>
<body>
    <div id="div1">
        <span id="span1">span</span>
    </div>
</body>
</html>
~~~

**鼠标的键值**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>自定义事件</title>
    <style>
        #div1 {width: 100px; height: 100px; background: red;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            $('#span1').on('mousedown', function(ev){
                //alert(ev.which); //点击鼠标左键弹1、滚轮弹2、右键弹3
                //要获得鼠标的键值，要用mousedown或mouseup事件来，而不能用click，因为click不仅是由鼠标来触发的
            })
        })
    </script>
</head>
<body>
    <div id="div1">
        <span id="span1">span</span>
    </div>
</body>
</html>
~~~

####ready()

- 与$(function(){})的关系
- 与原生window.onload的区别
- ready的问题

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>自定义事件</title>
    <style>
        #div1 {width: 100px; height: 100px; background: red;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        /*
        $(function(){
        })
        */
         //上面这种写法就相当于：
         /*
         $(document).ready(function(){
         })
         */
         /*
        $(function(){
            //等DOM加载完就执行 有图片加载的时候，需要获取img的宽、高等数据要小心
        })
        和
        $(window).load(function(){
            //等整个页面加载完才执行 
        })
        */
        $(function(){ //可以通过img的load方法来解决
            $('img').load(function(){
                alert($('img').width());
            });
        })
    </script>
</head>
<body>
    <img src="1.png" alt="">
</body>
</html>
~~~

###JQ的截至操作

####nextUntil() ★

####prevUntil() ★

####parentsUntil() ★

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>自定义事件</title>
    <style>
        #div1 {width: 100px; height: 100px; background: red;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //$('#span1').parents().css('border', '1px solid blue');
            $('#span1').parentsUntil('body').css('border', '1px solid blue'); //找到body就不再找了，而且body也不包括
            //nextUntil() 下面兄弟节点的截止位置
            //prevUntil() 上面兄弟节点的截止位置
        })
    </script>
</head>
<body>
    <div id="div1">
        <p>
            <span id="span1">span</span>
        </p>
    </div>
</body>
</html>
~~~

###数据缓存

####data() ★★★

- prop() ★★★
- 与attr()三者的区别
- removeAttr(), removeProp(), removeData()

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>自定义事件</title>
    <style>
        #div1 {width: 100px; height: 100px; background: red;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //data() 数据缓存两个参数
            $('#div1').data('name', 'hello'); //设置缓存数据到元素身上
            alert($('#div1').data('name')); //获取缓存数据
            //data() 把数据存在了一个大的集合中，放到了jQuery库的源码当中，并没有直接把数据存在元素身上，而是间接设置上去的。这种写法可以防止内存泄露。要想在元素身上缓存大量数据，用data()
            /*
            $('#div1').attr('name', 'hello'); 
            alert($('#div1').attr('name')); 
            */
            //attr是通过在元素身上添加自定义属性和自带属性，是直接往DOM某个元素本身身上设置
            //prop()与attr()略有不同：attr是通过原生的setAttribute和getAttribute来进行添加和设置的；而prop()是根据原生的点“.”或中括号“[]”来进行设置的。
            //oDiv.index = i; 或 oDiv['index'] = i; 这都是用prop()设置的
        })
    </script>
</head>
<body>
    <div id="div1">
        aaaaaa
    </div>
</body>
</html>
~~~

**attr()和prop()的选择**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>自定义事件</title>
    <style>
        #div1 {width: 100px; height: 100px; background: red;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            /*
            //原生的方法
            var aInput = document.getElementsByTagName('input');
            aInput[0].onclick = function(){
                for(var i=1; i<aInput.length; i++){
                    aInput[i].checked = true;
                }
            }
            */
            var bBtn = true;
            /*用attr设置出现了问题
            $('input[type=button]').click(function(){
                if(bBtn){
                    $('input[type=checkbox]').attr('checked', true);
                } else {
                    $('input[type=checkbox]').attr('checked', false);
                }
                bBtn = !bBtn;
            });
            */
            //用prop就没有问题。attr和prop的选择，可以参考原生的做法。如果原生是用.或[]设置的，那么jQuery来写就考虑用prop()的方法
            $('input[type=button]').click(function(){
                if(bBtn){
                    $('input[type=checkbox]').prop('checked', true);
                } else {
                    $('input[type=checkbox]').prop('checked', false);
                }
                bBtn = !bBtn;
            });
        })
    </script>
</head>
<body>
    <input type="button" value="全选">
    <input type="checkbox">
    <input type="checkbox">
    <input type="checkbox">
</body>
</html>
~~~

###JSON形式的设置

- on()
- css()
- attr()

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>json写法</title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //css()的json写法
            $('div').css({
                width: '100px',
                height: '100px',
                background: 'red'
            });
            /*
            //on()的json写法
            $('div').on({
                click: function(){},
                mouseover: function(){}
            })
            */
        })
    </script>
</head>
<body>
    <div></div>
</body>
</html>
~~~

###回调形式的设置

- addClass()
- html()
- val()

**addClass()**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>回调形式</title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            $('div').addClass(function(i, oldClass){
                console.log(i); //当前div的索引值
                console.log(oldClass); //div之前的class
                //上面的代码执行完毕，在控制台打印出来的就是：
                //0
                //box div1
                //1
                //(空字符串)
                //2
                //(空字符串)
                return 'box'+(i+1); //可以利用addClass()的回调，给三个div分别添加class：box1、box2和box3。注意此处的return
            });
        })
    </script>
</head>
<body>
    <div class="box div1">div</div>
    <div>div</div>
    <div>div</div>
</body>
</html>
~~~

###工具方法

####$.merge() ★

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            var a = [1, 2, 3];
            var b = [4, 5, 6];
            var c = $.merge(a, b); //$.merge只能是两个参数
            console.log(c); //[1, 2, 3, 4, 5, 6]
        })
    </script>
</head>
<body>
</body>
</html>
~~~

####$.map() ★

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //$.map(数组，回调)
            var arr = ['a', 'b', 'c'];
            arr = $.map(arr, function(val, i){
                console.log(val); //值
                console.log(i); //索引
                return val + i //数组就变成['a0', 'b1', 'c2']
                //return 'hello' //数组变成['hello', 'hello', 'hello']
            })
            console.log(arr);
        })
    </script>
</head>
<body>
</body>
</html>
~~~

####$.grep() ★

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            var arr = [1, 5, 3, 8, 2];
            arr = $.grep(arr, function(val, i){
                return val > 4; //返回值大于4的数 为真就保留，为假就剔除
            })
            console.log(arr); //[5, 8]
        })
    </script>
</head>
<body>
</body>
</html>
~~~

####$.unique() ★

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //$.unique() 针对dom节点的去重方法，对数组不起作用
            var aDiv = $('div').get(); //要转成原生
            var arr = [];
            for(var i=0; i<aDiv.length; i++){
                arr.push(aDiv[i]);
            }
            for(var i=0; i<aDiv.length; i++){
                arr.push(aDiv[i]);
            } //循环了两次，因此arr里面出现了一些重复的
            arr = $.unique(arr); //去掉了重复的
            console.log(arr); 
        })
    </script>
</head>
<body>
    <div class="box">div</div>
    <div>div</div>
    <div>div</div>
</body>
</html>
~~~

####$.inArray() ★

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //$.inArray() 类似于indexOf()的作用
            var arr = ['a', 'b', 'c', 'd'];
            console.log($.inArray('b', arr)); //'b'在arr中的位置是1，如果没有出现过的就返回-1
        })
    </script>
</head>
<body>
    <div class="box">div</div>
    <div>div</div>
    <div>div</div>
</body>
</html>
~~~

####$.makeArray() ★

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //$.makeArray() 把不是数组的转成数组
            var aDiv = document.getElementsByTagName('div');
            //aDiv.push() //会报错，因为aDiv不是数组
            aDiv = $.makeArray(aDiv);
            aDiv.push(); //这次就不报错了
            console.log(aDiv);
            var aString = 'hello';
            aString = $.makeArray(aString);
            console.log(aString);
        })
    </script>
</head>
<body>
    <div class="box">div</div>
    <div>div</div>
    <div>div</div>
</body>
</html>
~~~

####$.trim() ★★★

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            var str = '    hello   ';
            alert('(' + str + ')');
            alert('(' + $.trim(str) + ')');
        })
    </script>
</head>
<body>
    <div class="box">div</div>
    <div>div</div>
    <div>div</div>
</body>
</html>
~~~

###ajax扩展

####辅助

#####$.param() ★★★

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //'key = value$key=value$key=value' ajax中通过这种形式传到后台
            var obj = {"name": "hello", "age": "20"};
            obj = $.param(obj); //自动转成上述字符串
            console.log(obj); 
            /*
            $.ajax({
                data: {"name": "hello", "age": "20"} //后台会自动转成上面拼接的形式
            });
            */
        })
    </script>
</head>
<body>
    <div class="box">div</div>
    <div>div</div>
    <div>div</div>
</body>
</html>
~~~

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            var obj = [{name: 'hello', value: '20'}]; //注意这里加了中括号
            obj = $.param(obj);
            console.log(obj); //hello=20 name和value对应，这里就合成了一个整体
            var obj1 = [{name: 'hello', age: '20'}]; //注意这里加了中括号
            obj1 = $.param(obj1);
            console.log(obj1); //hello= 因为这里name和age无法对应，所以得不到hello=20
        })
    </script>
</head>
<body>
    <form action="">
        <input type="text" name="a" value="1">
        <input type="text" name="b" value="2">
        <input type="text" name="c" value="3">
    </form>
</body>
</html>
~~~

#####serialize() ★★★

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //serialize()是针对form表单的实例方法
            var a = $('form').serialize(); //注意：一定是针对form中的name和value的形式
            console.log(a); //a就处理为字符串："a=1&b=2&c=3"
            $.ajax({
                data: a //通过以上操作，在调用ajax的时候就可以直接调用这个a了
            })
        })
    </script>
</head>
<body>
    <form action="">
        <input type="text" name="a" value="1">
        <input type="text" name="b" value="2">
        <input type="text" name="c" value="3">
    </form>
</body>
</html>
~~~

#####serializeArray() ★★★

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //serializeArray()是针对form表单中的name和value的实例方法
            var a = $('form').serializeArray();
            console.log(a); //a就处理成[{name="a", value="1"}, {name="b", value="2"}, {name="c", value="3"}]
        })
    </script>
</head>
<body>
    <form action="">
        <input type="text" name="a" value="1">
        <input type="text" name="b" value="2">
        <input type="text" name="c" value="3">
    </form>
</body>
</html>
~~~

####快捷方法

#####load() ★

- 筛选的功能

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //load() 给元素里面添加东西
            //$('#div1').load('data.html', function(){}); //回调函数是加载后出发的函数，data.html的内容会直接被添加到指定的元素里面
            $('#div1').load('data.html .box', function(){}); //该函数还有筛选功能，在地址后面加个空格加上.box，那么在data.html中的.box的内容才能被加到div中来
        })
    </script>
</head>
<body>
    <div id="div1"></div>
</body>
</html>
~~~

#####$.getScript() ★

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            // $.getScript() 动态请求js文件
            $('#div1').click(function(){
                $.getScript('data.js', function(){});  //去动态加载data.js文件 文件加载完就会执行里面的代码。data.js加载完成之后，执行回调函数
            })
        })
    </script>
</head>
<body>
    <div id="div1">aaaa</div>
</body>
</html>
~~~

#####$.getJSON ★

- JSONP，不受同源影响
- 建议直接使用问号

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            // $.getJson() 动态请求json或JsonP
            //直接用$.getJSON，我们就不需要再通过设置dataType: json了
            $.getJSON('data.php', function(data){
                console.log(data);
            }); //data.php返给我们的是一个json格式
        })
    </script>
</head>
<body>
    <div id="div1">aaaa</div>
</body>
</html>
~~~

**jsonp的形式**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            // $.getJson() 动态请求json或JsonP
            //直接用$.getJSON，我们就不需要再通过设置dataType: json了
            $.getJSON('data.php', function(data){
                console.log(data);
            }); //data.php返给我们的是一个json格式
            //针对JSONP
            $.getJSON('data.php?callback=?', function(data){ //data.php返回的是jsonp的形式，我们就可以后面添上callback=? 注意其中callback是key值，而问号?是value值。一旦用getJSON时，一定要是用callback=?的。如果给callback指定了名称，那么返回的是字符串形式，并不是json形式，在getJSON里面就解析不了，所以就只能走error。所以在$.getJSON()里面给callback命名是没有意义的，一定要是用?才可以自动解析
                console.log(data);
            }).error(function(err){
                console.log(err);
            });
            $.ajax({ //在使用ajax的时候，可以给callback自定义名称，例如下面定义了“show”
                url:'data.php?callback=show',
                success: function(data){
                    //返回的数据就是一个类似"show({name: 'hello'})"的字符串，然后再后续处理进行使用
                }
            })
            //另外如果在$.ajax()中设置了datatype为'jsonp'，那么在url的地方是不需要加callback的，因为它会自动添加好
        })
    </script>
</head>
<body>
    <div id="div1">aaaa</div>
</body>
</html>
~~~

####默认配置

#####$.ajaxSetup() ★

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //如果有很多ajax，那么可以利用$.ajaxSetup()来进行默认设置
            $.ajaxSetup({
                type: 'POST' //那么所有的ajax传输类型都改为post了
            });
        })
    </script>
</head>
<body>
    <div id="div1">aaaa</div>
</body>
</html>
~~~

####全局事件

- 加到document上，参数的意义
- $.ajaxStart() ★
- $.ajaxStop() ★
- $.ajaxSuccess() ★
- $.ajaxError() ★
- $.ajaxComplete() ★
- $.ajaxSend() ★

####属性 ★

- Global, Context
- JSONP, jsonpCallback
- Cache, Timeout
- processData
- contentType

**ajax参考：**

- http://www.cnblogs.com/heyuquan/archive/2013/05/13/js-jquery-ajax.html

##2014年10月29日第七堂课

###防止库之间冲突 $.noConflict() ★

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        var J = $.noConflict();
        var $ = 123;
        //后面就可以用J代替$或者jQuery来直接用了
        J().css();
        J.trim();
    </script>
</head>
<body>
</body>
</html>
~~~

###遍历 $.each() ★★★

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //$().each() 只能针对jQuery的集合
            //$.each() 工具方法，可以针对原生的集合，还针对数组和json都可以
            var arr = ['a', 'b', 'c'];
            var obj = {'name': 'hello', 'age': '20'}
            $.each(arr, function(i, val){
                console.log(i);
                console.log(val);
            })
            $.each(obj, function(i, val){
                console.log(i);
                console.log(val);
            })
        })
    </script>
</head>
<body>
    <div></div>
    <div></div>
    <div></div>
</body>
</html>
~~~

###后退链式操作 end() ★

###后退添加链式操作 addBack() ★

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //end() 回到上一级
            //$('div').next().css('background', 'red').end().css('color', 'blue');
            //addBack() 不仅返回上一层，还会包含自己本身
            //$('div').next().css('background', 'red').addBack().css('color', 'blue');
            //add() 添加到集合中
            $('div').add('span').css('background', 'red').addBack().css('color', 'blue');
        })
    </script>
</head>
<body>
    <div>div</div>
    <span>span</span>
</body>
</html>
~~~

###JQ中的队列 ★

####\.queue().dequeue()

- 概念与参数意义
- 队列名称

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //$.queue() 三个参数：队列添加到哪个元素身上；队列的名字；第三个参数是一个函数
            //$.dequeue() 两个参数：元素和队列名字
            //JQ中的队列，存储的都是函数
            //JQ的队列，当进行出队的操作的时候，会自动执行相应的函数
            function a(){
                alert(1);
            }
            function b(){
                alert(2);
            }
            function c(){
                alert(3);
            }
            $.queue(document, 'miaov', a);
            $.queue(document, 'miaov', b);
            $.queue(document, 'miaov', c);
            $.dequeue(document, 'miaov'); //弹1
            $.dequeue(document, 'miaov'); //弹2
            $.dequeue(document, 'miaov'); //弹3
        })
    </script>
</head>
<body>
    <div>div</div>
    <span>span</span>
</body>
</html>
~~~

####queue() dequeue()

- 源码分析运动队列
- 默认队列名fx
- 队列的具体应用

**基本使用**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            function a(){
                alert(1);
            }
            function b(){
                alert(2);
            }
            function c(){
                alert(3);
            }
            $(document).queue('miaov', a);
            $(document).queue('miaov', b);
            $(document).queue('miaov', c);
            $(document).dequeue('miaov'); //弹1
            $(document).dequeue('miaov'); //弹2
        })
    </script>
</head>
<body>
    <div>div</div>
    <span>span</span>
</body>
</html>
~~~

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        div {width: 100px; height: 100px; background: red; position: absolute;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        //JQ中，animate的队列名称是'fx'
        $(function(){
            function a(){
                $('div').css('background', 'blue');
                $('div').dequeue('fx'); //如果不写这句话的话，队列就卡在这里了，没法往下执行了
            }
            $('div').animate({width: 200});
            $('div').queue('fx', a);
            $('div').animate({height: 200});
            $('div').animate({left: 200});
        })  
    </script>
</head>
<body>
    <div>div</div>
</body>
</html>
~~~

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        div {width: 100px; height: 100px; background: red; position: absolute;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        //JQ中，animate的队列名称是'fx'
        $(function(){
            $('div').animate({width: 200});
            //$('div').delay(2000); 下面的操作就相当于这一句的操作
            $('div').queue('fx', function(){
                setTimeout(function(){
                    $('div').dequeue();
                }, 2000)
            })
            $('div').animate({height: 200});
            $('div').animate({left: 200});
        })  
    </script>
</head>
<body>
    <div>div</div>
</body>
</html>
~~~

###JQ中的回调对象 ★

####$.Callbacks()

- 基本概念与用法 
    - add
    - remove
    - fire
- 应用场景
- 四大参数 
    - once
    - memory
    - unique
    - stopOnFalse

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        div {width: 100px; height: 100px; background: red; position: absolute;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            function a(){
                alert(1);
            }
            function b(){
                alert(2);
            }
            function c(){
                alert(3);
            }
            var cb = $.Callbacks(); //回调对象
            cb.add(a); //a添加到回调对象的集合里面
            cb.fire(); //fire就是触发 弹出1
            cb.add(b); 
            cb.fire(); //弹出1和2
            cb.add(c);
            cb.remove(b);
            cb.fire(); //弹出1和3
        })  
    </script>
</head>
<body>
</body>
</html>
~~~

**用回调对象来解决作用域的问题**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            var cb = $.Callbacks();
            function a(){
                alert(1);
            }
            (function(){
                function b(){
                    alert(2);
                }
                cb.add(a);
                cb.add(b);
            })();
            //a(); //弹1
            //b(); //b这个函数是找不到的，因为作用域里面没它
            cb.fire(); //弹1、2
        })  
    </script>
</head>
<body>
</body>
</html>
~~~

**once**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        div {width: 100px; height: 100px; background: red; position: absolute;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            function a(){
                alert(1);
            }
            function b(){
                alert(2);
            }
            function c(){
                alert(3);
            }
            //参数 once：只能触发一次
            var cb = $.Callbacks('once');
            cb.add(a);
            cb.add(b);
            cb.fire(); //弹1、2
            cb.fire(); //因为添加了参数once，所以前面触发过一次之后，这里不再触发
        })  
    </script>
</head>
<body>
</body>
</html>
~~~

**memory**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        div {width: 100px; height: 100px; background: red; position: absolute;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            function a(){
                alert(1);
            }
            function b(){
                alert(2);
            }
            function c(){
                alert(3);
            }
            //参数 memory：不管前后添加的都一起出发
            var cb = $.Callbacks('memory');
            cb.add(a);
            cb.add(b);
            cb.fire(); //弹1、2、3，因为参数memory，让触发时不管前面后面add的都触发
            cb.add(c); 
        })  
    </script>
</head>
<body>
</body>
</html>
~~~

**unique**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        div {width: 100px; height: 100px; background: red; position: absolute;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            function a(){
                alert(1);
            }
            function b(){
                alert(2);
            }
            function c(){
                alert(3);
            }
            //参数 unique：去重功能
            var cb = $.Callbacks('unique');
            cb.add(a);
            cb.add(a);
            cb.add(a);
            cb.add(b);
            cb.fire(); //弹1、2，而不是弹1,1,1,2
        })  
    </script>
</head>
<body>
</body>
</html>
~~~

**stopOnFalse**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        div {width: 100px; height: 100px; background: red; position: absolute;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            function a(){
                alert(1);
            }
            function b(){
                alert(2);
                return false;
            }
            function c(){
                alert(3);
            }
            //参数 unique：去重功能
            var cb = $.Callbacks('stopOnFalse');
            cb.add(a);
            cb.add(a);
            cb.add(b);
            cb.add(c);
            cb.fire(); //弹1,1,2 不谈3，因为在b里面碰到了false就不继续执行后面的函数c了
        })  
    </script>
</head>
<body>
</body>
</html>
~~~

**参数的组合使用**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        div {width: 100px; height: 100px; background: red; position: absolute;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            function a(){
                alert(1);
            }
            function b(){
                alert(2);
                return false;
            }
            function c(){
                alert(3);
            }
            //回调对象的参数可以组合使用
            var cb = $.Callbacks('once memory');
            cb.add(a);
            cb.add(a);
            cb.add(b);
            cb.fire(); //弹1,1,2,3   
            cb.add(c);
            cb.fire(); //什么也不弹
        })  
    </script>
</head>
<body>
</body>
</html>
~~~

###JQ中的延迟对象 ★★★

####$.Deferred()

- 基本概念与用法 
    - 与Callbacks()对比学习
    - 应用场景
    - 状态的定义
    - 状态的映射 
        - resolve, done
        - reject, fail
    - ajax中的应用 
        - $.when()
- 利用状态的应用

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        div {width: 100px; height: 100px; background: red; position: absolute;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            /*
            setTimeout(function(){
                alert(1);
            }, 1000);
            alert(2);
            */
            /*
            setTimeout(function(){
                alert(1);
                alert(2);
            }, 1000);
            */
            /*
            var cb = $.Callbacks();
            setTimeout(function(){
                alert(1);
                cb.fire();
            }, 1000);
            cb.add(function(){
                alert(2);
            })
            */
            //可以看出，用上面的cb和下面的dfd是非常相像的
            //一秒钟之后先弹1，再弹2
            //resolve对应done
            //reject对应fail
            var dfd = $.Deferred();
            setTimeout(function(){
                alert(1);
                //dfd.resolve(); //解决
                dfd.reject(); //未解决
            }, 1000);
            //dfd.done(function(){ //成功
            dfd.fail(function(){ //失败
                alert(2);
            })
        })  
    </script>
</head>
<body>
</body>
</html>
~~~

**延迟对象在ajax中的应用**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        div {width: 100px; height: 100px; background: red; position: absolute;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            /*
            $.ajax({
                url: 'xxx.php',
                success: function(){
                },
                error: function(){
                }
            });
            */
            $.ajax('xxx.php').done(function(){}).fail(function(){}); //这一句与上面的写法是一回
        })  
    </script>
</head>
<body>
</body>
</html>
~~~

**延迟对象的状态会被保持住**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        div {width: 100px; height: 100px; background: red; position: absolute;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            function a(){
                alert(1);
            }
            //点击第一次，延迟两秒钟弹；以后再点就立即弹
            /*
            var bBtn = true;
            $('input').click(function(){
                if(bBtn){
                    bBtn = false;
                    setTimeout(a, 2000);
                } else {
                    a();
                }
            })
            */
            //用延迟对象来做
            //第一次执行click的时候，a函数加到了延迟对象里面，然后延迟两秒钟，见到resolve之后，done里面的函数执行
            //第二次再点击的时候，因为前面dfd的状态已经变成resolve解决了，所以就可以直接执行done了
            //延迟对象的状态会保持住
            var dfd = $.Deferred();
            $('input').click(function(){
                setTimeout(function(){
                    dfd.resolve();
                }, 2000);
                dfd.done(a);
            })
        })  
    </script>
</head>
<body>
<input type="button" value="点击">
</body>
</html>
~~~

**$.when**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        div {width: 100px; height: 100px; background: red; position: absolute;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            /*
            //xxx获取成功做一件事、yyy获取成功做一件事
            $.ajax('xxx.php').done(function(){});
            $.ajax('yyy.php').done(function(){});
            */
            //等xxx和yyy都成功之后，再进行一个回调处理
            $.when($.ajax('xxx.php'), $.ajax('yyy.php')).done(function(){});
            //注意$.ajax('xxx.php')这种形式，返回的就是一个延迟对象
        })  
    </script>
</head>
<body>
<input type="button" value="点击">
</body>
</html>
~~~

###JQ源码架构

- 基于面向对象程序 
    - 实例方法
    - 静态方法
    - this对象格式
    - 下标

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>ajax</title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            $('div').css('background', 'red'); //对象.css(...)
            $('div').html(); //对象.html();
            //var arr = new Array();
            //arr.push();
            //arr.sort();
        //----------源码中----------
            function $(selector){
                return new Jquery();
            }
            function Jquery(selector){ //构造函数
                //selector -> 获取相对应的元素
                //this == $('div') //等价的
                /*
                this = { //this中存储的元素都是原生的
                    0: div1,
                    1: div2,
                    2: div3,
                    length: 3
                }
                */
            }
            Jquery.prototype.css = function(attr, value){ //attr -> background; value -> red
                for(var i=0; i<this.length; i++){
                    this[i].style[attr] = value;
                }
            }
            Jquery.prototype.html = function(){
            }
        });
    </script>
</head>
<body>
    <div>div1</div>
    <div>div2</div>
    <div>div3</div>
</body>
</html>
~~~

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>ajax</title>
    <style>
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //$('div').css('background', 'red');
            $('div')[1].style.background = 'red'; //理解了原生，就知道通过这种方式就可以找到div2了
            $('div').get(1).style.background = 'red'; //这个get就相当于上面的这种写法
            /*
            $('div').length //.length其实是$('div')这个jquery对象的json中的一个属性
            $('div')就是下面这样一个json
            {
                0: div1,
                1: div2,
                2: div3,
                length: 3
            }
            */
        });
    </script>
</head>
<body>
    <div>div1</div>
    <div>div2</div>
    <div>div3</div>
</body>
</html>
~~~

**实例方法和静态方法**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        div {width: 100px; height: 100px; background: red; position: absolute;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        //工具方法如：
        $.trim();
        $.type();
        //以上这些都是直接将方法挂载到$上，而$在源码中是一个函数，方法挂载在函数上也是可以的，因为函数也是对象。
        //----------源码中----------
            function $(selector){
                return new Jquery();
            }
            //下面两行是工具方法的扩展。面向对象当中，对函数扩展的方法叫作“静态方法”
            $.trim = function(){};
            $.type = function(){};
            function Jquery(selector){ 
            }
            //面向对象当中，在原型prototype上的方法叫做“实例方法”
            Jquery.prototype.css = function(attr, value){ 
            }
            Jquery.prototype.html = function(){
            }
        });
    </script>
</head>
<body>
</body>
</html>
~~~

###JQ插件编写 ★★★

- $.fn.extend() 
    - this指向
- $.extend()
- 编写插件基本格式 
    - 分析jQuery.e-calendar
    - 配置参数
    - 方法
    - 自定义事件
- 实例：编写选项卡插件

**$.extend()与$.fn.extend()**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        div {width: 100px; height: 100px; background: red; position: absolute;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $.extend(a); //在$.extend()里面只写一个参数的时候，就是说这个a要往jQuery源码本身身上添加 工具方法（静态方法）
        $.fn.extend(); //JQ方法（实例方法）
        //----------源码中----------
            function $(selector){
                return new Jquery();
            }
            $.trim = function(){};
            $.type = function(){};
            //上面两行的写法与下面这个$.extend的写法是一回事
            $.extend({
                trim: function(){},
                type: function(){}
            })
            function Jquery(selector){ 
            }
            Jquery.prototype.css = function(attr, value){ 
            }
            Jquery.prototype.html = function(){
            }
            //上面两个加载prototype上的实例方法也可以通过下面的$.fn.extend()来实现，两者是一回事
            $.fn.extend({
                css: function(){},
                html: function(){}
            })
        });
    </script>
</head>
<body>
</body>
</html>
~~~

**扩展工具方法**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        div {width: 100px; height: 100px; background: red; position: absolute;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //$.trim是去掉左右空格，现在扩展一个只去左边空格的方法
            $.extend({
                leftTrim: function(str){
                    //this : 工具方法中 this与$等价
                    return str.replace(/^\s+/g,'');
                }
            });
            var str = '   hello  ';
            alert('(' + $.leftTrim(str) + ')');
        })
    </script>
</head>
<body>
</body>
</html>
~~~

**扩展实例方法**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        div {width: 100px; height: 100px; background: red; position: absolute;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        $(function(){
            //$('div').size(); 自己实现以下这个size()的功能
            $.fn.extend({
                size2: function(){
                    //实例方法中：this 相当于调用这个方法的 $('div')
                    return this.length;
                }
            });
            //extend方法可以扩展多个方法，如果只扩展一个实例方法，也可以写成这样：$.fn.size2 = function(){};
            alert($('div').size2());
        })
    </script>
</head>
<body>
    <div>div1</div>
    <div>div2</div>
    <div>div3</div>
</body>
</html>
~~~

**选项卡插件**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>编写选项卡的插件</title>
    <style>
        #tab div {width: 200px; height: 200px; border: 1px #000 solid; display: none;}
        #tab .active {background: red;}
    </style>
    <script src="jquery-1.11.1.js"></script>
    <script>
        //自定义事件：
        //自定义一个切换前的事件和切换后的事件beforeChange和afterChange
        $(function(){
            //$('#tab').tabs();
            $('#tab').tabs({
                heads: ['体育', '娱乐', '新闻', '视频'],
                bodies: ['体育1111', '娱乐123123', '新闻ffff', '视频fffggg'],
                events: 'mouseover'
            });
            $('#tab').on('beforeChange', function(){
                alert($('#tab').find('div:visible').html());
            }); //把切换前的div内容弹出来
            $('#tab').on('afterChange', function(){
                alert($('#tab').find('div:visible').html());
            }); //把切换后的div内容弹出来
        });
        (function($){
            var defaults = {
                heads: ['1', '2', '3'],
                bodies: ['1111111', '2222222', '3333333'],
                events: 'click'
            };
            var settings = {};
            var $parent = null;
            function fnTab(options){
                $parent = this; //$parent就是#tabs
                settings = $.extend(settings, defaults, options); //有配置走配置，没配置走默认
                create();
                bind();
            }
            function create(){ //创建布局
                for(var i=0; i<settings.heads.length; i++){
                    var $input = $('<input type="button" value="' + settings.heads[i] + '">');
                    if(i == 0){
                        $input.attr('class', 'active');
                    }
                    $parent.append($input);
                }
                for(var i=0; i<settings.bodies.length; i++){
                    var $div = $('<div>' + settings.bodies[i] + '</div>');
                    if(i == 0){
                        $div.css('display', 'block');
                    }
                    $parent.append($div);
                }
            }
            function bind(){
                $parent.find('input').on(settings.events, function(){
                    //这里就是改变前beforeChange
                    $parent.trigger('beforeChange');
                    $parent.find('input').attr('class', '');
                    $(this).attr('class', 'active');
                    $parent.find('div').css('display', 'none');
                    $parent.find('div').eq($(this).index()).css('display', 'block');
                    //这里就是改变后的afterChange
                    $parent.trigger('afterChange');
                })
            }
            $.fn.extend({
                tabs: fnTab
            })
        })(jQuery);
    </script>
</head>
<body>
    <div id="tab">
        <!-- <input class="active" type="button" value="1">
        <input type="button" value="2">
        <input type="button" value="3">
        <div style="display: block">1111111</div>
        <div>2222222</div>
        <div>3333333</div> -->
    </div>
</body>
</html>
~~~

##2014年11月1日第八堂课


###Sizzle选择器 ★★★

- 介绍与实现接口
    - $() ->  find()
- 通用选择
    - \*
- 层级选择
    - \>
    - \+
    - ~
- 基本筛选
    - :animated
    - :eq()
    - :even
    - :odd
    - :first
    - :last
    - :gt()
    - :lt()
- 内容筛选
    - :contains()
    - :empty
    - :parent
- 可见性筛选
    - :hidden
    - :visible
- 子元素筛选
    - :first-child
    - :last-child
    - :first-of-type
    - :last-of-type
    - :nth-child()
    - :nth-of-type()
    - :only-child
    - :only-of-type
- 表单筛选
    - :button
    - :checkbox
    - :radio
    - :checked
    - :disabled
    - :enabled
    - :selected

###筛选方法 ★

####filter()   
####not()
####has()

###JQ中的调试 ★

- 基于firebug的插件firequery
    - 自动注入jquery库
    - 查看当前jquery库版本
    - 高亮对应选择DOM元素
    - 数据缓存查看

###JQ中的模版引擎 ★

- 概念与作用
- 基于JQ的Jsviews模版
    - http://www.jsviews.com/
    - JsRender
        - 模版使用
        - 模版语法
    - JsViews
        - MVVM动态数据
    - JsObservable
        - 数据交互

###单元测试Qunit                       ★

- 什么是单元测试
    - 与功能测试和集成测试的区别
    - 单元测试的好处
- Qunit的使用
    - 标签
        - quint
            - 测试主体区域
        - quint-fixture
            - 进行DOM测试
    - 方法
        - QUnit.test()
        - expect()
    - 断言
        - equal() notEqual()
        - ok()
    - 选项
        - Check for Globals
        - No try-catch
    - 查看jQuery库的单元测试案例

###jQuery Mobile ★
- 介绍
    - 基于jquery开发
    - 用于创建移动web应用的开发框架
- data-*
    - data-role
        - page
        - header
        - content
        - footer
        - listview
        - navbar
- 页面切换
    - 同一个页面，ID控制
    - transition: slide
    - direction: reverse
    - class: ui-btn-right
    - icon: arrow-r    
    - iconpos: notext
- 按钮
    - data-role: button
    - data-inline: true
    - data-rel: dialog
- 主题
    - data-theme
- 事件操作
    - swipeleft
    - swiperight
    - 图片划屏操作效果演示
- 参考: w3cschool.cc/jquerymobile/jquerymobile-tutorial.html
