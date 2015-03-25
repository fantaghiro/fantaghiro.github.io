---
layout: post
title: 妙味课堂——问题解答视频
category: study
tags:
- js
- 妙味课堂
- 前端基础
- 学习笔记
---

这是妙味课堂专门的问题解答视频的笔记。讲到的内容，其实在以前的视频中陆陆续续地碰到过，只是这里作为知识点进行一个汇总。这一系列的视频数量并不多，但是每一个视频倒都是直击痛点。

- 目录
{:toc}

##HTML5视频-历史管理

**没有历史管理的彩票抽奖**

- 历史管理
	- onhashchange: 改变hash值来管理
	- history: 
		- pushState: 三个参数：数据 标题（都没实现） 地址（可选）
		- popstate事件: 读取数据 event.state
		- 注意：网址是虚假的，需在服务器指定对应页面，不然刷新找不到页面

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>彩票</title>
	<script>
		window.onload = function(){
			var oInput = document.getElementById('input1');
			var oDiv = document.getElementById('div1');

			oInput.onclick = function(){
				var number = randomNum(35, 7);
				oDiv.innerHTML = number;
			}

			function randomNum(all, now){
				var arr = [];
				var newArr = [];
				for(var i=1; i<=all; i++){
					arr.push(i);
				}
				for(var i=0; i<now; i++){
					newArr.push(arr.splice(Math.floor(Math.random()*arr.length), 1));
				}
				return newArr;
			}
		}
	</script>
</head>
<body>
	<input type="button" value="35选7" id="input1">
	<div id="div1"></div>
</body>
</html>
~~~

**采用onhashchange的方法**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>彩票</title>
	<script>

		//onhashchange : 事件 当hash值有变化的时候，就会触发
		
		window.onload = function(){
			var oInput = document.getElementById('input1');
			var oDiv = document.getElementById('div1');
			var obj = {};

			oInput.onclick = function(){
				var number = randomNum(35, 7);
				oDiv.innerHTML = number;
				var oRD = Math.random();
				obj[oRD] = number;
				window.location.hash = oRD;
			}

			window.onhashchange = function(){
				var number = obj[window.location.hash.substring(1)] || '';
				oDiv.innerHTML = number;
			}

			function randomNum(all, now){
				var arr = [];
				var newArr = [];
				for(var i=1; i<=all; i++){
					arr.push(i);
				}
				for(var i=0; i<now; i++){
					newArr.push(arr.splice(Math.floor(Math.random()*arr.length), 1));
				}
				return newArr;
			}
		}
	</script>
</head>
<body>
	<input type="button" value="35选7" id="input1">
	<div id="div1"></div>
</body>
</html>
~~~

**用html5的history对象来实现**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>彩票</title>
	<script>
		window.onload = function(){
			var oInput = document.getElementById('input1');
			var oDiv = document.getElementById('div1');
			var iNow = 1;

			oInput.onclick = function(){
				var number = randomNum(35, 7);
				oDiv.innerHTML = number;
				history.pushState(number, '', iNow++);
			}

			window.onpopstate = function(ev){
				var number = ev.state || '';
				oDiv.innerHTML = number;
			}

			function randomNum(all, now){
				var arr = [];
				var newArr = [];
				for(var i=1; i<=all; i++){
					arr.push(i);
				}
				for(var i=0; i<now; i++){
					newArr.push(arr.splice(Math.floor(Math.random()*arr.length), 1));
				}
				return newArr;
			}
		}
	</script>
</head>
<body>
	<input type="button" value="35选7" id="input1">
	<div id="div1"></div>
</body>
</html>
~~~

##JavaScript性能-DOM优化

### 什么是DOM

- 用于操作XML和HTML文档的应用程序
	- DOM节点
	- DOM树
	- DOM API
		- getElementById
		- childNodes
		- appendChild
		- innerHTML

### DOM与JavaScript

- 浏览器会把DOM与js独立实现
	- 像两个独立的小岛
- js操作dom
	- 从一个岛到另一个岛
- dom的性能
 	- 岛与岛之间的桥，每次通过收取“过桥费”
 	- 尽量减少过桥的次数
- innerHTML与dom方法对比

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Javascript性能-DOM优化</title>
	<script>
		window.onload = function(){
			var oDiv = document.getElementById('div1');
			var str = '';

			/* 这个在控制台打印出来的时间大约是240多毫秒
			console.time('hello');
			for(var i=0; i<5000; i++){
				oDiv.innerHTML += 'a';
			}
			console.timeEnd('hello');
			*/

			console.time('hello'); //这样执行，大约用0.2毫秒
			for(var i=0; i<5000; i++){
				str += 'a';
			}
			oDiv.innerHTML = str;
			console.timeEnd('hello');
		}
	</script>
