---
layout: post
title: 妙味课堂——HTML5
category: study
tags:
- js
- HTML5
- 妙味课堂
- 前端基础
- 学习笔记
---

HTML5的内容虽然学得快但也学得糙，欠练。就此妙味课堂所有主干的课程已经学习得差不多了。今后可能没有那么省事的视频可看了，不过对前端知识的学习还是要持之以恒才行。从开始学习妙味课堂第一个前段视频开始到现在差不多是5个月的时间，每日坚持，进步看得见。

- 目录
{:toc}

##新增的语义化标签

###新的页面结构以及宽松的语法规范

~~~ html
<!doctype html>
<html>
	<head>
		<meta charset="utf-8"/>
		<title></title>
	</head>
	<body>
	</body>
</html>
~~~

###新的结构化元素

- 语义化标签的由来 [http://devfiles.myopera.com/articles/572/idlist-url.htm](http://devfiles.myopera.com/articles/572/idlist-url.htm)

###语义化标签

- &lt;header>&lt;/header> 页眉
	- 主要用于页面的头部的信息介绍，也可用于板块头部
- &lt;hgroup>&lt;/hgroup> 页面上的一个标题组合
	- 一个标题和一个子标题，或者标语的组合

~~~ html
<hgroup>
	<h1>妙味课堂</h1>
	<h2>待您进入富有人情味的IT培训</h2>
</hgroup>
~~~

- &lt;nav>&lt;/nav>导航（包含链接的一个列表）

~~~ html
<nav><a href="#">链接</a><a href="#">链接</a></nav>
---
<nav>
	<p><a href="#">妙味课堂</a></p>
	<p><a href="#">妙味课堂</a></p>
</nav>
---
<nav>
	<h2>妙味精品课程</h2>
	<ul>
		<li><a href="#">javascript</a></li>
		<li><a href="#">html+css</a></li>
	</ul>
</nav>
~~~

- &lt;footer>&lt;/footer> 页脚 页面的底部 或者 版块底部
- &lt;section>&lt;/section> 页面上的板块
- &lt;article>&lt;/article> 用来在页面中表示一套结构完整且独立的内容部分
	- 可以用来呈现论坛的一个帖子、杂志或报纸中的一篇文章、一篇博客、用户提交的评论内容、可互动的页面模块挂件等。
- &lt;aside>&lt;/aside> 元素标签可以包含与当前页面或主要内容相关的引用、侧边栏、广告、nav元素组、以及其他类似的有别于主要内容的部分
	- aside的内容应该与article的内容相关
	- 被包含在&lt;article>中作为主要内容的附属信息部分，其中的内容是与当前文章有关的引用、词汇列表等
	- 在&lt;article>之外使用，作为页面或站点全局的附属信息部分；最典型的形式是侧边栏（sidebar），其中的内容可以是友情链接、附属导航或广告单元等。
- &lt;figure>&lt;/figure>用于对元素进行组合。一般用于图片或视频
- &lt;figcaption>&lt;/figcaption> figure的子元素 用于对figure的内容进行说明

~~~ html
<figure>
	<img src="miaov.png" /> //注意没有alt
	<figcaption>妙味课堂 photo&copy 妙味趣学</figcaption>
</figure>
~~~

- &lt;time>&lt;/time> 用来表现时间或日期

~~~ html
<p>
	我们在每天早上<time>9:00</time>开始营业。
</p>
<p>
	我在<time datetime="2008-02-14">情人节</time>有个约会。
</p>
~~~

- &lt;datalist>&lt;/datalist> 选项列表。与input元素配合使用，来定义input可能的值。

~~~ html
<input type="text" list="valList" />
<datalist id="valList">
	<option value="javascript">javascript</option>
	<option value="html">html</option>
	<option value="css">css</option>
</datalist>
~~~

- &lt;details>&lt;/details> 用于描述文档或文档某个部分的细节
	- 该元素用于摘录引用等 应该与页面的主要内容区分开的其他内容
	- open属性默认展开
- &lt;summary>&lt;/summary> details元素的标题

~~~ html
<details>
	<summary>妙味课堂</summary>
	<p>国内将知名的IT培训机构</p>
</details>
~~~

- &lt;dialog>&lt;/dialog> 定义一段对话

~~~ html
<dialog>
	<dt>老师</dt>
	<dd>2+2等于？</dd>
	<dt>学生</dt>
	<dd>4</dd>
	<dt>老师</dt>
	<dd>答对了！</dd>
</dialog>
~~~

- &lt;address>&lt;/address> 定义文章或页面作者的详细联系信息
- &lt;mark>&lt;/mark> 需要标记的词或句子
- &lt;keygen>给表单添加一个公钥

~~~ html
<form action="http://www.baidu.com" method="get">
	用户：<input type="text" name="usr_name" />
	公钥：<keygen name="security" />
	<input type="submit">
</form>
~~~

- &lt;progress>&lt;/progress> 定义进度条

~~~ html
<progress max="100" value="76">
	<span>76</span>% //该行用于向下兼容
</progress>
~~~

###IE下的兼容

- 插件：html5shiv.js
- 标签
	- 针对IE6-8这些不支持HTML5语义化标签的浏览器，我们可以使用javascript来解决他们。方法：在页面的头部加上：

~~~ html
<script>
	document.createElement('header');
	document.createElement('nav');
	document.createElement('footer');
	...
</script>
~~~

- 样式
	- HTML5语义化标签在IE6-8下，我们用js创造出来之后，它是不会有任何默认样式的甚至是display，所以在样式表里，要对这些标签定义一下它们默认的display

###forms

- 新的输入型控件
	-email：电子邮箱文本框，跟普通的没什么区别
		- 当输入不是邮箱的时候，验证通不过
		- 移动端的键盘会有变化
	- tel：电话号码
	- url：网页的URL
	- search：搜索引擎
		- chrome下输入文字后，会多出一个关闭的X
	- range：特定范围内的数值选择器
		- min、max、step（步数）
		- 例子：用js来显示当前数值
	- number：只能包含数字的输入框
	- color：颜色选择器
	- datetime：显示完整日期
	- datetime-local：显示完整日期，不含时区
	- time：显示时间，不含时区
	- date：显示日期
	- week：显示周
	- month：显示月

- 新的表单特性和函数
	- placeholder：输入框提示信息
		- 例子：微博的密码框提示
	- autocomplete：是否保存用户输入值
		- 默认为on，关闭提示选择off
	- autofocus：指定表单获取输入焦点
	- list和datalist：为输入框构造一个选择列表
		- list值为datalist标签的id
	- required：此项必填，不能为空
	- pattern：正则验证 pattern="\d{1,5}"
	- formaction：在submit里定义提交地址

- 表单验证
	- validity对象，通过下面的valid可以查看验证是否通过，如果八种验证都通过返回true，一种验证失败返回false
	- oText.addEventListener('invalid', fn1, false);
	- ev.preventDefault()
	- valueMissing: 输入值为空时
	- typeMismatch: 控件值与预期类型不匹配
	- patternMismatch: 输入值不满足pattern正则
	- tooLong: 超过maxLength最大限制
	- rangeUnderflow: 验证的range最小值
	- rangeOverflow: 验证的range最大值
	- stepMismatch: 验证range的当前值是否符合min、max及step的规则
	- customError 不符合自定义验证
		- setCustomValidity(); 自定义验证
	- invalid事件：验证反馈 input.addEventListener('invalid', fn, false)
		- 阻止默认验证: ev.preventDefault()
	- formnovalidate属性：关闭验证

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>表单的验证反馈</title>
</head>
<body>
	<form>
		<input type="text" required id="text" pattern="d{1,5}" maxlength="5">
		<input type="submit">
	</form>
	<script>
		var oText = document.getElementById('text');
		oText.addEventListener('invalid', fn, false);
		function fn(){
			// alert(this.validity);
			// alert(this.validity.valid);
			// alert(this.validity.valueMissing);
			// alert(this.validity.typeMismatch);
			// alert(this.validity.patternMismatch);
			// alert(this.validity.tooLong);
			ev.preventDefault();
		}

		//valueMissing: 当输入值为空时，返回true
		//typeMismatch: 当输入类型和要求的类型不一致时，返回true
		//patternMismatch: 当输入内容和预期的正则是不匹配时，返回true
		//tooLong: 当输入内容的长度超出了maxlength的限制，返回true
	</script>
</body>
</html>
~~~

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>表单的验证反馈</title>
</head>
<body>
	<form>
		<input type="text" id="text">
		<input type="submit">
	</form>
	<script>
		var oText = document.getElementById('text');
		oText.addEventListener('invalid', fn, false);
		oText.oninput = function(){
			if(this.value == '敏感词'){
				this.setCustomValidity('请不要输入敏感词');
			} else {
				this.setCustomValidity('');
			}
		}
		function fn(){
			alert(this.validity.customError);
			ev.preventDefault(); 
		}

		//customError: 不符合自定义验证的时候，返回true
	</script>
</body>
</html>
~~~

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
</head>
<body>
	<form action="http://www.baidu.com">
		<input type="text" placeholder="请输入4—16个字符" name="user" pattern="d{4,16}" required />
		<input type="submit" value="提交" />
		<input type="submit" value="保存至草稿箱" formaction="http://www.qq.com" formnovalidate />
	</form>
</body>
</html>
~~~

##HTML5新特性的浏览器支持情况

[http://www.caniuse.com/#index](http://www.caniuse.com/#index)

##新的选择器

- querySelector
- querySelectorAll
- getElementsByClassName

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>新的选择器</title>
	<script>
		// document.getElementById();
		// document.getElementsByTagName();
		//$('#div1') $('.box') $('ul li')

		window.onload = function(){
			//querySelector只能选择到一组元素中的第一个元素
			// var oDiv = document.querySelector('#div1'); //id形式
			// var oDiv = document.querySelector('div'); //标签形式 
			// var oDiv = document.querySelector('.box'); //class形式
			var oDiv = document.querySelector('[title=hello]'); //通过属性值查找
			
			oDiv.style.background = 'red';

			//querySelectorAll 选择到一组元素
			var aDiv = document.querySelectorAll('.box');
			alert(aDiv.length);
			aDiv[1].style.background = "blue";

			var aBox = document.getElementsByClassName('box');
			alert(aBox.length);
		}
	</script>
</head>
<body>
	<div id="div1" class="box" title="hello">div</div>
	<div class="box">div2</div>
	<p class="box">p</p>
</body>
</html>
~~~

##获取class列表属性

- classList
	- length: class的长度
	- add(): 添加class方法
	- remove(): 删除class方法
	- toggle(): 切换class方法

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>class列表属性</title>
	<script>
		window.onload = function(){
			var oDiv = document.querySelector('#div1');
			// alert(oDiv.classList); //box1 box2 box3
			// alert(typeof oDiv.classList); //object 类似于数组的对象
			// alert(oDiv.classList.length); //3
			oDiv.classList.add('box4');
			oDiv.classList.remove('box2');
			oDiv.classList.toggle('box3'); //如果原本有box3，就remove；如果没有，就add
		}
	</script>
</head>
<body>
	<div id="div1" class="box1 box2 box3">div</div>
</body>
</html>
~~~

##JSON的新方法

- parse(): 把字符串转成json
	- 字符串中的属性要严格的加上引号
- stringify(): 把json转化成字符串
	- 会自动的把双引号加上
- 新方法与eval的区别
- 新方法的应用
	- 深度克隆新对象
- 如何其他浏览器做到兼容
	- [http://www.json.org](http://www.json.org)去下载json2.js

**parse()方法**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>json的新方法</title>
	<script>
	/* 用eval
		var str = 'function show(){alert(123)}';
		eval(str); //eval能把字符串转为js
		show();
	*/
	//eval可以解析任何字符串变成JS
	//parse只能解析json形式的字符串变成js （安全性更高一些）

	/* 报错，因为parse转不了function这样的字符串
		var str = 'function show(){alert(123)}';
		JSON.parse(str); //eval能把字符串转为js
		show();
	*/

	/* 报错，这里的name没有加双引号就不行
		var str = '{name: "hello"}';
		var json = JSON.parse(str);
		alert(json.name);
	*/

		var str = '{"name": "hello"}'; //一定是严格的json形式
		var json = JSON.parse(str);
		alert(json.name); //弹出hello
	</script>
</head>
<body>
</body>
</html>
~~~

**stringify()方法**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>json的新方法</title>
	<script>
		var json = {name: "hello"};
		var str = JSON.stringify(json);
		alert(str); //{"name":"hello"}
	</script>
</head>
<body>
</body>
</html>
~~~

**对象拷贝**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>对象的拷贝</title>
	<script>
		var a = {
			name: 'hello'
		}

		/*
		//浅拷贝
		var b = {};
		for(var attr in a){
			b[attr] = a[attr];
		}
		*/
	
		//用parse()和stringify()来实现
		

		var str = JSON.stringify(a);
		var b = JSON.parse(str);

		b.name = 'hi';
		alert(a.name); //hello
	</script>
</head>
<body>
</body>
</html>
~~~

##data自定义数据

- dataset
	- data-name: dataset.name
	- data-name-first: dataset.nameFirst
- data数据在jQuery Mobile中有着重要作用

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>data自定义数据</title>
	<script>
		window.onload = function(){
			//getAttribute
			
			var oDiv = document.querySelector('#div1');
			alert(oDiv.dataset.miaov);
			alert(oDiv.dataset.miaovAll);
		}
	</script>
</head>
<body>
	<div id="div1" data-miaov="妙味" data-miaov-all="妙味课堂"></div>
</body>
</html>
~~~

##延迟加载JS

- JS的加载会影响后面的内容加载
	- 很多浏览器都采用了并行加载JS，但还是会影响其他内容
- HTML5的defer和async
	- defer: 延迟加载，会按顺序执行，在onload执行前被触发
	- async: 异步加载，加载完就触发，有顺序问题
- Labjs库

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>JS加载</title>
	<script src="a.js"></script>
	<script src="b.js"></script>
	<script src="c.js"></script>
	<!-- 解决方法 -->
	<!-- 1. 把script放到body底部 -->
	<!-- 2. 给外部的script添加 defer = "defer" 这个是延迟到onload执行前触发 -->
	<!-- 3. 给script添加 async = "async" 加上异步，就代表是与其他内容并排加载的-->
</head>
<body>
	<!-- 默认上面所有的js都加载完毕之后，再加载img -->
	<img src="1.jpg" alt="">
</body>
</html>
~~~

##历史管理

- 触发历史管理：1. 跳转页面；2. hash；3. pushState
- onhashchange: 改变hash值来管理
- history:
	- 服务器下运行
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

##拖放事件

- draggable:
	- 设置为true，元素就可以拖拽了
- 拖拽元素事件：事件对象为被拖拽元素
	- dragstart，拖拽前触发
	- drag，拖拽前、拖拽结束之间，连续触发(不管鼠标是否在移动)
	- dragend，拖拽结束触发
- 目标元素事件：事件对象为目标元素
	- dragenter，进入目标元素触发，相当于mouseover
	- dragover，进入目标、离开目标之间，连续触发(不管鼠标是否在移动)
	- dragleave，离开目标元素触发，相当于mouseout
	- drop，在目标元素上释放鼠标触发
- 事件的执行顺序：drop不触发的时候
	- dragstart -> drag -> dragenter -> dragover -> dragleave -> dragend
- 事件的执行顺序：drop触发的时候（dragover的时候阻止默认事件）
	- dragstart -> drag -> dragenter -> dragover -> drop -> dragend
- 不能释放的光标和能释放的光标不一样

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>拖放操作</title>
	<style>
		li {width: 100px; height: 30px; background: yellow; margin: 10px; list-style: none;}
		#div1 {width: 100px; height: 100px; background: red; margin: 200px;}
	</style>
	<script>
		window.onload = function(){
			var aLi = document.querySelectorAll('li');
			var oDiv = document.querySelector('#div1');
			var i = 0;

			for(var i=0; i<aLi.length; i++){
				aLi[i].ondragstart = function(){
					this.style.background = 'green';
				}

				aLi[i].ondrag = function(){
					// document.title = i++;
				}

				aLi[i].ondragend = function(){
					this.style.background = 'yellow';
				}
			}

			oDiv.ondragenter = function(){
				this.style.background = 'blue';
			}
			
			oDiv.ondragover = function(ev){
				// document.title = i++;
				// 要想触发drop事件，就必须在dragover当中阻止默认事件
				var ev = ev || window.event;
				ev.preventDefault();
			}

			oDiv.ondragleave = function(){
				this.style.background = 'red';
			}

			oDiv.ondrop = function(){
				alert(123);
			}
		}
	</script>
</head>
<body>
	<ul>
		<li draggable="true">a</li>
		<li draggable="true">b</li>
		<li draggable="true">c</li>
	</ul>
	<div id="div1"></div>
</body>
</html>
~~~

- 解决火狐下的问题
	- 必须设置dataTransfer对象才可以拖拽除图片外的其他标签
- dataTransfer对象（该对象是event对象下的）
	- setData(): 设置数据 key和value （必须是字符串）
	- getData(): 获取数据，根据key值，获取对应的value
	- effectAllowed
		- effectAllowed: 设置光标样式(none, copy, copyLink, copyMove, link, linkMove, move, all和uninitialized)
	- setDragImage
		- 三个参数：指定的元素或图片，坐标X，坐标Y
	- files
		- 获取外部拖拽的文件，返回一个filesList列表
		- filesList下有个type属性，返回文件的类型
	- FileReader对象（读取文件信息）
		- readAsDataURL
			- 参数为要读取的文件对象，将文件读取为DataURL
		- onload
			- 当读取文件成功完成的时候触发此事件
			- this.result，来获取读取的文件数据，如果是图片，将返回base64格式的图片数据
- 实例
	- 拖拽删除列表
	- 拖拽购物车
	- 上传图片预览功能

**实现火狐下的拖拽**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>拖放操作——解决火狐的问题</title>
	<style>
		li {width: 100px; height: 30px; background: yellow; margin: 10px; list-style: none;}
		#div1 {width: 100px; height: 100px; background: red; margin: 200px;}
	</style>
	<script>
		window.onload = function(){
			var aLi = document.querySelectorAll('li');
			var oDiv = document.querySelector('#div1');
			var i = 0;

			for(var i=0; i<aLi.length; i++){
				aLi[i].ondragstart = function(ev){
					var ev = ev || window.event;
					ev.dataTransfer.setData('name', 'hello'); //火狐下面的操作 设置过这个就可以拖放了
					this.style.background = 'green';
				}

				aLi[i].ondrag = function(){
					// document.title = i++;
				}

				aLi[i].ondragend = function(){
					this.style.background = 'yellow';
				}
			}

			oDiv.ondragenter = function(){
				this.style.background = 'blue';
			}
			
			oDiv.ondragover = function(ev){
				// document.title = i++;
				// 要想触发drop事件，就必须在dragover当中阻止默认事件
				var ev = ev || window.event;
				ev.preventDefault();
			}

			oDiv.ondragleave = function(){
				this.style.background = 'red';
			}

			oDiv.ondrop = function(ev){
				var ev = ev || window.event;
				alert(ev.dataTransfer.getData('name')); //可以setData就可以getData
				alert(123);
			}
		}
	</script>
</head>
<body>
	<ul>
		<li draggable="true">a</li>
		<li draggable="true">b</li>
		<li draggable="true">c</li>
	</ul>
	<div id="div1"></div>
</body>
</html>
~~~

**拖拽删除列表**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>拖拽删除列表</title>
	<style>
		li {width: 100px; height: 30px; background: yellow; margin: 10px; list-style: none;}
		#div1 {width: 100px; height: 100px; background: red; margin: 200px;}
	</style>
	<script>
		window.onload = function(){
			var aLi = document.querySelectorAll('li');
			var oDiv = document.querySelector('#div1');
			var oUl = document.querySelector('#ul1')
			var i = 0;

			for(var i=0; i<aLi.length; i++){
				aLi[i].index = i;
				aLi[i].ondragstart = function(ev){
					var ev = ev || window.event;
					ev.dataTransfer.setData('name', this.index);
					this.style.background = 'green';
				}

				aLi[i].ondrag = function(){
					// document.title = i++;
				}

				aLi[i].ondragend = function(){
					this.style.background = 'yellow';
				}
			}

			oDiv.ondragenter = function(){
				this.style.background = 'blue';
			}
			
			oDiv.ondragover = function(ev){
				// document.title = i++;
				// 要想触发drop事件，就必须在dragover当中阻止默认事件
				var ev = ev || window.event;
				ev.preventDefault();
			}

			oDiv.ondragleave = function(){
				this.style.background = 'red';
			}

			oDiv.ondrop = function(ev){
				var ev = ev || window.event;
				oUl.removeChild(aLi[ev.dataTransfer.getData('name')]);
				for(var i=0; i<aLi.length; i++){
					aLi[i].index = i;
				}
			}
		}
	</script>
</head>
<body>
	<ul id="ul1">
		<li draggable="true">a</li>
		<li draggable="true">b</li>
		<li draggable="true">c</li>
	</ul>
	<div id="div1"></div>
</body>
</html>
~~~

**effectAllowed和setDragImage**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>拖放操作——effectAllowed和setDragImage</title>
	<style>
		li {width: 100px; height: 30px; background: yellow; margin: 10px; list-style: none;}
		#div1 {width: 100px; height: 100px; background: red; margin: 200px;}
	</style>
	<script>
		window.onload = function(){
			var aLi = document.querySelectorAll('li');
			var oDiv = document.querySelector('#div1');
			var oUl = document.querySelector('#ul1');
			var oImg = document.querySelector('img');
			var i = 0;

			for(var i=0; i<aLi.length; i++){
				aLi[i].ondragstart = function(ev){
					var ev = ev || window.event;
					ev.dataTransfer.setData('name', 'hello');
					ev.dataTransfer.effectAllowed = 'link';
					ev.dataTransfer.setDragImage(oImg, 0, 0);
					
				}

				aLi[i].ondrag = function(){
				}

				aLi[i].ondragend = function(){
					this.style.background = 'yellow';
				}
			}

			oDiv.ondragenter = function(){
				this.style.background = 'blue';
			}
			
			oDiv.ondragover = function(ev){
				var ev = ev || window.event;
				ev.preventDefault();
			}

			oDiv.ondragleave = function(){
				this.style.background = 'red';
			}

			oDiv.ondrop = function(ev){
				
			}
		}
	</script>
</head>
<body>
	<ul id="ul1">
		<li draggable="true">a</li>
		<li draggable="true">b</li>
		<li draggable="true">c</li>
	</ul>
	<div id="div1"></div>
	<img src="img/ppt.gif" style="display: none;">
</body>
</html>
~~~

**拖放外部文件**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>拖放操作——拖放外部文件</title>
	<style>
		#div1 {width: 200px; height: 200px; background: red; margin: 100px;}
	</style>
	<script>
		window.onload = function(){
			var oDiv = document.querySelector('#div1');
			var oImg = document.querySelector('img');
			var i = 0;

			oDiv.ondragenter = function(){
				this.innerHTML = '可以释放啦';
			}
			
			oDiv.ondragover = function(ev){
				var ev = ev || window.event;
				ev.preventDefault();
			}

			oDiv.ondragleave = function(){
				this.innerHTML = '将文件拖拽到此区域';
			}

			oDiv.ondrop = function(ev){
				var ev = ev || window.event;
				ev.preventDefault();
				var fs = ev.dataTransfer.files;
				// alert(fs); //object Filelist
				// alert(fs.length);
				// alert(fs[0].type); //文件类型
				var fd = new FileReader();
				fd.readAsDataURL(fs[0]);
				fd.onload = function(){ //上面文件信息读取成功之后就会走这个onload
					alert(this.result);
				}
			}
		}
	</script>
</head>
<body>
	<div id="div1">将文件拖拽到此区域</div>
</body>
</html>
~~~

**图片预览功能**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>图片预览</title>
	<style>
		#div1 {width: 200px; height: 200px; background: red; margin: 100px;}
	</style>
	<script>
		window.onload = function(){
			var oDiv = document.querySelector('#div1');
			var oUl = document.getElementById('ul1')
			var oImg = document.querySelector('img');
			var i = 0;

			oDiv.ondragenter = function(){
				this.innerHTML = '可以释放啦';
			}
			
			oDiv.ondragover = function(ev){
				var ev = ev || window.event;
				ev.preventDefault();
			}

			oDiv.ondragleave = function(){
				this.innerHTML = '将文件拖拽到此区域';
			}

			oDiv.ondrop = function(ev){
				var ev = ev || window.event;
				ev.preventDefault();
				var fs = ev.dataTransfer.files;
				/*if(fs[0].type.indexOf('image') != -1){
					var fd = new FileReader();
					fd.readAsDataURL(fs[0]);
					fd.onload = function(){ 
						var oLi = document.createElement('li');
						var oImg = document.createElement('img');
						oImg.src = this.result;
						oLi.appendChild(oImg);
						oUl.appendChild(oLi);
					}
				} else {
					alert('亲，请上传图片类型！');
				}	*/
				for(var i=0; i<fs.length; i++){
					if(fs[i].type.indexOf('image') != -1){
						var fd = new FileReader();
						fd.readAsDataURL(fs[i]);
						fd.onload = function(){ 
							var oLi = document.createElement('li');
							var oImg = document.createElement('img');
							oImg.src = this.result;
							oLi.appendChild(oImg);
							oUl.appendChild(oLi);
						}
					} else {
						alert('亲，请上传图片类型！');
					}
				}
			}
		}
	</script>
</head>
<body>
	<div id="div1">将文件拖拽到此区域</div>
	<ul id="ul1"></ul>
</body>
</html>
~~~

**拖拽购物车**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>拖拽购物车</title>
	<style>
		* {margin: 0; padding: 0;}
		li {list-style: none;}
		li {float: left; width: 200px; border: 1px solid #000; margin: 10px;}
		li img {width: 200px;}
		p {border-bottom: 1px dashed #333; height: 20px;}
		#div1 {width: 600px; border: 1px solid #000; height: 300px; clear: both;}
		.box1 {float: left; width: 200px;}
		.box2 {float: left; width: 200px;}
		.box3 {float: left; width: 200px;}
		#allMoney {float: right;}
	</style>
	<script>
		window.onload = function(){
			var aLi = document.getElementsByTagName('li');
			var oDiv = document.getElementById('div1');
			var obj = {};
			var iNum = 0;
			var allMoney = null;

			for(var i=0; i<aLi.length; i++){
				aLi[i].ondragstart = function(ev){
					var aP = this.getElementsByTagName('p');
					var ev = ev || window.event;
					ev.dataTransfer.setData('title', aP[0].innerHTML);
					ev.dataTransfer.setData('money', aP[1].innerHTML);
					ev.dataTransfer.setDragImage(this, 0, 0);
				}
			}

			oDiv.ondragover = function(ev){
				ev.preventDefault();
			}

			oDiv.ondrop = function(ev){
				ev.preventDefault();

				var sTitle = ev.dataTransfer.getData('title');
				var sMoney = ev.dataTransfer.getData('money');

				if(!obj[sTitle]){
					var oP = document.createElement('p');
					var oSpan = document.createElement('span');
					oSpan.className = 'box1';
					oSpan.innerHTML = 1;
					oP.appendChild(oSpan);
					var oSpan = document.createElement('span');
					oSpan.className = 'box2';
					oSpan.innerHTML = sTitle;
					oP.appendChild(oSpan);
					var oSpan = document.createElement('span');
					oSpan.className = 'box3';
					oSpan.innerHTML = sMoney;
					oP.appendChild(oSpan);

					oDiv.appendChild(oP);

					obj[sTitle] = 1;
				} else {
					var box1 = document.getElementsByClassName('box1');
					var box2 = document.getElementsByClassName('box2');

					for(var i=0; i<box2.length; i++){
						if(box2[i].innerHTML == sTitle){
							box1[i].innerHTML = parseInt(box1[i].innerHTML) + 1;
						}
					}
				}

				if(!allMoney){
					allMoney = document.createElement('div');
					allMoney.id = 'allMoney';
				}
				iNum += parseInt(sMoney.substring(1));
				allMoney.innerHTML = '￥' + iNum;
				oDiv.appendChild(allMoney);
			}
		}
	</script>
</head>
<body>
	<ul>
		<li draggable="true">
			<img src="images/1.png">
			<p>javascript语言精粹</p>
			<p>￥40</p>
		</li>
		<li draggable="true">
			<img src="images/2.png">
			<p>javascript权威指南</p>
			<p>￥120</p>
		</li>
		<li draggable="true">
			<img src="images/3.png">
			<p>精通javascript</p>
			<p>￥35</p>
		</li>
		<li draggable="true">
			<img src="images/4.png">
			<p>DOM编程艺术</p>
			<p>￥45</p>
		</li>
	</ul>
	<div id="div1">
		<!-- <p>
			<span class="box1">1</span>
			<span class="box2">DOM编程艺术</span>
			<span class="box3">￥45</span>
		</p>
		<p>
			<span class="box1">1</span>
			<span class="box2">DOM编程艺术</span>
			<span class="box3">￥45</span>
		</p>
		<div id="allMoney">￥90</div> -->
	</div>
</body>
</html>
~~~

##跨文档消息通信

###postMessage对象

- 接收消息的窗口对象 .postMessage()
- 一参 : 发送的数据；二参 : 接收的域
- 交互方式
	- iframe : 父页面 : contentWindow、子页面 : window.top （parent => window 如果子页面的parent页面是顶级，没有被其他页面所包含，那么parent就是当前页面的window对象；如果被包含了，则parent就是包含当前页面的父级页面的window对象。window：当前窗口；parent：父级窗口；top：顶级窗口）
	- 窗口页 : 父页面 : window.open、子页面 : window.opener
- 接收事件
	- message
	- ev.origin : 发送数据来源的域
	- ev.data : 发送的数据

- 同域下多窗口之间的通信可以采用以下方法：
	- iframe 我们可以通过js去访问被包含页面的DOM元素
	- window.open

**通过iframe进行窗口间通信(同域)**

~~~ html
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title></title>
<script>
/*
我们可以通过js去访问被包含页面的DOM元素
*/
window.onload = function() {
	
	var oBtn = document.getElementById('btn');
	var oMyIframe = document.getElementById('myframe');
	
	oBtn.onclick = function() {
		
		//如果我们要操作一个iframe里面的dom元素，首先要获取到iframe引入的页面的window
		//oMyIframe.contentWindow -> 被iframe包含的页面的window对象
		//alert(oMyIframe.contentWindow);
		
		oMyIframe.contentWindow.document.body.style.background = 'red';
	}
}
</script>
</head>

<body>
	<input type="button" value="点击我，改变2.iframe.html的背景色" id="btn" />
	<iframe id="myframe" src="2.iframe.html"></iframe>
</body>
</html>
~~~

**通过window.open来进行窗口间通信（同域）**

~~~ html
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>无标题文档</title>
<script>
window.onload = function() {
	
	var oBtn = document.getElementById('btn');
	var oBtn2 = document.getElementById('btn2');
	var newWindow = null;
	
	oBtn.onclick = function() {
		//window.open 返回被打开窗口的window对象
		newWindow = window.open('4.window.open.html', '_blank');	
	}
	
	oBtn2.onclick = function() {
		newWindow.document.body.style.background = 'red';
	}
}
</script>
</head>

<body>
	<input type="button" value="点击我，开启一个新的窗口打开4.window.open.html页面" id="btn" />
    <input type="button" value="点击我，改变4.window.open.html页面的背景色" id="btn2" />
</body>
</html>
~~~

**通过postMessage进行跨域的窗口通信 发送消息**

~~~ html
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>无标题文档</title>
<script>
window.onload = function() {
	
	var oBtn = document.getElementById('btn');
	var oMyIframe = document.getElementById('myframe');
	
	/*
		postMessage : 可以通过这个方法给另外一个窗口发送信息
		
		接收消息的窗口的window对象.postMessage();
	*/
	
	oBtn.onclick = function() {
		
		//当本页面和包含页面不在同一个域名下的时候，这样操作就会有跨域操作安全限制问题。
		
		//oMyIframe.contentWindow.document.body.style.background = 'red';
		
		/*
		第一个参数：发送的数据
		第二个参数：接收数据的域名｛带上协议｝
		*/
		
		oMyIframe.contentWindow.postMessage('1', 'http://www.b.com');
		//alert(oMyIframe.contentWindow.postMessage)
		
	}
	
}
</script>
</head>

<body>
	<input type="button" value="点击我，改变2.iframe.html的背景色" id="btn" />
	<iframe id="myframe" src="http://www.b.com/3.postMessage.html"></iframe>
</body>
</html>
~~~

**通过message接收postMessage发来的信息**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
	<script>
	window.onload = function(){
		/*
		message: 当窗口接收到通过postMessage发送过来的数据的时候触发
		 */
		
		window.addEventListener('message', function(ev){
			//alert('b.com下的页面接受到了内容了')
			
			//message事件的事件对象保存了发送过来的内容
			//ev.data: 发送过来的数据
			//ev.origin: 发送消息的来源域
			
			//alert('我接受到了a.com页面发送过来的数据，内容是：'+ ev.data)
			//alert(ev.origin);
			
			if(ev.origin == 'www.a.com' && ev.data == '1'){
				document.body.style.background = 'red';
			}
		}, false);
	}
	</script>
</head>
<body>
	这是b.com的potMessage.html页面
</body>
</html>
~~~

###XMLHttpRequest Level 2

- XMLHttpRequest 改进版
	- 请求页面与数据页面必须属于不同的域
	- 服务器要设置响应头信息 header('Access-Control-Allow-origin:http://www.a.com') （注意，这里的a.com是可以更改的。这句话的意思就是允许访问该资源的域为http://www.a.com，注意带协议）
	- Origin值展现
	- IE : XDomainRequest
	- 新的事件 : onload等
	- [http://www.w3.org/TR/XMLHttpRequest2](http://www.w3.org/TR/XMLHttpRequest2)
	- [http://msdn.microsoft.com/en-us/library/cc288060(V5.85).aspx](http://msdn.microsoft.com/en-us/library/cc288060(V5.85).aspx)
- 进度事件
	- upload : 上传
	- FormData对象
	- ev.total(已发送的总量)、ev.loaded(待发送的总量)
	- onprogress事件

**Ajax获取同域下的内容**

~~~ html
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>无标题文档</title>
<script>
window.onload = function() {
	
	var oBtn = document.getElementById('btn');
	
	oBtn.onclick = function() {
		
		var xhr = new XMLHttpRequest();
		xhr.onreadystatechange = function() {
			if (xhr.readyState == 4) {
				if (xhr.status == 200) {
					alert(xhr.responseText);
				}
			}
		}
		xhr.open('get', 'ajax.php', true);
		xhr.send();
		
	}
	
}
</script>
</head>

<body>
	<input type="button" value="获取同域下内容" id="btn" />
</body>
</html>
~~~

**IE下的跨域请求**

~~~ html
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>无标题文档</title>
<script>
window.onload = function() {
	
	/*
	在标准浏览器下，XMLHttpRequest对象已经是升级版本，支持了更多的特性，可以跨域了
	但是，如果想实现跨域请求，还需要后端的相关配合才可以
	
	XMLHttpRequest : 增加很多功能，他也不推荐使用onreadystatechange这个事件来监听，推荐使用onload
	
	XDomainRequest : IE如果想实现跨域请求，则需要使用另外一个对象去实现
	*/
	var oBtn = document.getElementById('btn');
	
	oBtn.onclick = function() {
		
		/*var xhr = new XMLHttpRequest();
		xhr.onreadystatechange = function() {
			if (xhr.readyState == 4) {
				if (xhr.status == 200) {
					alert(xhr.responseText);
				}
			}
		}
		xhr.open('get', 'http://www.b.com/ajax.php', true);
		xhr.send();*/
		
		var oXDomainRequest = new XDomainRequest();
		oXDomainRequest.onload = function() {
			alert(this.responseText);
		}
		oXDomainRequest.open('get', 'http://www.b.com/ajax.php', true);
		oXDomainRequest.send();		
	}	
}
</script>
</head>

<body>
	<input type="button" value="获取同域下内容" id="btn" />
</body>
</html>
~~~

**Ajax实现无刷新上传**

~~~ html
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>无标题文档</title>
<style>
#div1 {width: 300px; height: 30px; border: 1px solid #000; position: relative;}
#div2 {width: 0; height: 30px; background: #CCC;}
#div3 {width: 300px; height: 30px; line-height: 30px; text-align: center; position: absolute; left: 0; top: 0;}
</style>
<script>
window.onload = function() {
	
	var oBtn = document.getElementById('btn');
	var oMyFile = document.getElementById('myFile');
	var oDiv1 = document.getElementById('div1');
	var oDiv2 = document.getElementById('div2');
	var oDiv3 = document.getElementById('div3');
	
	oBtn.onclick = function() {
		
		//alert(oMyFile.value);	//获取到的是file控件的value值，这个内容是显示给你看的文字，不是我们选择的文件
		
		//oMyFile.files file控件中选择的文件列表对象
		//alert(oMyFile.files);
		
		//我们是要通过ajax把oMyFile.files[0]数据发送给后端
		
		/*for (var attr in oMyFile.files[0]) {
			console.log( attr + ' : ' + oMyFile.files[0][attr] );
		}*/
		
		var xhr = new XMLHttpRequest();
		
		xhr.onload = function() {
			//alert(1);
			//var d = JSON.parse(this.responseText);
			
			//alert(d.msg + ' : ' + d.url);
			
			alert('OK,上传完成');
		}
		
		//alert(xhr.upload);
		var oUpload = xhr.upload;
		//alert(oUpload);
		oUpload.onprogress  = function(ev) {
			console.log(ev.total + ' : ' + ev.loaded);
			
			var iScale = ev.loaded / ev.total;
			
			oDiv2.style.width = 300 * iScale + 'px';
			oDiv3.innerHTML = iScale * 100 + '%';
			
		}
		
		xhr.open('post', 'post_file.php', true);
		xhr.setRequestHeader('X-Request-With', 'XMLHttpRequest');
		
		var oFormData = new FormData();	//通过FormData来构建提交数据
		oFormData.append('file', oMyFile.files[0]);
		xhr.send(oFormData);
		
	}
	
}
</script>
</head>

<body>
	<input type="file" id="myFile" /><input type="button" id="btn" value="上传" />
    <div id="div1">
    	<div id="div2"></div>
        <div id="div3">0%</div>
    </div>

</body>
</html>
~~~

**form的上传方式**

~~~ html
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>无标题文档</title>
</head>

<body>
	<form method="post" action="post_file.php" enctype="multipart/form-data">
    	<input type="file" name="file" />
        <input type="submit" value="上传" />
    </form>
</body>
</html>
~~~

###websocket

- 互联网协议

- [http://www.ruanyifeng.com/blog/2012/05/internet_protocol_suite_part_i.html](http://www.ruanyifeng.com/blog/2012/05/internet_protocol_suite_part_i.html)
- TCP/IP协议
	- 定义了电子设备如何连入因特网，以及数据在它们之间传输的标准（如何传输）
	- 传输数据（协议）类型：Email、www、FTP等
- HTTP协议
	- 浏览器和万维网服务器之间互相通信的规则
- HTTP协议的特点
	- 功能很强大
	- 采用请求、响应模式，单向通信
	- 短连接，响应完成连接就断开
- 实时web交互
	- 股票、聊天室、网游等应用
	- 如何实现实时应用？服务器推送

- 什么是web socket？
	- 基于TCP的双向的、全双工的数据连接
		- 双向的：客户端、服务器端
		- 全双工：数据的发送与接收，两者同步进行
	- 建立socket应用？
		- 服务器必须支持web socket
		- Nodejs的简介
			- Ryan Dahl基于Google V8引擎创造的一套用来编写高性能网络服务器的ECMAScript工具包
		- Nodejs：用js去写服务器应用

- Node.js
	- 安装node.js
	- 转到项目目录
	- 运行node scriptname.js
	- http服务器的创建
	- 安装websocket模块 npm install socket.io
	- websocket服务的创建

~~~ js
var http = require('http');

var serv = http.createServer(function(req, res) {
	
	console.log('有人进来了');
	
	/*res.writeHeader(200, {
		'content-type' : 'text/html;charset="utf-8"'
	});*/
	
	/*res.writeHeader(404, {
		'content-type' : 'text/html;charset="utf-8"'
	});
	
	res.write('你要访问的页面资源不存在！');
	res.end();*/
	
	console.log(req);
	
}).listen(8888);

console.log('服务器开启成功');
~~~

~~~ js
var http = require('http');
var fs = require('fs');

var documentRoot = 'E:/HTML5/websocket/www';

var httpServer = http.createServer(function(req, res) {
	
	var url = req.url;
	//console.log(url);
	
	var file = documentRoot + url;
	console.log(file);
	
	fs.readFile(file, function(err, data) {
		
		if (err) {
			res.writeHeader(404, {
				'content-type' : 'text/html;charset="utf-8"'
			});
			res.write('<h1>404</h1><p>你要找的页面被LEO吃了</p>');
			res.end();
		} else {
			res.writeHeader(200, {
				'content-type' : 'text/html;charset="utf-8"'
			});
			res.write(data);
			res.end();
		}
		
	});
	
}).listen(8888);
~~~

~~~ js
var http = require('http');
var fs = require('fs');
var io = require('socket.io');

var documentRoot = 'E:/HTML5/websocket/www';

var httpServer = http.createServer(function(req, res) {
	
	var url = req.url;
	//console.log(url);
	
	var file = documentRoot + url;
	console.log(file);
	
	fs.readFile(file, function(err, data) {
		
		if (err) {
			res.writeHeader(404, {
				'content-type' : 'text/html;charset="utf-8"'
			});
			res.write('<h1>404</h1><p>你要找的页面被LEO吃了</p>');
			res.end();
		} else {
			res.writeHeader(200, {
				'content-type' : 'text/html;charset="utf-8"'
			});
			res.write(data);
			res.end();
		}
		
	});
	
}).listen(8888);

var socket = io.listen(httpServer);

socket.sockets.on('connection', function(socket) {
	
	//socket
	
	//console.log('有人通过socket连接进来了');
	
	socket.emit('hello', '欢迎');
	
	/*socket.on('hellotoo', function(data) {
		console.log(data);
	})*/

	
	//socket.broadcast.emit('a');
	
	socket.broadcast.emit('a', '有新人进来了');
	
	socket.on('move', function(data) {
		
		socket.broadcast.emit('move2', data);

	});
	
});
~~~

##HTML5的离线存储（applicationCache）

- 离线应用是什么
	- 乘坐飞机、手机信号弱；去演讲的时候，可能没有网络，这个时候就可以采用离线应用
	- 离线存储如何工作的？
- 离线存储的好处
	- 没网的时候，可以正常访问
	- 快速响应页面，不必用多个HTTP占用资源带宽
	- 缓存的可以是任何文件

###搭建离线应用程序

- ① 服务器设置头信息：
	- AddType text/cache-manifest.manifest
- ② html标签加：
	- manifest="xxxxx.manifest"
- ③ 写manifest文件：离线的清单列表
	- 先写：CACHE MANIFEST
	- FALLBACK：第一个网络地址没获取到，就走第二个缓存的
	- NETWORK：无论缓存中存在与否，均从网络获取

**manifest文件**

~~~ 
CACHE MANIFEST

2.png
1.jpg

FALLBACK

style1.css style2.css

NETWORK

a.jpg
~~~

##Web Workers

- 什么是worker
	- JS的单线程（放入UI队列的个数，利用定时器解决）
	- 可以让web应用程序具备后台处理能力，对多线程的支持非常好
- Worker API
	- new Worker('后台处理的JS地址')
	- 利用postMessage传输数据
	- importScripts('导入其他JS文件')
- Worker运行环境
	- navagator: appName、appVersion、userAgent、platform
	- location: 所有属性都是只读的
	- self: 指向全局的worker对象
	- 所有的ECMA对象：Object、Array、Date等
	- XMLHttpRequest构造器
	- setTimeout和setInterval方法
	- close()方法，立刻停止worker运行
	- importScripts方法：引入其他线程文件

**Web Worker简单应用**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Web Worker</title>
	<script type="text/javascript">
		var w1 = new Worker('test.js');
		w1.postMessage('hi');
		w1.onmessage = function(ev){
			alert(ev.data);
		}
	</script>
</head>
<body>
	
</body>
</html>
~~~

~~~ js
//test.js

self.onmessage = function(ev){ //这里的self就是指自己本身，也就是w1这个web worker
	//alert(ev.data); //web worker中的js里面有些命令是不认的，例如alert就不认。

	self.postMessage(ev.data + '妙味课堂');
}
~~~

**使用Worker提高像素显字的代码性能**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>像素显字</title>
    <style>
        body {background: #000; color: white; font-size: 30px;}
        #c1 {background: #fff;}
    </style>
    <script>
        window.onload = function(){
            var oC = document.getElementById('c1');
            var oGC = oC.getContext('2d');
            var aLi = document.getElementsByTagName('li');
            for(var i=0; i<aLi.length; i++){
                aLi[i].onclick = function(){
                    var str = this.innerHTML;
                    var h = 180;
                    oGC.clearRect(0, 0, oC.width, oC.height);
                    oGC.font = h + 'px impact';
                    oGC.fillStyle = 'red';
                    oGC.textBaseline = 'top';
                    var w = oGC.measureText(str).width;
                    oGC.fillText(str, (oC.width - w) / 2, (oC.height - h) / 2);
                    var oImg = oGC.getImageData((oC.width - w) / 2, (oC.height - h) / 2, w, h);
                    oGC.clearRect(0, 0, oC.width, oC.height);

                    //下面启用的Worker
                    var w1 = new Worker('canvas.js');
                    w1.postMessage(w*h);
                    w1.onmessage = function(ev){
                        var arr = ev.data;
                        var newImg = oGC.createImageData(w, h);
                        for(var i = 0; i<arr.length; i++){
                            newImg.data[arr[i]*4] = oImg.data[4*arr[i]];
                            newImg.data[arr[i]*4+1] = oImg.data[4*arr[i]+1];
                            newImg.data[arr[i]*4+2] = oImg.data[4*arr[i]+2];
                            newImg.data[arr[i]*4+3] = oImg.data[4*arr[i]+3];
                        }
                        oGC.putImageData(newImg, (oC.width - w) / 2, (oC.height - h) / 2);
                    }     
                }
            }
        }
    </script>
</head>
<body>
    <canvas id="c1" width="400" height="400"></canvas>
    <ul style="float: left">
        <li>秒</li>
        <li>味</li>
        <li>课</li>
        <li>堂</li>
    </ul>
</body>
</html>
~~~

~~~ js
//canvas.js

function randomArr(iAll, iNow){ //从iAll个数里面随机取出iNow个数
    var arr = [];
    var newArr = [];
    for(var i=0; i<iAll; i++){
        arr.push(i);
    }
    for(var i=0; i<iNow; i++){
        newArr.push(arr.splice(Math.floor(Math.random()*arr.length), 1));
    }
    return newArr;
}

self.onmessage = function(ev){
    var arr = randomArr(ev.data, ev.data/10);
    self.postMessage(arr);
}
~~~

##HTML5其他功能

###内容编辑

- contenteditable="true"

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
    <div contenteditable="true" style="height: 200px; width: 200px; background: red;">aaaaaaaaaaa</div>
</body>
</html>
~~~

###语言输入

- &lt;input type="text" x-webkit-speech />

###桌面提醒

##地理信息（Geolocation）

- 地理位置
	- 经度：南北极的连接线
	- 维度：东西连接的线
- 位置信息从何而来
	- IP地址
	- GPS全球定位系统
	- Wi-Fi无线网络
	- 基站
- 地理位置对象
	- navigator.geolocation
		- 单次定位请求：getCurrentPosition(请求成功, 请求失败, 数据收集方式)
		- 请求成功函数
			- 经度：coords.longitude
			- 维度：coords.latitude
			- 准确度：coords.accuracy
			- 海拔：coords.altitude
			- 海拔准确度：coords.altitudeAcuracy
			- 行进方向：coords.heading
			- 地面速度：coords.speed
			- 时间戳：new Date(position.timestamp)
		- 请求失败函数
			- 失败编号：code
			- 0：不包括其他错误编号中的错误
			- 1：用户拒绝浏览器获取位置信息
			- 2：尝试获取用户信息，但失败了
			- 3：设置了timeout值，获取位置超时了
		- 数据收集：json的形式
			- enableHighAcuracy：更精确的查找，默认false
			- timeout：获取位置允许最长时间，默认infinity
			- maximumAge：位置可以缓存的最大时间，默认0
		- 多次定位请求：watchPosition(像setInterval)
			- 移动设备有用，位置改变才会触发
			- 配置参数：frequency 更新的频率
		- 关闭更新请求：clearWatch(像clearInterval)
- 百度地图API
	- &lt;script src="http://api.map.baidu.com/api?v=1.3">&lt;/script>
	- 创建基于地图的应用

**单次定位请求**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <script>
    // LBS：基于地理信息的应用
    window.onload = function(){
        var oInput = document.getElementById('input1');
        var oT = document.getElementById('t1');
        
        oInput.onclick = function(){
        
            navigator.geolocation.getCurrentPosition(function(position){
                
                oT.value += '经度:' + position.coords.longitude+'\n';
                oT.value += '纬度 :' + position.coords.latitude+'\n';
                oT.value += '准确度 :' + position.coords.accuracy+'\n';
                oT.value += '海拔 :' + position.coords.altitude+'\n';
                oT.value += '海拔准确度 :' + position.coords.altitudeAcuracy+'\n';
                oT.value += '行进方向 :' + position.coords.heading+'\n';
                oT.value += '地面速度 :' + position.coords.speed+'\n';
                oT.value += '时间戳:' + new Date(position.timestamp)+'\n';
                    
                
            }, function(err){
                
                //err.code // 失败所对应的编号
                
                alert( err.code );
                
            }, {
                enableHighAcuracy : true,
                timeout : 5000,
                maximumAge : 5000
            });
            
        };

    }
    </script>
</head>
<body>
<input type="button" value="请求" id="input1"><br>
<textarea id="t1" style="width: 400px; height: 400px; border: 1px solid #000"></textarea>
</body>
</html>
~~~

**多次定位请求**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <script>
    // LBS：基于地理信息的应用
    window.onload = function(){
        var oInput = document.getElementById('input1');
        var oT = document.getElementById('t1');
        var timer = null;
        
        oInput.onclick = function(){
        
            timer = navigator.geolocation.watchPosition(function(position){
                
                oT.value += '经度:' + position.coords.longitude+'\n';
                oT.value += '纬度 :' + position.coords.latitude+'\n';
                oT.value += '准确度 :' + position.coords.accuracy+'\n';
                oT.value += '海拔 :' + position.coords.altitude+'\n';
                oT.value += '海拔准确度 :' + position.coords.altitudeAcuracy+'\n';
                oT.value += '行进方向 :' + position.coords.heading+'\n';
                oT.value += '地面速度 :' + position.coords.speed+'\n';
                oT.value += '时间戳:' + new Date(position.timestamp)+'\n';
                    
                
            }, function(err){
                
                //err.code // 失败所对应的编号
                alert( err.code );

                navigator.geolocation.clearWatch(timer);
                
            }, {
                enableHighAcuracy : true,
                timeout : 5000,
                maximumAge : 5000,
                frequency : 1000
            });
            
        };

    }
    </script>
</head>
<body>
<input type="button" value="请求" id="input1"><br>
<textarea id="t1" style="width: 400px; height: 400px; border: 1px solid #000"></textarea>
</body>
</html>
~~~

**地图应用**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>地图应用</title>
    <style>
	#div1{ width:400px; height:400px; border:1px #000 solid;}
	</style>
	<script src="h	ttp://api.map.baidu.com/api?v=1.3"></script>
	<script>

	window.onload = function(){
		var oInput = document.getElementById('input1');
		
		oInput.onclick = function(){
			
			navigator.geolocation.getCurrentPosition(function(position){
				
				var y = position.coords.longitude;
				var x = position.coords.latitude;
				
				var map = new BMap.Map("div1");
				
				var pt = new BMap.Point(y, x);
				
				map.centerAndZoom(pt, 14);
				map.enableScrollWheelZoom();
				var myIcon = new BMap.Icon("miaov.png", new BMap.Size(30,30));
				var marker2 = new BMap.Marker(pt,{icon:myIcon});  // 创建标注
				map.addOverlay(marker2); 
				
				var opts = {
				  width : 200,     // 信息窗口宽度
				  height: 60,     // 信息窗口高度
				  title : "妙味课堂"  // 信息窗口标题
				}
				var infoWindow = new BMap.InfoWindow("IT培训机构", opts);  // 创建信息窗口对象
				map.openInfoWindow(infoWindow,pt); //开启信息窗口		
			});
		};
	};
	</script>
</head>

<body>
<input type="button" value="请求" id="input1" />
<div id="div1"></div>
</body>
</html>
~~~

##本地存储

- cookie
	- 数据存储到计算机中，通过浏览器控制添加与删除数据
- cookie的特点
	- 存储限制
		- 域名100个cookie，每组值大小4KB
	- 客户端、服务器端，都会请求服务器（头信息）
	- 页面间的cookie是共享的
- storage
	- sessionStorage
		- session临时回话，从页面打开到页面关闭的时间段
		- 窗口的临时存储，页面关闭，本地存储消失
	- localStorage
		- 永久存储（可以手动删除数据）
- storage的特点
	- 存储量限制（5M）
	- 客户端完成，不会请求服务器处理
	- sessionStorage数据是不共享、localStorage共享
- storage API
	- setItem()
		- 设置数据，key\value类型，类型都是字符串
		- 可以用获取属性的形式操作
	- getItem()
		- 获取数据，通过key来获取到相应的value
	- removeItem()
		- 删除数据，通过key来删除相应的value
	- clear()
		- 删除全部存储的值
	- 例子：保存注册信息
	- 存储事件
		- 当数据有修改或删除的情况下，就会触发storage事件
		- 在对数据进行改变的窗口对象上是不会触发的
		- key：修改或删除的key值，如果调用clear()，key为null
		- newValue：新设置的值，如果调用removeStorage()，key为null
		- oldValue：调用改变前的value值
		- storageArea：当前的storage对象
		- url：触发该脚本变化的文档的url
		- 注：session同窗口才可以，例子：iframe操作
	- 例子：同步购物车
- 综合实例
	- 行走日记
		- 地图
		- 本地存储

**Storage API**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>本地存储</title>
    <style></style>
    <script>
    window.onload = function(){
        var aInput = document.getElementsByTagName('input');
        aInput[0].onclick = function(){ //设置
            // sessionStorage : 临时性存储
            // localStorage : 永久性存储
            
            //window.sessionStorage.setItem('name', aInput[3].value);
            window.localStorage.setItem('name', aInput[3].value);
        }

        aInput[1].onclick = function(){ //获取
            //alert(window.sessionStorage.getItem('name'));
            alert(window.localStorage.getItem('name'));
        }

        aInput[2].onclick = function(){ //删除
            //window.localStorage.removeItem('name');
            window.localStorage.clear(); //删除全部数据
        }
    }
    </script>
</head>
<body>
<input type="button" value="设置">
<input type="button" value="获取">
<input type="button" value="删除">
<input type="text">
</body>
</html>
~~~

**保存注册信息**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>保存注册信息</title>
    <style></style>
    <script>
    window.onload = function(){
        var aInput = document.getElementsByTagName('input');
        var oT = document.getElementById('t1');

        if(window.localStorage.getItem('name')){
            aInput[0].value = window.localStorage.getItem('name');
        }

        if(window.localStorage.getItem('sex')){
           for(var i=1; i<aInput.length; i++){
            if(aInput[i].value == window.localStorage.getItem('sex')){
                aInput[i].checked = true;
            }
           }
        }

        if(window.localStorage.getItem('ta')){
           oT.value = window.localStorage.getItem('ta');
        }

        window.onunload = function(){
            if(aInput[0].value){
                window.localStorage.setItem('name', aInput[0].value);
            }

            for(var i=1; i<aInput.length; i++){
                if(aInput[i].checked == true){
                    window.localStorage.setItem('sex', aInput[i]);
                }
            }

            if(oT.value){
                window.localStorage.setItem('ta', oT.value);
            }
        }
    }
    </script>
</head>
<body>
<p>
    用户名：<input type="text">
</p>
<p>
    性别：男 <input type="radio" name="sex">女 <input type="radio" name="sex">
</p>
内容：<textarea id="t1"></textarea>
</body>
</html>
~~~

**storage事件**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>本地存储</title>
    <style></style>
    <script>
    window.onload = function(){
        var aInput = document.getElementsByTagName('input');
        aInput[0].onclick = function(){
            window.localStorage.setItem('name', aInput[3].value);
        }

        aInput[1].onclick = function(){ 
            alert(window.localStorage.getItem('name'));
        }

        aInput[2].onclick = function(){
            window.localStorage.removeItem('name');
        }

        window.addEventListener('storage', function(ev){ //当前页面的事件不会触发，其他页面会触发
            alert(123);
            
            console.log(ev.key);
            console.log(ev.newValue);
            console.log(ev.oldValue);
            console.log(ev.storageArea);
            console.log(ev.url);

        }, false);
    }
    </script>
</head>
<body>
<input type="button" value="设置">
<input type="button" value="获取">
<input type="button" value="删除">
<input type="text">
</body>
</html>
~~~

**同步购物车**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>同步购物车</title>
    <style></style>
    <script>
    window.onload = function(){
        var aInput = document.getElementsByTagName('input');

        for(var i=0; i<aInput.length; i++){
            aInput[i].onclick = function(){
                if(this.checked){
                    window.localStorage.setItem('sel', this.value);
                } else {
                    window.localStorage.setItem('unSel', this.value)
                }
            }
        }

        window.addEventListener('storage', function(ev){
            if(ev.key == 'sel'){
                for(var i=0; i<aInput.length; i++){
                    if(ev.newValue == aInput[i].value){
                        aInput[i].checked = true;
                    }
                }
            } else if(ev.key == 'unSel'){
                for(var i=0; i<aInput.length; i++){
                    if(ev.newValue == aInput[i].value){
                        aInput[i].checked = false;
                    }
                }
            }
        }, false);
    }
    </script>
</head>
<body>
<input type="checkbox" value="香蕉">香蕉<br>
<input type="checkbox" value="苹果">苹果<br>
<input type="checkbox" value="西瓜">西瓜<br>
<input type="checkbox" value="哈密瓜">哈密瓜<br>
</body>
</html>
~~~

**行走日记**

~~~ html
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>无标题文档</title>
<style>
*{ margin:0; padding:0;}
li{ list-style:none;}
#div1,#div2{ float:left; width:400px; height:400px; border:1px #000000 solid; margin:10px; position:relative; overflow:hidden;}
#div2 ul{ position:absolute; left:0; width:2000px;}
#div2 ul .box{ width:400px; height:400px; float:left; overflow:hidden;}
#div2 #childUl{ width:400px;}
#childUl li{ width:400px; border-bottom:1px #666666 dashed;}
#map{ width:100%; height:380px;}
</style>
<script src="move.js"></script>
<script src="http://api.map.baidu.com/api?v=1.3"></script>
<script>

window.onload = function(){
	var oDiv = document.getElementById('div1');
	var aInput = oDiv.getElementsByTagName('input');
	var oT = document.getElementById('t1');
	
	var iNow = window.localStorage.getItem('num') || 0;
	
	var oChildUl = document.getElementById('childUl');
	var aChildLi = oChildUl.getElementsByTagName('li');
	
	var oUl = document.getElementById('ul1');
	var aBox = oUl.getElementsByClassName('box');
	
	var aBox1_input = aBox[1].getElementsByTagName('input');
	var aBox1_div = aBox[1].getElementsByTagName('div');
	
	var oBox2_input = aBox[2].getElementsByTagName('input')[0];
	var index = 0;
	
	if( window.localStorage.getItem('num') ){
		
		for(var i=0;i<iNow;i++){
			
			var oLi = document.createElement('li');
			oLi.innerHTML = window.localStorage.getItem('title'+i);
			oChildUl.appendChild( oLi );
			
		}
		
		changeLi();
		
	}
	
	
	aInput[1].onclick = function(){  //保存本地
	
		window.localStorage.setItem('title'+iNow,aInput[0].value);
		window.localStorage.setItem('ta'+iNow,oT.value);
		
		createLi();
		
		iNow++;
		
		window.localStorage.setItem('num',iNow);
	
	};
	
	aInput[2].onclick = function(){ //提交后台
	};
	
	aInput[3].onclick = function(){ //删除所有的数据
		window.localStorage.clear();
	};
	
	aInput[4].onclick = function(){
		
		var This = this;
		
		navigator.geolocation.getCurrentPosition(function(position){
			
			var y = position.coords.longitude;
			var x = position.coords.latitude;
			
			
			if( This.checked ){
				window.localStorage.setItem('y'+iNow,y);
				window.localStorage.setItem('x'+iNow,x);
			}
			else{
				window.localStorage.removeItem('y'+iNow);
				window.localStorage.removeItem('x'+iNow);
			}
			
			
		});
		
		
		
	};
	
	function createLi(){
		
		var oLi = document.createElement('li');
		oLi.innerHTML = window.localStorage.getItem('title'+iNow);
		oChildUl.appendChild( oLi );
		
		changeLi();
		
	}
	
	function changeLi(){
		
		for(var i=0;i<aChildLi.length;i++){
			aChildLi[i].index = i;
			aChildLi[i].onclick = function(){
				
				startMove(oUl,{left : -aBox[0].offsetWidth });
				
				aBox1_div[0].innerHTML = window.localStorage.getItem('title'+this.index);
				aBox1_div[1].innerHTML = window.localStorage.getItem('ta'+this.index);
				
				
				if( window.localStorage.getItem('y'+this.index) ){
					aBox1_input[1].disabled = false;
					
				}
				else{
					aBox1_input[1].disabled = true;
				}
				
				index = this.index;
				
			};
		}
		
	}
	
	aBox1_input[0].onclick = function(){
		
		startMove(oUl,{left : 0});
		
	};
	
	aBox1_input[1].onclick = function(){
		
		startMove(oUl,{left : -2*aBox[0].offsetWidth});
		
		
		var map = new BMap.Map("map");            
		var y = window.localStorage.getItem('y'+index);
		var x = window.localStorage.getItem('x'+index);
		var title = window.localStorage.getItem('title'+index);
		var text = window.localStorage.getItem('ta'+index);
		var point = new BMap.Point(y, x);    
		map.centerAndZoom(point,15);                    
		map.enableScrollWheelZoom();
		
		var marker1 = new BMap.Marker(point);
		map.addOverlay(marker1); 
		
		var opts = {
		  width : 250,     // 信息窗口宽度
		  height: 100,     // 信息窗口高度
		  title : title  // 信息窗口标题
		}
		
		var infoWindow = new BMap.InfoWindow(text, opts);
		map.openInfoWindow(infoWindow,point);
		
		
	};
	
	oBox2_input.onclick = function(){
		
		startMove(oUl,{left : -aBox[0].offsetWidth });
		
	};
	
};

</script>
</head>

<body>
<div id="div1">
标题:<input type="text" /><br />
内容:<textarea id="t1" style="height:300px; width:300px;"></textarea><br />
<input type="button" value="保存本地" />
<input type="button" value="同步服务器" />
<input type="button" value="删除所有数据" />
<input type="checkbox" />记录地图位置
</div>
<div id="div2">
	<ul id="ul1">
		<li class="box">
			<ul id="childUl">
			</ul>
		</li>
		<li class="box">
			<input type="button" value="后退" />
			<input style="float:right" type="button" value="前进" />
			<div></div>
			<div></div>
		</li>
		<li class="box">
			<input type="button" value="后退" />
			<div id="map"></div>
		</li>
	</ul>
</div>
</body>
</html>

~~~

##音频和视频

- 标签
	- audio、video
	- source
- 视频容器
	- 容器文件，类似于压缩了一组文件
		- 音轨频道
		- 视频轨道
		- 元数据：封面、标题、字幕等
		- 格式：.avi、.flv、.mp4、.mkv、.ogv等
- 编解码器
	- 原始的视频容器非常大，添加需编码，播放需解码
	- 音频编解码器
		- AAC、MPEG-3、Ogg Vorbis
	- 视频编解码器
		- H.264、VP8、Ogg Theora
- 媒体元素
	- controls：显示或隐藏用户控制界面
	- autoplay：媒体是否自动播放
	- loop：媒体是否循环播放
	- currentTime：开始到播放现在所用的时间
	- duration：媒体总时间（只读）
	- volume：0.0 — 1.0 的音量相对值
	- muted：是否静音
	- autobuffer：开始的时候是否缓冲加载，autoplay的时候，忽略此属性
	- paused：媒体是否暂停（只读）
	- ended：媒体是否播放完毕（只读）
	- error：媒体发声错误的时候，返回错误代码（只读）
	- currentSrc：以字符串的形式返回媒体地址（只读）
	- play()：媒体播放
	- pause()：媒体暂停
	- load()：重新加载媒体
	- 媒体元素中的事件：loadstart progress suspend emptied stalled play pause loadedmetadata loadeddata waiting playing canplay canplaythrough seeking seeked timeupdate ended ratechange durationchange volumechange
- video额外特性
	- poster：视频播放前的预览图片
	- width、height：设置视频的尺寸
	- videoWidth、videoHeight：视频的实际尺寸（只读）
	- 例子：带声音的导航
	- 例子：视频与canvas结合
	- 例子：自制播放器
	- [http://www.alloyteam.com/wp-content/uploads/2012/03/palydemo/index.html](http://www.alloyteam.com/wp-content/uploads/2012/03/palydemo/index.html)

**音视频的基本操作**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>HTML5音视频</title>
    <style></style>
    <script>
    window.onload = function(){
        var oA = document.getElementById('a1');
        var oV = document.getElementById('v1');
        var oInput = document.getElementById('input1');
        var aS = document.getElementsByTagName('source');

        // setInterval(function(){
        //     console.log(oA.currentTime);
        // }, 1000);
        
        oA.currentTime = 60; //音频从60秒开始播放 currentTime属性既可以读取也可以设置
        console.log(oA.duration);
        console.log(oA.volume);
        console.log(oA.muted); //静音就返回真；否则就返回假
        console.log(oA.paused);
        console.log(oA.ended);
        console.log(oA.error);
        console.log(oA.currentSrc);

        oV.onmouseover = function(){
            this.play();
        }
        oV.onmouseout = function(){
            this.pause();
        }

        oInput.onclick = function(){
            aS[0].src = 'XXXX.mp4';
            aS[1].src = 'XXXX.ogv';

            oV.load();
        }

        oV.poster = 'images/1.png';

        oV.addEventListener('ended', function(){
            alert(123);
        }, false)
    }
    </script>
</head>
<body>
<!-- <audio controls src="johann_sebastian_bach_air.mp3"></audio>
<audio controls src="johann_sebastian_bach_air.ogg"></audio>
<video controls src="Intermission-Walk-in_512kb.mp4"></video>
<video controls src="Intermission-Walk-in.ogv"></video> -->

<!-- <video controls>
    //先找第一个source，如果浏览器不支持第一个，就找下一个
    <source src="Intermission-Walk-in.ogv"></source>
    <source src="Intermission-Walk-in_512kb.mp4"></source>
</video> -->

<audio id="a1" controls autobuffer src="johann_sebastian_bach_air.mp3"></audio>

<input type="button" value="重新加载" id="input1">
<video id="v1">
    //先找第一个source，如果浏览器不支持第一个，就找下一个
    <source src="Intermission-Walk-in.ogv"></source>
    <source src="Intermission-Walk-in_512kb.mp4"></source>
</video>
</body>
</html>
~~~

**带声音的导航**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>带声音的导航</title>
    <style>
    * {margin: 0; padding: 0;}
    #ul1 {width: 1000px; height: 30px;}
    #ul1 li {list-style: none; width: 100px; height: 30px; background: red; color: white; border: 1px solid #000; float: left; text-align: center; line-height: 30px;}
    </style>
    <script>
    window.onload = function(){
        var aLi = document.getElementsByTagName('li');
        var oA = document.getElementById('a1');

        for(var i=0; i<aLi.length; i++){
            aLi[i].onmouseover = function(){
                //this.getAttribute('au')
                oA.src = 'http://s8.qhimg.com/share/audio/piano1/' + this.getAttribute('au') + '4.mp3';
                oA.play();
            }
        }
    }
    </script>
</head>
<body>
<ul id="ul1">
    <li au="c">00001</li>
    <li au="d">00002</li>
    <li au="e">00003</li>
    <li au="f">00004</li>
    <li au="g">00005</li>
    <li au="a">00006</li>
    <li au="b">00007</li>
</ul>
<audio id="a1"></audio>
</body>
</html>
~~~

**视频与canvas结合**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>视频与canvas结合</title>
    <style></style>
    <script>
    window.onload = function(){
        var oV = document.getElementById('v1');
        var oC = document.getElementById('c1');
        var oGC = oC.getContext('2d');

        oC.width = oV.videoWidth;
        oC.height = oV.videoHeight;

        setInterval(function(){
            oGC.drawImage(oV, 0, 0); //drawImage里面也可以添加视频
        }, 30);
    }
    </script>
</head>
<body>
<video controls id="v1">
    <source src="Intermission-Walk-in.ogv"></source>
    <source src="Intermission-Walk-in.mp4"></source>
</video>
<canvas id="c1"></canvas>
</body>
</html>
~~~

**自制播放器**

~~~ html
<!DOCTYPE html>
<head>
<title>无标题文档</title>
<style>
*{ margin:0; padding:0;}
#div1{ width:300px; height:30px; background:#666; overflow:hidden; position:relative;}
#div2{ width:60px; height:30px; background:red; position:absolute; left:0; top:0;}

#div3{ width:300px; height:10px; background:#666; overflow:hidden; position:relative; top:10px;}
#div4{ width:60px; height:10px; background:yellow; position:absolute; left:240px; top:0;}

</style>
<script>

window.onload = function(){
	var oV = document.getElementById('v1');
	var aInput = document.getElementsByTagName('input');	
	var oDiv1 = document.getElementById('div1');
	var oDiv2 = document.getElementById('div2');
	var oDiv3 = document.getElementById('div3');
	var oDiv4 = document.getElementById('div4');	
	var disX = 0;
	var disX2 = 0;	
	var timer = null;
	
	aInput[0].onclick = function(){		
		if( oV.paused ){		
			oV.play();		
			this.value = '暂停';		
			nowTime();
			timer = setInterval(nowTime,1000);		
		}else{	
			oV.pause();
			this.value = '播放';
			clearInterval(timer);
		}
	};
	
	
	aInput[2].value = changeTime(oV.duration);
	aInput[3].onclick = function(){
		if( oV.muted ){
			oV.volume = 1;
			this.value = '静音';
			oV.muted = false;
		}else{
			oV.volume = 0;
			this.value = '取消静音';
			oV.muted = true;
		}
	};
	
	aInput[4].onclick = function(){ //全屏方法
		if (oV.requestFullscreen) {
          oV.requestFullscreen();
        } else if (oV.msRequestFullscreen) {
          oV.msRequestFullscreen();
        } else if (oV.mozRequestFullScreen) {
          oV.mozRequestFullScreen();
        } else if (oV.webkitRequestFullscreen) {
          oV.webkitRequestFullscreen();
        }
	};
	
	
	function nowTime(){
		aInput[1].value = changeTime(oV.currentTime);
		var scale = oV.currentTime/oV.duration;
		oDiv2.style.left = scale * 240 + 'px';
	}
	
	function changeTime(iNum){
		iNum = parseInt( iNum );
		var iH = toZero(Math.floor(iNum/3600));
		var iM = toZero(Math.floor(iNum%3600/60));
		var iS = toZero(Math.floor(iNum%60));
		return iH + ':' +iM + ':' + iS;
	}
	
	function toZero(num){
		if(num<=9){
			return '0' + num;
		}
		else{
			return '' + num;
		}
	}
	
	oDiv2.onmousedown = function(ev){
		var ev = ev || window.event;
		disX = ev.clientX - oDiv2.offsetLeft;
		
		document.onmousemove = function(ev){
			var ev = ev || window.event;
			var L = ev.clientX - disX;
			
			if(L<0){
				L = 0;
			}else if(L>oDiv1.offsetWidth - oDiv2.offsetWidth){
				L = oDiv1.offsetWidth - oDiv2.offsetWidth;
			}
			oDiv2.style.left = L + 'px';
			
			var scale = L/(oDiv1.offsetWidth - oDiv2.offsetWidth);
			oV.currentTime = scale * oV.duration;
			nowTime();
			
		};
		document.onmouseup = function(){
			document.onmousemove = null;
		};
		return false;
	};
	
	
	oDiv4.onmousedown = function(ev){
		var ev = ev || window.event;
		disX2 = ev.clientX - oDiv4.offsetLeft;
		
		document.onmousemove = function(ev){
			var ev = ev || window.event;
			var L = ev.clientX - disX2;
			if(L<0){
				L = 0;
			}else if(L>oDiv3.offsetWidth - oDiv4.offsetWidth){
				L = oDiv3.offsetWidth - oDiv4.offsetWidth;
			}
			oDiv4.style.left = L + 'px';
			
			var scale = L/(oDiv3.offsetWidth - oDiv4.offsetWidth);
			oV.volume = scale;
		};
		document.onmouseup = function(){
			document.onmousemove = null;
		};
		return false;
	};
};

</script>
</head>
<body>
<video id="v1">
	<source src="Intermission-Walk-in.ogv"></source>
    <source src="Intermission-Walk-in_512kb.mp4"></source>
</video><br />
<input type="button" value="播放" />
<input type="button" value="00:00:00" />
<input type="button" value="00:00:00" />
<input type="button" value="静音" />
<input type="button" value="全屏" />
<div id="div1">
	<div id="div2"></div>
</div>
<div id="div3">
	<div id="div4"></div>
</div>
</body>
</html>
~~~
