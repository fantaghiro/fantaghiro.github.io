---
layout: post
title: JS与三角函数
category: study
description: 妙味课堂 JS与三角函数学习笔记
tags:
- 学习笔记
- js
---

#三角函数与JavaScript

##直角三角形

###勾股定理

- 可以实现两点坐标求距离的应用
- JS中的平方和开放
- 例子：苹果菜单

```html
//苹果菜单
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8">
	<title>苹果菜单</title>
	<style type="text/css">
		* {margin: 0; padding: 0;}
		#div1 {width: 100%; position: absolute; bottom: 0; text-align: center;}
		img {width: 64px;}
	</style>
	<script type="text/javascript">
		window.onload = function(){
			var aInput = document.getElementsByTagName('input');
			var oDiv = document.getElementById('div1');
			var aImg = oDiv.getElementsByTagName('img');

			document.onmousemove = function(ev){
				var ev = ev || window.event;
				for(var i = 0; i < aImg.length; i++){
					var x = aImg[i].offsetLeft + aImg[i].offsetWidth / 2;
					var y = aImg[i].offsetTop + oDiv.offsetTop + aImg[i].offsetHeight / 2;

					var b = ev.clientX - x;
					var a = ev.clientY - y;
					var c = Math.sqrt(Math.pow(a, 2) + Math.pow(b, 2));

					var scale = 1- c / 300;

					if(scale < 0.5){
						scale = 0.5;
					}
					aInput[i].value = scale;

					aImg[i].style.width = scale * 128 + 'px';
					aImg[i].style.height = scale * 128 + 'px';

				}

			}

				
		}
	</script>
</head>
<body>
	<input type="text">
	<input type="text">
	<input type="text">
	<input type="text">
	<input type="text">
	<div id="div1">
		<img src="img/1.png">
		<img src="img/2.png">
		<img src="img/3.png">
		<img src="img/4.png">
		<img src="img/5.png">
	</div>
</body>
</html>
```

##三角函数

- sinα （对边与斜边的比值） cosα （临边比斜边的比值） tanα （对边与临边的比）
- JS中的表示语法

```js
Math.sin(弧度);
Math.cos(弧度);
Math.tan(弧度);
```

##角度

- 角度与弧度的关系
	- 1弧度的概念（一个圆中，一定角度对应的圆弧，把它拉直了，如果长度等于半径的话，那么这个角度就是一弧度）
	- 360 = 2π；1° = π/180; 一弧度=180/π
	- 例子：圆周运动
	- 三维运动（三维旋转矩阵）

```html
//圆周运动
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8">
	<title>圆周运动</title>
	<style type="text/css">
		#div1 {width: 20px; height: 20px; background: red; position: absolute; left: 800px; top: 300px;}
		.box {border: 1px #000 solid; position: absolute;}
	</style>
	<script type="text/javascript">
		window.onload = function(){
			var oDiv = document.getElementById("div1");
			var r = 100;
			var x = 700;
			var y = 300;
			var num = 0;

			setInterval(function(){
				num++;
				// Math.sin(num * Math.PI/180) = a/r;
				// Math.cos(num * Math.PI/180) = b/r;
				var a = Math.sin(num * Math.PI/180) * r;
				var b = Math.cos(num * Math.PI/180) * r;

				oDiv.style.left = x + b + 'px';
				oDiv.style.top = y + a + 'px';

				var oBox = document.createElement('div');
				oBox.className = "box";
				document.body.appendChild(oBox);

				oBox.style.left = oDiv.offsetLeft + 'px';
				oBox.style.top = oDiv.offsetTop + 'px';
			}, 30);
		}
	</script>
</head>
<body>
	<div id="div1"></div>
</body>
</html>
```

```html
//三维运动，利用近大远小
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8">
	<title>三维圆周运动</title>
	<style type="text/css">
		#div1 {width: 20px; height: 20px; background: red; position: absolute; left: 800px; top: 300px;}
		.box {border: 1px #000 solid; position: absolute;}
	</style>
	<script type="text/javascript">
		window.onload = function(){
			var oDiv = document.getElementById("div1");
			var r = 100;
			var x = 700;
			var y = 300;
			var num = 0;

			setInterval(function(){
				num++;
				// Math.sin(num * Math.PI/180) = a/r;
				// Math.cos(num * Math.PI/180) = b/r;
				var a = Math.sin(num * Math.PI/180) * r;
				var b = Math.cos(num * Math.PI/180) * r;

				oDiv.style.left = x + b + 'px';
				//oDiv.style.top = y + a + 'px';
				
				oDiv.style.width = a / 100 * 30 + 50;
				oDiv.style.height = a / 100 * 30 + 50;

				// var oBox = document.createElement('div');
				// oBox.className = "box";
				// document.body.appendChild(oBox);

				// oBox.style.left = oDiv.offsetLeft + 'px';
				// oBox.style.top = oDiv.offsetTop + 'px';
			
			}, 30);	
		}
	</script>
</head>
<body>
	<div id="div1"></div>
</body>
</html>
```

##反三角函数

- arcsinα arccosα arctanα
	- 利用反三角函数，可以求未知的角度（或弧度）
- JS中的表示语法