</head>
<body>
	<div id="div1"></div>
</body>
</html>
~~~

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Javascript性能-DOM优化</title>
	<script>

	// chrome、safari类型的webkit的浏览器：dom方法要不innerHTML要好
	// IE、火狐中：innerHTML比dom方法要好

		window.onload = function(){
			var oUl = document.getElementById('ul1');
			var str = '';

			/*console.time('hello'); 
			for(var i=0; i<5000; i++){
				var oLi = document.createElement('li');
				oUl.appendChild(oLi);
			}
			console.timeEnd('hello');*/

			console.time('hello'); 
			for(var i=0; i<5000; i++){
				str += '<li></li>';
			}
			oUl.innerHTML = str;
			console.timeEnd('hello');
		}
	</script>
</head>
<body>
	<ul id="ul1"></ul>
</body>
</html>
~~~

###DOM优化

- 减少DOM操作
	- 节点克隆
		- cloneNode
	- 访问元素集合
		- 尽量用局部变量
	- 元素节点
		- 尽量用只获取元素的节点方法
	- 选择器API
		- 利用querySelector、querySelectorAll

**cloneNode**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Javascript性能-DOM优化</title>
	<script>

	//克隆方式要比上面的那种方式好一些。复制节点要比新创建好一些

	window.onload = function(){
			var oUl = document.getElementById('ul1');
			var str = '';

			/*console.time('hello'); 
			for(var i=0; i<5000; i++){
				var oLi = document.createElement('li');
				oLi.innerHTML = 'li';
				oUl.appendChild(oLi);
			}
			console.timeEnd('hello');*/

			console.time('hello');
			var oLi = document.createElement('li');
			oLi.innerHTML = 'li';
			for(var i=0; i<5000; i++){
				var newLi = oLi.cloneNode(true);
				oUl.appendChild(newLi);
			}
			console.timeEnd('hello');

		}
	</script>
</head>
<body>
	<ul id="ul1"></ul>
</body>
</html>
~~~

**尽量使用局部变量**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Javascript性能-DOM优化</title>
	<script>

	window.onload = function(){
			var oUl = document.getElementById('ul1');
			var aLi = oUl.getElementsByTagName('li');
			
			for(var i=0; i<5000; i++){
				var oLi = document.createElement('li');
				oUl.appendChild(oLi);
			}
			
			/*console.time('hello');
			for(var i=0; i<aLi.length; i++){
				aLi[i].innerHTML = 'li';
			}
			console.timeEnd('hello');*/

			console.time('hello');
			var len = aLi.length;
			for(var i=0; i<len; i++){
				aLi[i].innerHTML = 'li';
			}
			console.timeEnd('hello');

			//下面这种方法比上面注释起来的那种好。因为在aLi.length那里，不需要重复去获取元素计算长度
		}
	</script>
</head>
<body>
	<ul id="ul1"></ul>
</body>
</html>
~~~

**尽量用只获取元素的节点方法**

例如：

- childNodes => 可以获取到元素节点和文本节点
- children => 只能获取到元素节点
- firstChild => 元素节点 + 文本节点
- firstElementChild => 元素节点

**选择器API**

~~~ js
//var oUl = document.getElementById('ul1');
//var aLi = oUl.getElementsByTagName('li');

//用querySelectorAll这个方法，获取aLi，下面一句话就够了
var aLi = document.querySelectorAll('#ul1 li');
~~~

###DOM与浏览器

- 重排：改变页面的内容
- 重绘：浏览器显示内容
- 添加顺序
	- 尽量在appendChild前添加操作
- 合并dom操作
	- 利用cssText
- 缓存布局信息
- 文档碎片
	- createDocumentFragment()

**尽量在appendChild前添加操作**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Javascript性能-DOM优化</title>
	<script>

	window.onload = function(){
			var oUl = document.getElementById('ul1');
			
			/*console.time('hello');
			for(var i=0; i<5000; i++){
				var oLi = document.createElement('li');
				oUl.appendChild(oLi);
				oLi.innerHTML = 'li';
			}
			console.timeEnd('hello');*/

			console.time('hello'); //下面这种写法，性能上要优于上面的写法
			for(var i=0; i<5000; i++){
				var oLi = document.createElement('li');
				oLi.innerHTML = 'li';
				oUl.appendChild(oLi);
			}
			console.timeEnd('hello');
			
		}
	</script>
</head>
<body>
	<ul id="ul1"></ul>
</body>
</html>
~~~

**用cssText**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Javascript性能-DOM优化</title>
	<script>

	window.onload = function(){
			var oUl = document.getElementById('ul1');
			
			/*console.time('hello');
			for(var i=0; i<5000; i++){
				var oLi = document.createElement('li');
				oLi.style.width = '100px';
				oLi.style.height = '100px';
				oLi.style.background = 'red';
				oUl.appendChild(oLi);
			}
			console.timeEnd('hello');*/

			console.time('hello');
			for(var i=0; i<5000; i++){
				var oLi = document.createElement('li');
				oLi.style.cssText = 'width: 100px; height: 100px; background: red';
				oUl.appendChild(oLi);
			}
			console.timeEnd('hello');
		}
	</script>
</head>
<body>
	<ul id="ul1"></ul>
</body>
</html>
~~~

**缓存布局信息**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Javascript性能-DOM优化</title>
	<style>
		#div1 {width: 100px; height: 100px; background: red; position: absolute;}
	</style>
	<script>
	window.onload = function(){
			var oDiv = document.getElementById('div1');
			var L = oDiv.offsetLeft;
			var T = oDiv.offsetTop;
			/*setInterval(function(){
				oDiv.style.left = oDiv.offsetLeft + 1 + 'px';
				oDiv.style.top = oDiv.offsetTop + 1 + 'px';
			}, 30)*/

			setInterval(function(){
				L++;
				T++;
				oDiv.style.left = L + 'px';
				oDiv.style.top = T + 'px';
			}, 30)
	}
	</script>
</head>
<body>
	<div id="div1"></div>
</body>
</html>
~~~

**文档碎片**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Javascript性能-DOM优化</title>
	<style>
		#div1 {width: 100px; height: 100px; background: red; position: absolute;}
	</style>
	<script>
	window.onload = function(){
		var oUl = document.getElementById('ul1');
		var oFrag = document.createDocumentFragment();

		/*console.time('hello');
		for(var i=0; i<5000; i++){
			var oLi = document.createElement('li');
			oUl.appendChild(oLi);
		}
		console.timeEnd('hello');*/

		console.time('hello');
		for(var i=0; i<5000; i++){
			var oLi = document.createElement('li');
			oFrag.appendChild(oLi);
		}
		oUl.appendChild(oFrag);
		console.timeEnd('hello');
	}
	</script>
</head>
<body>
	<ul id="ul1"></ul>
</body>
</html>
~~~

###DOM与事件

- 事件委托

###DOM与前端模板

- 能更好的对逻辑和视图分离，MVC架构的基础

##JS的跨域

- www.a.com/a.js和www.a.com/c/b.js 这种都不存在跨域问题

存在跨域问题的包括：

- www.a.com和b.a.com
- www.a.com和www.b.com

ajax: XMLHttpRequest(); //ajax是不能跨域的

解决方式：

1. 子域与主域之间：设置document.domain = 'a.com'
2. 通过服务器代理：在服务器上做一个XMLHttpRequest代理文件
3. 利用script标签：jsonp
4. 利用location.hash来跨域
5. 利用window.name来跨域
6. 通过flash
7. html5的postMessage


jsonp : json + padding(内填充)

**a.com**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Javascript性能-DOM优化</title>
	<script>
		//a.com
		//jsonp : json + padding(内填充)
		
		function box(json){
			alert(json.name); //miaov
		}
		
	</script>
	<script type="text/javascript" src="jsonp.js"></script>
</head>
<body>
</body>
</html>
~~~

**b.com的jsonp文件**

~~~ html
//jsonp.js
//b.com
box({name: 'miaov'});
~~~

**a.com优化的写法**

~~~ js
function createJs(sUrl){
	var oScript = document.createElement('script');
	oScript.type = 'text/javascript';
	oScript.src = sUrl;
	document.getElementsByTagName('head')[0].appendChild(oScript);
}
createJs('jsonp.js?callback=box');
function box(json){
	alert(json.name); //miaov
}
~~~

##闭包

###什么是闭包？