```js
Math.asin(1/2); //求出来的是弧度
Math.acos();
Math.atan();
```

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8">
	<title>265网站眼睛跟随鼠标</title>
	<style type="text/css">
		* {margin: 0; padding: 0;}
		#div1 {width: 176px; height: 91px; background: url(265.png) no-repeat; posotion: absolute; left: 300px; top: 200px;} //这个是背景图
		#div2 {border: 2px #000 solid; position: absolute; left: 115px; top: 43px; border-radius: 50%;}
		#div3 {	border: 2px #000 solid; position: absolute; left: 135px; top: 43px;	border-radius: 50%;} //#div2和#div3就是小眼睛
	</style>
	<script type="text/javascript">
		window.onload = function(){
			var oDiv2 = document.getElementById('div2');
			var oDiv3 = document.getElementById('div3');

			var r = 5; //眼睛在半径为5的范围内运动
			var L2 = 115;
			var T2 = 43;
			var L3 = 135;
			var T3 = 43;

			document.onmousemove = function(ev){
				var ev = ev || window.event;

				change(oDiv2, ev.clientX, ev.clientY, L2, T2);
				change(oDiv3, ev.clientX, ev.clientY, L3, T3);

				function change(obj, x, y, l, t){
					var changeX = 0;
					var changeY = 0;

					var b = Math.abs(x - (obj.offsetLeft + obj.parentNode.offsetLeft));
					var a = Math.abs(y - (obj.offsetTop + obj.parentNode.offsetTop));

					if(x > obj.offsetLeft + obj.parentNode.offsetLeft && y < obj.offsetTop + obj.parentNode.offsetTop){ //右上
						changeX = Math.sin(Math.atan(b/a)) * r;
						changeY = Math.cos(Math.atan(b/a)) * -r;
					} else if(x > obj.offsetLeft + obj.parentNode.offsetLeft && y > obj.offsetTop + obj.parentNode.offsetTop){ //右下
						changeX = Math.sin(Math.atan(b/a)) * r;
						changeY = Math.cos(Math.atan(b/a)) * r;
					} else if(x < obj.offsetLeft + obj.parentNode.offsetLeft && y > obj.offsetTop + obj.parentNode.offsetTop){ //左下
						changeX = Math.sin(Math.atan(b/a)) * -r;
						changeY = Math.cos(Math.atan(b/a)) * r;
					} else if(x < obj.offsetLeft + obj.parentNode.offsetLeft && y < obj.offsetTop + obj.parentNode.offsetTop){ //左上
						changeX = Math.sin(Math.atan(b/a)) * -r;
						changeY = Math.cos(Math.atan(b/a)) * -r;
					}

					obj.style.left = l + changeX + 'px';
					obj.style.top = t + changeY + 'px';
				}

			}
		}
	</script>
</head>
<body>
	<div id="div1">
		<div id="div2"></div>
		<div id="div3"></div>
	</div>
</body>
</html>
```

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8">
	<title>圆的碰撞检测(只做了一个方向的)</title>
	<style type="text/css">
		* {margin: 0 padding: 0;}
		#div1 {width: 200px; height: 200px; background: red; border-radius: 50%; position: absolute; left: 700px; top: 100px;}
		#div2 {width: 100px; height: 100px; background: blue; border-radius: 50%; position: absolute; left: 100px; top: 250px;}
	</style>
	<script type="text/javascript">
		window.onload = function(){
			var oDiv1 = document.getElementById("div1");
			var oDiv2 = document.getElementById("div2");

			var sX1 = 0;
			var sY1 = 0;
			var sX2 = 10;
			var sY2 = 0;

			setInterval(function(){
				oDiv2.style.left = oDiv2.offsetLeft + 10 + 'px';

				var a = Math.abs((oDiv1.offsetLeft + 100) - (oDiv2.offsetLeft + 50));
				var b = Math.abs((oDiv1.offsetTop + 100) - (oDiv2.offsetTop + 50));
				var c = Math.sqrt(Math.pow(a, 2) + Math.pow(b, 2));

				if(c <= 100 + 50){
					//alert("碰上了");
					var ang = Math.asin(b/c);
					var s1 = Math.cos(ang) * sX2;
					var s2 = Math.sin(ang) * sX2;

					var x2change1 = Math.cos(ang)*(-s1);
					var y2change1 = Math.sin(ang)*s1;

					var x2change2 = Math.sin(ang) * s2;
					var y2change2 = Math.cos(ang) * s2;

					sX2 = x2change1 + x2change2;
					sY2 = y2change1 + y2change2;

					sX1 = Math.cos(ang)*s1;
					sY2 = Math.sin(ang)*(-s1);

					oDiv1.style.left = oDiv1.offsetLeft + sX1 + 'px';
					oDiv1.style.top = oDiv1.offsetTop + sY1 + 'px';
				}

				oDiv2.style.left = oDiv2.offsetLeft + sX2 + 'px';
				oDiv2.style.top = oDiv2.offsetTop + sY2 + 'px';

			}, 30)
		}
	</script>
</head>
<body>
	<div id="div1"></div>
	<div id="div2"></div>
</body>
</html>
```

##三角函数图象

- 单位圆坐标系
- 弧度与sin之间的关系
- sin函数图象
- 例子：JS画sin图象
	- 可配合canvas做流体运动

```html
//JS画sin图象
<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8">
	<title>JS画sin图象</title>
	<style type="text/css">
		#div1 {width: 50px; height: 50px; background: red; position: absolute; left: 100px; top: 300px;}
		.box {border: 1px #000 solid; position: absolute;}
	</style>
	<script type="text/javascript">
		window.onload = function(){
			var oDiv = document.getElementById('div1');

			var num = 0;
			var val = 100;
			var L = 100;
			var T = 300;

			setInterval(function(){
				//弧度控制：left
				//sin控制：top
				num++;
				oDiv.style.left = L + (num*Math.PI/180)*val + 'px';
				oDiv.style.top = T - Math.sin(num*Math.PI/180)*val + 'px';

				var oBox = document.createElement('div');
				oBox.className = 'box';
				document.body.appendChild(oBox);
				oBox.style.left = oDiv.offsetLeft + 'px';
				oBox.style.top = oDiv.offsetTop + 'px';
			}, 30);
		}
	</script>
</head>
<body>
	<div id="div1"></div>
</body>
</html>
```