- 函数嵌套函数
- 内部函数可以应用外部函数的参数和变量
- 参数和变量不会被垃圾回收机制所收回。

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>闭包</title>
	<script>
		//函数嵌套函数，内部函数可以应用外部函数的参数和变量，参数和变量不会被垃圾回收机制所收回。
		
		/*function aaa(a){
			var b = 5;

			function bbb(){
				alert(a);
				alert(b);
			}
		}

		aaa(); //aaa执行后，变量a、b并没有被垃圾回收机制收回。因为里面的函数bbb还在应用着。

		//JS中的垃圾回收机制
		
		function aaa(){
			var a = 1;
		}

		aaa(); //函数一致性，变量a就会被垃圾回收机制收回*/

		function aaa(){
			var a = 5;

			function bbb(){
				alert(a);
			}
			return bbb;
		}

		var c = aaa(); //aaa这里已经执行了，返回的bbb函数给了c
		c(); //c执行就相当于函数bbb执行了，这时候还是能够找到变量a，因此可以弹出5。这说明变量a并没有被垃圾回收机制收回。这就是一个典型的闭包。

	</script>
</head>
<body>
</body>
</html>
~~~

###闭包有什么好处？应用在哪里？

1. 希望一个变量长期驻扎在内存当中
2. 可以避免全局变量的污染
3. 私有成员的存在

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>闭包</title>
	<script>
		/* 全局变量受到污染
			var a = 1;

			function aaa(){
				a++;
				alert(a);
			}

			aaa(); //2
			aaa(); //3
			alert(a);
		 */
		
			/* 垃圾回收机制起作用，虽然全局变量没被污染，但是a却不能累加了
			function aaa(){
				var a = 1;
				a++;
				alert(a);
			}

			aaa(); //2
			aaa(); //2
			 */
			
			// 通过闭包实现在不污染全局变量的情况下，a还能够累加
			function aaa(){
				var a = 1;
				return function(){
					a++;
					alert(a);
				}
			}

			var b = aaa();
			b(); //2
			b(); //3
			alert(a); //报错，因为这个a是局部的，不是全局的了

	</script>
</head>
<body>
</body>
</html>
~~~

###闭包的用法

1. 模块化代码
2. 在循环中直接找到对应元素的索引

**改写**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>闭包</title>
	<script>
		/*function aaa(){
			alert(1);
		}

		aaa();*/

		/*(function(){
			alert(1);
		})();*/

		//下面这一段就是模块化代码
		var aaa = (function(){
			var a = 1;
			return function(){
				a++;
				alert(a);
			}
		})();

		aaa(); //2
		aaa(); //3
	</script>
</head>
<body>
</body>
</html>
~~~

**私有成员的存在**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>闭包</title>
	<script>
		var aaa = (function(){
			var a = 1;
			function bbb(){
				a++;
				alert(a);
			}
			function ccc(){
				a++;
				alert(a);
			}
			return {
				b: bbb, //私有方法
				c: ccc  //私有方法
			}
		})();

		aaa.b(); //2
		aaa.c(); //3
		alert(a); //报错
		alert(bbb); //报错
		alert(ccc); //报错 因为a、bbb和ccc都是私有的，在aaa外面调用不到
	</script>
</head>
<body>
</body>
</html>
~~~

**在循环中直接找到对应元素的索引**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>闭包</title>
	<script>
		window.onload = function(){
			var aLi = document.getElementsByTagName('li');

			/*for(var i=0; i<aLi.length; i++){
				aLi[i].onclick = function(){
					alert(i); //不论点击哪个li，都弹出3。当点击的时候，循环已经结束了，循环结束i就是3
				}
			}*/

			/* 写法一
			for(var i=0; i<aLi.length; i++){
				(function(i){
					aLi[i].onclick = function(){
						alert(i); //这时候依次点击li，分别弹出0、1、2
					}
				})(i);	
			}
			*/
		
			//写法二
			for(var i=0; i<aLi.length; i++){
				aLi[i].onclick = (function(i){
					return function(){
						alert(i); //这时候依次点击li，分别弹出0、1、2
					}
				})(i);
			}
		}
	</script>
</head>
<body>
	<ul>
		<li>111111111</li>
		<li>111111111</li>
		<li>111111111</li>
	</ul>
</body>
</html>
~~~

###闭包需要注意的地方。

- 在IE下有可能引起内存泄露

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>闭包</title>
	<script>
		//IE下会引发内存泄露
		/* 第一种解决IE下内存泄露的方法
		window.onload = function(){
			var oDiv = document.getElementById('div1');

			oDiv.onclick = function(){
				alert(oDiv.id);
			}

			//以下是解决办法
			window.onunload = function(){
				oDiv.onclick = null;
			}
		}
		*/
	
		//第二种解决方法
		window.onload = function(){
			var oDiv = document.getElementById('div1');
			var id = oDiv.id;
			oDiv.onclick = function(){
				alert(id);
			}
			oDiv = null;
		}
	</script>
</head>
<body>
	<div id="div1">aaaaaa</div>
</body>
</html>
~~~

##操作iframe

**iframe1.html**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>iframe1</title>
</head>
<body>
	<div id="div1">aaaaaa</div>
</body>
</html>
~~~

**操作iframe1的demo1.html**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>操作iframe</title>
	<script>
		window.onload = function(){
			var oInput = document.getElementById('input1');
			var oIframe = document.getElementById('iframe1');

			oInput.onclick = function(){
				//alert(oIframe.contentWindow); //contentWindow就是iframe的window对象 所有浏览器都支持
				oIframe.contentWindow.document.getElementById('div1').style.color = 'red';
				//contentDocument直接获取到iframe的document对象 IE6、7不支持
				//oIframe.contentDocument.getElementById('div1').style.background = 'red'; 
			}
		}
	</script>
</head>
<body>
	<input type="button" value="改变" id="input1">
	<iframe src="iframe1.html" id="iframe1"></iframe>
</body>
</html>
~~~


**iframe2.html**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>iframe1</title>
	<script>
		window.onload = function(){
			var oInput = document.getElementById('input1');

			oInput.onclick = function(){
				window.parent.document.getElementById('div1').style.color = 'red'; //window.parent指的就是它的父层 只隔一层

				//window.top找的是最顶层，当iframe出现多层嵌套的时候，可以用window.top找到最顶层
			}
			
		}
	</script>
</head>
<body>
	<input type="button" value="改变" id="input1">
</body>
</html>
~~~

**操作iframe2的demo2.html**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>操作iframe</title>
	<script>
	</script>
</head>
<body>
	<div id="div1">aaaaaa</div>
	<iframe src="iframe2.html" id="iframe2"></iframe>
</body>
</html>
~~~

**iframe的onload事件**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>操作iframe</title>
	<script>
		window.onload = function(){
			var oIframe = document.createElement('iframe');
			oIframe.src = 'iframe1.html';
			document.body.appendChild(oIframe);

			/*oIframe.onload = function(){
				alert(123);
			}*/

			//IE下的iframe的onload事件只能用绑定的形式
			oIframe.attachEvent('onload', function(){
				alert(123);
			})
		}
	</script>
</head>
<body>
</body>
</html>
~~~

**放钓鱼网站，防止自己被别家引用**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>操作iframe</title>
	<script>
		window.onload = function(){
			//当当前的window不是window.top的时候，说明这个window被其他的iframe嵌套了，那么就将自己的地址赋给window.top的地址。这样打开嵌套了这个网页的网页，就会自动跳到真正被嵌套的网页的地址
			if(window != window.top){
				window.top.location.href = window.location.href;
			} 
		}
	</script>
</head>
<body>
</body>
</html>
~~~

**如何改变iframe的大小**

**iframe3.html**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>iframe1</title>
</head>
<body>
	<div style="width: 200px; height: 200px; background: red"></div>
</body>
</html>
~~~

**iframe4.html**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>iframe1</title>
</head>
<body>
	<div style="width: 400px; height: 400px; background: green"></div>
</body>
</html>
~~~

**改变iframe大小的demo.html**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>操作iframe</title>
	<script>
		window.onload = function(){
			var aInput = document.getElementsByTagName('input');
			var oIframe = document.getElementById('iframe1');

			function changeHeight(){
				setTimeout(function(){
					oIframe.height = oIframe.contentWindow.document.body.offsetHeight;
				}, 100);
			}
			changeHeight();

			aInput[0].onclick = function(){
				oIframe.src = 'iframe3.html';
				changeHeight();
			}
			aInput[1].onclick = function(){
				oIframe.src = 'iframe4.html';
				changeHeight();
			}
		}
	</script>
</head>
<body>
	<input type="button" value="切换1">
	<input type="button" value="切换2">
	<iframe src="iframe3.html" id="iframe4" scrolling="no"></iframe>
</body>
</html>
~~~

##对象引用

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>对象引用</title>
	<script>
		/*var a = 5;
		var b = a;

		b += 3;
		alert(b); //8
		alert(a); //5

		//以上这种赋值的关系，a/b之间不互相影响，这存在于基本类型中（字符串、数字、布尔、空对象和undefined）*/
		
		/*var a = [1, 2, 3];
		var b = a;
		
		b.push(4);
		alert(b); //[1, 2, 3, 4];
		alert(a); //[1, 2, 3, 4]
		//以上不是赋值关系，而是引用关系，因此a、b互相影响*/

		//对象和函数都是引用的关系
		
		var a = [1, 2, 3];
		var b = a;

		var b = [1, 2, 3, 4]; //这里b是重新赋值了，与a之间的引用关系就断开了
		alert(b); //[1, 2, 3, 4]
		alert(a); //[1, 2, 3]
	</script>
</head>
<body>
	
</body>
</html>
~~~

**对象的复制**

**浅拷贝

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>对象引用</title>
	<script>
		/*var obj = {
			a : 10
		}
		var obj2 = obj;

		obj2.a = 20;
		alert(obj.a); //20*/

		var obj = {
			a : 10
		}

		function copy(obj){ //浅拷贝 浅克隆
			var newObj = {};

			for(var attr in obj){
				newObj[attr] = obj[attr];
			}

			return newObj;
		}
		var obj2 = copy(obj);
		obj2.a = 20;
		alert(obj.a); //10
	</script>
</head>
<body>
	
</body>
</html>
~~~

**深拷贝**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>对象引用</title>
	<script>
		/*//浅拷贝的问题
		var obj = {
			a : { b : 10 }
		}

		function copy(obj){
			var newObj = {};

			for(var attr in obj){
				newObj[attr] = obj[attr];
			}

			return newObj;
		}
		var obj2 = copy(obj);
		obj2.a.b = 20;
		alert(obj.a.b); //20*/

		/*//递归的写法：用递归求阶乘
		//1. 函数调用函数自身，执行递的动作
		//2. 最后一次判断一个终止条件，可以执行归的动作
		function test(n){
			if(n == 1){
				return 1;
			}
			return n*test(n-1);
		}
		alert(test(4)); //1*2*3*4=24*/
		

		//深拷贝
		var obj = {
			a : { b : 10 }
		}

		function deepCopy(obj){ //深拷贝

			if(typeof obj != 'object'){
				//console.trace();
				return obj;
			}

			var newObj = {};

			for(var attr in obj){
				newObj[attr] = deepCopy(obj[attr]);
			}

			return newObj;
		}

		var obj2 = deepCopy(obj);
		obj2.a.b = 20;
		alert(obj.a.b); //10
	</script>
</head>
<body>
	
</body>
</html>
~~~

##快速排序

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>js中的排序</title>
	<script>
		//js自带的排序：sort
		//比较流行的排序算法：快速排序
		
		//快速排序：
		//1. 找一个基准点
		//2. 建立两个数组，分别存储左边和右边的数
		//3. 利用递归进行下次比较
		
		function quickSort(arr){
			if(arr.length <= 1){
				return arr;
			}

			var num = Math.floor(arr.length / 2);
			var numValue = arr.splice(num, 1);
			var left = [];
			var right = [];

			for(var i=0; i<arr.length; i++){
				if(arr[i] < numValue){
					left.push(arr[i]);
				} else {
					right.push(arr[i]);
				}
			}

			return quickSort(left).concat([numValue], quickSort(right));
		}

		alert(quickSort([12, 5, 37, 6, 22, 40]));
	</script>
</head>
<body>
</body>
</html>
~~~

##枚举算法

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>枚举算法</title>
	<style>
		div {width: 300px; position: relative;}
		div span {margin: 10px;}
	</style>
	<script>
		//枚举算法：用for来从众多的候选答案中，通过if找出正确的解
		
		window.onload = function(){

			var aP = document.getElementsByTagName('p');
			var aSpan1 = aP[0].getElementsByTagName('span');
			var aSpan2 = aP[1].getElementsByTagName('span');
			var aSpan3 = aP[2].getElementsByTagName('span');
			var oInput = document.getElementById('input1');

			oInput.onclick = function(){
				solvePuzzle();
			}

			function solvePuzzle(){
				for(var i=1; i<=9; i++){
					for(var j=0; j<=9; j++){
						for(var k=0; k<=9; k++){
							for(var m=0; m<=9; m++){
								for(var n=0; n<=9; n++){

									var a = 10000*i + 1000*j + 100*k + 10*m +n;
									var b = i;
									var c = n*111111;

									if(a*b == c){
										aSpan1[0].innerHTML = i;
										aSpan1[1].innerHTML = j;
										aSpan1[2].innerHTML = k;
										aSpan1[3].innerHTML = m;
										aSpan1[4].innerHTML = n;

										aSpan2[0].innerHTML = i;

										for(var x=0; x<aSpan3.length; x++){
											aSpan3[x].innerHTML = n;
										}
									}

								}
							}
						}
					}
				}
			}	
		}
	</script>
</head>
<body>
	<div>
		<p style="margin-left: 35px;"><span>枚</span><span>举</span><span>算</span><span>法</span><span>题</span></p>
		<p>*  <span style="position: absolute; top: 30px; left: 180px;">枚</span></p>
		<hr>
		<p><span>题</span><span>题</span><span>题</span><span>题</span><span>题</span><span>题</span></p>
	</div>
	<input type="button" value="求解" id="input1">
</body>
</html>
~~~

**枚举法用到页面中**

~~~
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>枚举算法</title>
	<style>
		div {width: 300px; position: relative;}
		div span {margin: 10px;}
	</style>
	<script>
		window.onload = function(){

			var aA = document.getElementsByTagName('a');
			var oUl = document.getElementById('ul1');
			var aLi = oUl.getElementsByTagName('li');

			for(var i=0; i<aA.length; i++){
				aA[i].onclick = function(){
					if (mj(this.innerHTML)){
						var oLi = document.createElement('li');
						oLi.innerHTML = this.innerHTML;
						if(!aLi[0]){
							oUl.appendChild(oLi);
						} else {
							oUl.insertBefore(oLi, aLi[0]);
						}
					} else {
						mj2(this.innerHTML);
					}
				}
			}

			function mj(text){
				var result = true;
				for(var i=0; i<aLi.length; i++){
					if(aLi[i].innerHTML == text){
						result = false;
					}
				}
				return result;
			}

			function mj2(text){
				for(var i=0; i<aLi.length; i++){
					if(aLi[i].innerHTML == text){
						oUl.insertBefore(aLi[i], aLi[0]);
					}
				}
			}

		}
	</script>
</head>
<body>
	<a href="javascript:;">北京</a>
	<a href="javascript:;">上海</a>
	<a href="javascript:;">深圳</a>
	<a href="javascript:;">广州</a>
	<a href="javascript:;">天津</a>
	<a href="javascript:;">重庆</a>
	<a href="javascript:;">杭州</a>
	<ul id="ul1"></ul>
</body>
</html>
~~~

##函数声明与函数表达式

**函数声明与函数表达式的形式**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>函数声明与函数表达式</title>
	<script>
		//函数声明：function 函数名(){}
		//函数表达式：function 函数名（可写可不写）(){} : 命名函数表达式 匿名函数表达式
		
		// function aaa(){} : 函数声明
		// var a = function aaa(){} : 命名函数表达式
		// var a = function(){} : 匿名函数表达式
		
		// (function aaa(){}) : 表达式 函数放到括号里
		// ~function aaa(){} : 表达式 函数前面加了运算符
		// -function aaa(){} : 表达式 函数前面加了运算符
		// +function aaa(){} : 表达式 函数前面加了运算符 
		// !function aaa(){} : 表达式 函数前面加了运算符
	</script>
</head>
<body>
	
</body>
</html>
~~~

**函数声明与函数表达式的区别**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>函数声明与函数表达式</title>
	<script>
		//函数声明与函数表达式之间的区别
		//1. 函数表达式可以直接后面加括号执行，而函数声明是不可以的
		//2. 函数声明可以被提前解析出来的。函数声明有预解析

		// function aaa(){alert(1);}(); //报错
		//var a = function aaa(){alert(1);}(); //弹出1
		//~function aaa(){alert(1);}(); //弹出1
		
		/*if(true){
			function aaa(){
				alert(1);
			}
		} else {
			function aaa(){
				alert(2);
			}
		}
		aaa(); //chrome下弹出2，因为函数声明预解析，后面的函数声明覆盖了前面的函数声明，等到if执行的时候，函数aaa里面已经变成alert(2)了*/

		/*//用函数表达式就不会出现上述问题
		if(true){
			var a = function aaa(){
				alert(1);
			}
		} else {
			var a = function aaa(){
				alert(2);
			}
		}
		a();*/

		/*//命名函数表达式VS匿名函数表达式
		if(true){
			var a = function aaa(){
				alert(1);
			}
		} else {
			var a = function aaa(){
				alert(2);
			}
		}
		aaa(); //在ie下可以，在chrome下报错，说aaa是undefined*/

	</script>
</head>
<body>
	
</body>
</html>
~~~

**命名函数表达式的问题**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>函数声明与函数表达式2</title>
	<script>
		//不推荐使用命名的函数表达式，只有在debug的时候可以考虑使用，否则容易出现问题：

		/*var a = function aaa(){
			alert();
			alert(typeof aaa); //这个aaa在函数内部是可以找到的
		}

		// a(); //所有浏览器都支持
		// aaa(); //chrome和firefox报错；ie下可以。在外面，标准浏览器是找不到的*/

		(function aaa(){alert(1)}) //有名字的函数表达式
		aaa(); //在外面在chrome和火狐下是找不到的
	</script>
</head>
<body>
	
</body>
</html>
~~~

**只有在debugger时使用命名函数表达式**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>函数声明与函数表达式3</title>
	<script>
		function aaa(){
			return bbb();
		}

		/*function bbb(){
			debugger;
		}*/

		var bbb = (function bbb(){
			return function(){
				debugger;
			}
		})();

		aaa();
	</script>
</head>
<body>
	
</body>
</html>
~~~

##事件委托（事件代理）

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>事件委托</title>
	<script>

		//事件委托：利用冒泡的原理，把事件加到父级上，触发执行效果
		//好处：
		//1. 提高性能
		//2. 新添加的元素还有之前的事件

		window.onload = function(){
			var oUl = document.getElementById('ul1');
			var aLi = oUl.getElementsByTagName('li');

			/*for(var i=0; i<aLi.legnth; i++){
				aLi[i].onclick = function(){
					alert(123);
				}
			}*/

			oUl.onclick = function(){
				alert(123);
			}
		}
	</script>
</head>
<body>
	<ul id="ul1">
		<li>001</li>
		<li>002</li>
		<li>003</li>
		<li>004</li>
	</ul>
</body>
</html>
~~~

**提高性能**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>事件委托2</title>
	<script>
		//event对象：事件源：不管在哪个事件中，只要你操作的那个元素就是事件源
		//ie: window.event.srcElement
		//标准下: event.target
		//nodeName : 找到元素的标签名

		window.onload = function(){
			var oUl = document.getElementById('ul1');
			var aLi = oUl.getElementsByTagName('li');

			/*for(var i=0; i<aLi.length; i++){
				aLi[i].onmouseover = function(){
					this.style.background = 'red';
				}
				aLi[i].onmouseout = function(){
					this.style.background = '';
				}
			}*/

			oUl.onmouseover = function(ev){
				var ev = ev || window.event;
				var target = ev.target || ev.srcElement;

				//alert(target.innerHTML);
				//alert(target.nodeName);
				
				if(target.nodeName.toLowerCase() == 'li'){
					target.style.background = 'red';
				}
				
			}
			oUl.onmouseout = function(ev){
				var ev = ev || window.event;
				var target = ev.target || ev.srcElement;

				if(target.nodeName.toLowerCase() == 'li'){
					target.style.background = '';
				}
			}
		}
	</script>
</head>
<body>
	<ul id="ul1">
		<li>001</li>
		<li>002</li>
		<li>003</li>
		<li>004</li>
	</ul>
</body>
</html>
~~~

**新添加的元素还有原来的事件**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>事件委托2</title>
	<script>
		window.onload = function(){
			var oUl = document.getElementById('ul1');
			var aLi = oUl.getElementsByTagName('li');
			var oInput = document.getElementById('input1');
			var iNow = 4;

			oInput.onclick = function(){
				iNow++;
				var oLi = document.createElement('li');
				oLi.innerHTML = iNow * 111;
				oUl.appendChild(oLi);
			}

			/*for(var i=0; i<aLi.length; i++){
				aLi[i].onmouseover = function(){
					this.style.background = 'red';
				}
				aLi[i].onmouseout = function(){
					this.style.background = '';
				}
			}*/

			oUl.onmouseover = function(ev){
				var ev = ev || window.event;
				var target = ev.target || ev.srcElement;
				if(target.nodeName.toLowerCase() == 'li'){
					target.style.background = 'red';
				}
				
			}
			oUl.onmouseout = function(ev){
				var ev = ev || window.event;
				var target = ev.target || ev.srcElement;

				if(target.nodeName.toLowerCase() == 'li'){
					target.style.background = '';
				}
			}
		}
	</script>
</head>
<body>
	<input type="button" value="添加" id="input1">
	<ul id="ul1">
		<li>001</li>
		<li>002</li>
		<li>003</li>
		<li>004</li>
	</ul>
</body>
</html>
~~~
