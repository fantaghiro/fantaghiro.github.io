---
layout: post
title: 妙味课堂——canvas
category: study
tags:
- js
- 妙味课堂
- 前端基础
- 学习笔记
---

还记得一年前第一次接触canvas的时候，感觉编写步骤真的是十分繁琐。经历了半年比较密集的js学习之后，目前学习canvas基础知识部分的难度已经大大降低了，学习进度也加快了起来。canvas可以完成十分复杂的图形绘制和交互功能，从妙味课堂的远程视频中，学习得只能算是个基础吧。

- 目录
{:toc}

##标签

- &lt;canvas>不支持canvas的浏览器可以看到的内容&lt;/canvas>

##绘制环境

- getContext('2d') : 目前支持2d的场景

##绘制方块

- fillRect(L,T,W,H) : 默认颜色是黑色
- strokeRect(L,T,W,H) : 带边框的方块
	- 默认一像素黑色边框，显示出来的不一样原因（边框是从左边的中间开始往两边延伸的）

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>canvas</title>
	<style>
		body {background: #000;}
		#c1 {background: #fff;}
		span {color: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d'); //通过getContext('2d')才可以得到可以绘图的对象;webGL是支持3D绘图的
			// oGC.fillRect(50, 50, 100, 100);
			//oGC.strokeRect(50, 50, 100, 100); //边框默认为1像素，但仔细看，边框是2像素，因为边框绘制在50,50位置，向左延伸了0.5，向右延伸了0.5
			oGC.strokeRect(50.5, 50.5, 100, 100); //这时候边框就刚好是1像素了
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"> <!-- canvas的宽高最好在标签中设置，而不是在style中设置 -->
		<span>不支持canvas的浏览器可以看到这里的文字</span>
	</canvas> <!-- 默认：宽300 高150 -->
</body>
</html>
~~~

##设置绘图

- fillStyle : 填充颜色（绘制canvas是有顺序的）
- lineWidth : 线宽度，是一个数值
- strokeStyle : 边线颜色

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>canvas</title>
	<style>
		body {background: #000;}
		#c1 {background: #fff;}
		span {color: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d'); 

			oGC.fillStyle = 'red';
			oGC.strokeStyle = 'blue';
			oGC.lineWidth = 10;

			//注意，下面两句话的顺序不同，出现的效果可能是不一样的，先写fill后写stroke，那么边框是压在填充上面的；如果先写stroke，后写fill，那么填充是盖在边框上面的
			oGC.fillRect(50, 50, 100, 100);
			oGC.strokeRect(50.5, 50.5, 100, 100);
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"> 
		<span>不支持canvas的浏览器可以看到这里的文字</span>
	</canvas>
</body>
</html>
~~~

##边界绘制

- lineJoin : 边界连接点样式
	- miter（默认）、round（圆角）、bevel（斜角）
- lineCap : 端点样式
	- butt（默认）、round（圆角）、square（高度多出为宽一半的值）

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>canvas</title>
	<style>
		body {background: #000;}
		#c1 {background: #fff;}
		span {color: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d'); 

			oGC.fillStyle = 'red';
			oGC.strokeStyle = 'blue';
			oGC.lineWidth = 10;
			oGC.lineJoin = 'bevel';

			oGC.fillRect(50, 50, 100, 100);
			oGC.strokeRect(50.5, 50.5, 100, 100);
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"> 
		<span>不支持canvas的浏览器可以看到这里的文字</span>
	</canvas>
</body>
</html>
~~~

##绘制路径

- beginPath : 开始绘制路径
- closePath : 结束绘制路径
- moveTo : 移动到绘制的新目标点
- lineTo : 新的目标点
- stroke : 划线，默认黑色
- fill : 填充，默认黑色
- rect : 矩形区域
- clearRect : 删除一个画布的矩形区域
- save : 保存路径
- restore : 恢复路径
- 小例子 : 鼠标画线
- 小例子 : 方块移动

**moveTo, lineTo, stroke, fill**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>canvas</title>
	<style>
		body {background: #000;}
		#c1 {background: #fff;}
		span {color: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d'); 

			oGC.beginPath();
			oGC.moveTo(100, 100);
			oGC.lineTo(200, 200);
			oGC.stroke();
			oGC.lineTo(300, 200);
			oGC.closePath(); //闭合路径
			oGC.stroke();

			//注意针对不同的绘制，进行开始和闭合的操作

			oGC.beginPath(); //如果不添加beginPath，后面的OGC.fill()也会作用于上面的那个三角形，添加了beginPath()，OGC.fill()就仅作用于当前的绘制
			oGC.moveTo(100, 200);
			oGC.lineTo(200, 300);
			oGC.stroke();
			oGC.lineTo(300, 300);
			oGC.closePath();
			oGC.fill();
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"> 
		<span>不支持canvas的浏览器可以看到这里的文字</span>
	</canvas>
</body>
</html>
~~~

**rect**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>canvas</title>
	<style>
		body {background: #000;}
		#c1 {background: #fff;}
		span {color: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d'); 

			oGC.beginPath();

			oGC.rect(100, 100, 100, 100);

			oGC.closePath(); 
			oGC.stroke();
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"> 
		<span>不支持canvas的浏览器可以看到这里的文字</span>
	</canvas>
</body>
</html>
~~~

**clearRect**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>canvas</title>
	<style>
		body {background: #000;}
		#c1 {background: #fff;}
		span {color: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d'); 

			oGC.beginPath();

			oGC.rect(100, 100, 100, 100);

			oGC.closePath(); 
			oGC.fill();

			oGC.clearRect(0, 0, oC.width, oC.height);
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"> 
		<span>不支持canvas的浏览器可以看到这里的文字</span>
	</canvas>
</body>
</html>
~~~

**save()和restore()**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>canvas</title>
	<style>
		body {background: #000;}
		#c1 {background: #fff;}
		span {color: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d'); 

			oGC.save();
			oGC.fillStyle = 'red'; //这一句话封闭到了oGC.save()和oGC.restore()之中，不会影响到下面一个三角的fillStyle

			oGC.beginPath();
			oGC.moveTo(100, 100);
			oGC.lineTo(200, 200);
			oGC.lineTo(300, 200);
			oGC.closePath(); 
			oGC.fill();
			oGC.restore();

			oGC.beginPath();
			oGC.moveTo(100, 200);
			oGC.lineTo(200, 300);
			oGC.lineTo(300, 300);
			oGC.closePath();
			oGC.fill();
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"> 
		<span>不支持canvas的浏览器可以看到这里的文字</span>
	</canvas>
</body>
</html>
~~~

**断点样式**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>canvas</title>
	<style>
		body {background: #000;}
		#c1 {background: #fff;}
		span {color: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d'); 

			oGC.lineWidth = 20;
			oGC.lineCap = 'square';
			oGC.moveTo(100, 100);
			oGC.lineTo(200, 200);
			oGC.stroke();
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"> 
		<span>不支持canvas的浏览器可以看到这里的文字</span>
	</canvas>
</body>
</html>
~~~

**鼠标画线**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>鼠标画线</title>
	<style>
		body {background: #000;}
		#c1 {background: #fff;}
		span {color: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d'); 

			oC.onmousedown = function(ev){
				var ev = ev || window.event;
				oGC.moveTo(ev.clientX-oC.offsetLeft, ev.clientY-oC.offsetTop);
				document.onmousemove = function(ev){
					var ev = ev || window.event;
					oGC.lineTo(ev.clientX-oC.offsetLeft, ev.clientY-oC.offsetTop);
					oGC.stroke();
				}
				document.onmouseup = function(){
					document.onmousemove = null;
					document.onmouseup = null;
				}
			}
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"> 
		<span>不支持canvas的浏览器可以看到这里的文字</span>
	</canvas>
</body>
</html>
~~~

**方块移动**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>方块移动</title>
	<style>
		body {background: #000;}
		#c1 {background: #fff;}
		span {color: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d'); 
			var num = 0;

			oGC.fillRect(0, 0, 100, 100);
			setInterval(function(){
				num++;
				oGC.clearRect(0, 0, oC.width, oC.height);
				oGC.fillRect(num, num, 100, 100);
			}, 30)
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"> 
		<span>不支持canvas的浏览器可以看到这里的文字</span>
	</canvas>
</body>
</html>
~~~

**在style中设置canvas宽高的问题**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>在style中设置canvas宽高的问题</title>
	<style>
		body {background: #000;}
		#c1 {background: #fff; width: 400px; height: 400px;}
		span {color: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d'); 
			
			oGC.fillRect(0, 0, 100, 100); //把canvas的宽高写在style中，其实没有实际上更改canvas的宽高，而是将canvas进行等比例放大。因此这时候看起来这个方块就很大。	

			//在canvas标签上进行的width和height的设置是真正宽高的设置；在style中给canvas设置的宽高，其实会让canvas从默认300*150的基础上等比例缩放。
		}
	</script>
</head>
<body>
	<canvas id="c1"> 
		<span>不支持canvas的浏览器可以看到这里的文字</span>
	</canvas>
</body>
</html>
~~~

##绘制圆

- arc(x, y, 半径, 起始弧度, 结束弧度, 旋转方向)
	- x, y : 圆心坐标
	- 弧度与角度的关系 : 弧度 = 角度 * Math.PI/180
	- 旋转方向 : 顺时针（默认: false）、逆时针（true）
	- 例子 : 用arc去画个钟表

**绘制圆**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>画圆</title>
	<style>
		body {background: #000;}
		#c1 {background: #fff;}
		span {color: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d'); 
			
			oGC.moveTo(200, 200);

			//弧度 = 角度 * Math.PI/180
			oGC.arc(200, 200, 150, 0, 90*Math.PI/180, true);
			//oGC.closePath();
			oGC.stroke();
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
</body>
</html>
~~~

**用arc绘制钟表**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>画钟表</title>
	<style>
		body {background: #000;}
		#c1 {background: #fff;}
		span {color: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d'); 
			
			function toDraw(){
				var x = 200;
				var y = 200;
				var r = 150;

				oGC.clearRect(0, 0, oC.width, oC.height);

				var oDate = new Date();
				var oHours = oDate.getHours();
				var oMin = oDate.getMinutes();
				var oSec = oDate.getSeconds();
				var oHoursValue = (-90 + oHours*30 + oMin/2) * Math.PI/180;
				var oMinValue = (-90 + oMin*6) * Math.PI/180;
				var oSecValue = (-90 + oSec*6) * Math.PI/180;

				/*oGC.moveTo(x, y);
				oGC.arc(x, y, r, 0, 6*Math.PI/180, false);
				oGC.moveTo(x, y);
				oGC.arc(x, y, r, 6*Math.PI/180, 12*Math.PI/180, false);*/

				oGC.beginPath();
				for(var i=0; i<60; i++){
					oGC.moveTo(x, y);
					oGC.arc(x, y, r, 6*i*Math.PI/180, 6*(i+1)*Math.PI/180, false);
				}
				oGC.closePath();
				oGC.stroke();

				oGC.fillStyle = '#fff';
				oGC.beginPath();
				oGC.moveTo(x, y);
				oGC.arc(x, y, r*19/20, 0, 360*Math.PI/180);
				oGC.closePath();
				oGC.fill();

				oGC.lineWidth = 3;
				oGC.beginPath();
				for(var i=0; i<12; i++){
					oGC.moveTo(x, y);
					oGC.arc(x, y, r, 30*i*Math.PI/180, 30*(i+1)*Math.PI/180, false);
				}
				oGC.closePath();
				oGC.stroke();

				oGC.fillStyle = '#fff';
				oGC.beginPath();
				oGC.moveTo(x, y);
				oGC.arc(x, y, r*18/20, 0, 360*Math.PI/180);
				oGC.closePath();
				oGC.fill();

				//下面是画分针
				oGC.lineWidth = 5;
				oGC.beginPath();
				oGC.moveTo(x, y);
				oGC.arc(x, y, r*10/20, oHoursValue, oHoursValue, false); //起始点和终止点写同一个弧度，就是一条直线
				oGC.closePath();
				oGC.stroke();

				//下面是画时针
				oGC.lineWidth = 3;
				oGC.beginPath();
				oGC.moveTo(x, y);
				oGC.arc(x, y, r*14/20, oMinValue, oMinValue, false); //起始点和终止点写同一个弧度，就是一条直线
				oGC.closePath();
				oGC.stroke();

				//下面是画秒针
				oGC.lineWidth = 1;
				oGC.beginPath();
				oGC.moveTo(x, y);
				oGC.arc(x, y, r*18/20, oSecValue, oSecValue, false); //起始点和终止点写同一个弧度，就是一条直线
				oGC.closePath();
				oGC.stroke();
			}

			setInterval(toDraw, 1000);

			toDraw();
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
</body>
</html>
~~~

##绘制其他曲线

- arcTo(x1, y1, x2, y2, r)
	- 第一组坐标、第二组坐标、半径
- quadraticCurveTo(dx, dy, x1, y1)
	- 贝塞尔曲线：第一组控制点、第二组结束坐标
- bezierCurveTo(dx1, dy1, dx2, dy2, x1, y1)
	- 贝塞尔曲线：第一组控制点、第二组控制点、第三组结束坐标

**arcTo()**

~~~ html
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
	<style>
		body {background: #000;}
		#c1 {background: #fff;}
		span {color: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d'); 
			
			oGC.moveTo(100, 200);
			oGC.arcTo(100, 100, 200, 100, 50);
			oGC.stroke();
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
</body>
</html>
~~~

**quadraticCurveTo()**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
	<style>
		body {background: #000;}
		#c1 {background: #fff;}
		span {color: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d'); 
			
			oGC.moveTo(100, 200);
			oGC.quadraticCurveTo(100, 100, 200, 100);
			oGC.stroke();
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
</body>
</html>
~~~

**bezierCurveTo()**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
	<style>
		body {background: #000;}
		#c1 {background: #fff;}
		span {color: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d'); 
			
			oGC.moveTo(100, 200);
			oGC.bezierCurveTo(100, 100, 200, 200, 200, 100);
			oGC.stroke();
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
</body>
</html>
~~~

##变换

- translate
	- 偏移 : 从起始点为基准点，移动当前坐标位置
- rotate（以坐标顶点[左上角]为顶点旋转）
	- 旋转 : 参数为弧度 
	- 例子 : 旋转的小方块
- scale
	- 缩放例子 : 旋转加缩放的小方块

**变换的基本应用**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
	<style>
		body {background: #000;}
		#c1 {background: #fff;}
		span {color: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d'); 
			
			oGC.translate(100, 100);
			oGC.rotate(45*Math.PI/180);
			oGC.scale(2, 2);
			oGC.fillRect(0, 0, 100, 100);
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
</body>
</html>
~~~

**旋转的小方块**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
	<style>
		body {background: #000;}
		#c1 {background: #fff;}
		span {color: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d'); 
			var num = 0;
			
			setInterval(function(){
				num++;
				oGC.save(); //添加上save和restore，防止旋转角度的累加
				oGC.clearRect(0,0,oC.width,oC.height);
				oGC.translate(100, 100);
				oGC.rotate(num*Math.PI/180);
				oGC.translate(-50, -50); //让方块围绕中心旋转
				oGC.fillRect(0, 0, 100, 100);
				oGC.restore();
			}, 30)
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
</body>
</html>
~~~

**缩放小方块**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
	<style>
		body {background: #000;}
		#c1 {background: #fff;}
		span {color: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d'); 
			var num = 0;
			var num2 = 0;
			var value = 1;
			
			setInterval(function(){
				num++;
				oGC.save(); //添加上save和restore，防止旋转角度的累加
				oGC.clearRect(0,0,oC.width,oC.height);
				oGC.translate(100, 100);

				if(num2 == 75){
					value = -1;
				} else if(num2 == 25) {
					value = 1;
				}
				num2 += value;
				oGC.scale(num2*1/50, num2*1/50);
				oGC.rotate(num*Math.PI/180);
				oGC.translate(-50, -50); //让方块围绕中心旋转

				oGC.fillRect(0, 0, 100, 100);
				oGC.restore();
			}, 30)
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
</body>
</html>
~~~

##插入图片

- 等图片加载完，再执行canvas操作
	- 图片预加载 : 在onload中调用方法
- drawImage(oImg, x, y, w, h)
	- oImg : 当前图片x, y: 坐标； w, h: 宽高
	- 例子 : 微博的图片旋转效果



##设置背景

- createPattern(oImg, 平铺方式)
	- 第二个参数为: repeat, repeat-x, repeat-y, no-repeat


**drawImage()方法**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
	<style>
		body {background: #000;}
		#c1 {background: #fff;}
		span {color: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d'); 
			
			//图片预加载的方法
			var yImg = new Image();
			yImg.onload = function(){
				draw(this);
			}
			yImg.src = 'images/2.png';

			function draw(obj){
				oGC.drawImage(obj, 0, 0, 400, 400);
			}
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
</body>
</html>
~~~

**微博的图片旋转效果**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
	<style>
		body {background: #000;}
		#c1 {background: #fff;}
		span {color: #fff;}
	</style>
	<script>
		window.onload = function(){
			var aInput = document.getElementsByTagName('input');
			var oImg = document.getElementById('img1');
			var iNow = 0;

			var yImg = new Image();
			yImg.onload = function(){
				draw(oImg);
			}
			yImg.src = oImg.src;
			function draw(obj){
				var oC = document.createElement('canvas');
				var oGC = oC.getContext('2d');

				oC.width = obj.width;
				oC.height = obj.height;

				obj.parentNode.replaceChild(oC, obj)
				oGC.drawImage(obj, 0, 0);

				aInput[1].onclick = function(){
					//iNow记录点击了多少次
					if(iNow == 3){
						iNow = 0;
					} else {
						iNow++; 
					}
					toChange(); //旋转图片的方法
				}

				aInput[0].onclick = function(){
					if(iNow == 0){
						iNow = 3;
					} else {
						iNow--; 
					}
					toChange(); //旋转图片的方法
				}

				function toChange(){
					switch(iNow){
						case 1:
							oC.width = obj.height;
							oC.height = obj.width;
							oGC.rotate(90*Math.PI/180);
							oGC.drawImage(obj, 0, -obj.height);
						break;

						case 2:
							oC.width = obj.width;
							oC.height = obj.height;
							oGC.rotate(180*Math.PI/180);
							oGC.drawImage(obj, -obj.width, -obj.height);
						break;

						case 3:
							oC.width = obj.height;
							oC.height = obj.width;
							oGC.rotate(270*Math.PI/180);
							oGC.drawImage(obj, -obj.width, 0);
						break;

						case 0:
							oC.width = obj.width;
							oC.height = obj.height;
							oGC.rotate(0);
							oGC.drawImage(obj, 0, 0);
						break;
					}
				}
			}	
		}
	</script>
</head>
<body>
	<input type="button" value="←">
	<input type="button" value="→">
	<div>
		<img src="images/2.png" id="img1">
	</div>
</body>
</html>
~~~

**设置背景**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
	<style>
		body {background: #000;}
		#c1 {background: #fff;}
		span {color: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d');

			var yImg = new Image();
			yImg.onload = function(){
				draw(this);
			}
			yImg.src = 'images/2.png';
			function draw(obj){
				var bg = oGC.createPattern(obj, 'repeat');
				oGC.fillStyle = bg;
				oGC.fillRect(0, 0, 300, 300);
			}	
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
</body>
</html>
~~~

##渐变

- createLinearGradient(x1, y1, x2, y2)
	- 线性渐变
	- 第一组参数 : 起始点坐标；第二组参数 : 结束点坐标
	- addColorStop(位置, 颜色) 添加渐变点
- createRadialGradient(x1, y1, r1, x2, y2, r2)
	- 放射性渐变
	- 参数 : 第一个圆的坐标和半径，第二个圆的坐标和半径

**线性渐变**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
	<style>
		body {background: #000;}
		#c1 {background: #fff;}
		span {color: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d');

			var obj = oGC.createLinearGradient(150, 100, 250, 200); //从起点坐标到终点坐标进行一个渐变
			obj.addColorStop(0, 'red'); //起点用0表示
			obj.addColorStop(0.5, 'yellow');
			obj.addColorStop(1, 'blue'); //终点用1表示
			oGC.fillStyle = obj;
			oGC.fillRect(150, 100, 100, 100);
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
</body>
</html>
~~~

**径向渐变**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
	<style>
		body {background: #000;}
		#c1 {background: #fff;}
		span {color: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d');

			var obj = oGC.createRadialGradient(200, 200, 100, 200, 200, 150); //从起点坐标到终点坐标进行一个渐变
			obj.addColorStop(0, 'red'); //起点用0表示
			obj.addColorStop(0.5, 'yellow');
			obj.addColorStop(1, 'blue'); //终点用1表示
			oGC.fillStyle = obj;
			oGC.fillRect(0, 0, oC.width, oC.height);
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
</body>
</html>
~~~

##文本

- strokeText(文字, x, y)
	- 文字边框
- fillText(文字, x, y)
	- 文字填充
- font
	- 文字大小 : '60px impact' 两个参数必须要写
- textAlign
	- 默认是start跟left一样的效果 end right center
- textBaseline
	- 文字上下的位置的方式 默认: alphabetic
- measureText()
	- measureText(str).width : 只有宽度，没有高度
	- 例子 : 文字居中

**文本的操作**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
	<style>
		body {background: #000;}
		#c1 {background: #fff;}
		span {color: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d');

			oGC.font = '60px impact'; //两个参数必须要写
			oGC.textBaseline = 'top';
			oGC.fillText('妙味课堂', 0, 0);
			oGC.strokeText('妙味课堂', 0, 200);
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
</body>
</html>
~~~

**文字居中**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
	<style>
		body {background: #000;}
		#c1 {background: #fff;}
		span {color: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d');

			oGC.font = '60px impact'; 
			oGC.textBaseline = 'top'; //middle bottom

			var w = oGC.measureText('妙味课堂').width;
			oGC.fillText('妙味课堂', (oC.width - w) / 2, (oC.height - 60) / 2);
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
</body>
</html>
~~~

##阴影

- shadowOffsetX、shadowOffsetY
	- x轴偏移、y轴偏移
- shadowBlur
	- 高斯模糊值
- shadowColor
	- 阴影颜色 （默认颜色是rgba(0, 0, 0, 0) 黑色透明）

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
	<style>
		body {background: #000;}
		#c1 {background: #fff;}
		span {color: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d');

			oGC.font = '60px impact'; 
			oGC.textBaseline = 'top';
			oGC.shadowOffsetX = 10;
			oGC.shadowOffsetY = 10;
			oGC.shadowBlur = 3;
			oGC.shadowColor = 'yellow'; //一定要设置阴影颜色，阴影才能显示出来。阴影的默认颜色是rgba(0,0,0,0)即黑色透明
			var w = oGC.measureText('妙味课堂').width;
			oGC.fillText('妙味课堂', (oC.width - w) / 2, (oC.height - 60) / 2);
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
</body>
</html>
~~~

##像素

- getImageData(x, y, w, h)
	- 获取图像数据
- putImageData(获取图像, x, y)
	- 设置新的图像数据
- 属性
	- width : 一行的像素个数
	- height : 一列的像素个数
	- data : 一个数组，包含每个像素的rgba四个值，注意每个值都在0~255之间的整数
- createImageData(w, h)
	- 生成新的像素矩阵，初始值是全透明的黑色，即(0, 0, 0, 0)
	- 像素显字
- 获取和设置指定坐标
	- 封装 : getXY、setXY
- 图片的像素操作
	- 必须是同源下
	- 例子 : 反色、倒影、渐变等
	- 例子 : 马赛克效果

**getImageData和putImageData**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
	<style>
		body {background: #000;}
		#c1 {background: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d');

			oGC.fillRect(0, 0, 100, 100);

			var oImg = oGC.getImageData(0, 0, 100, 100); //获取方块的所有像素的值
			//alert(oImg.width); //一行的像素个数
			//alert(oImg.height); //一列的像素个数
			//alert(oImg.data); //整体像素的数组集合
			//alert(oImg.data.length); //40000 这个方块应该是10000个像素。也就是数组中每四个值代表一个像素。一个像素中的四个值代表r/g/b/a。
			//alert(oImg.data[0]); //0 0-255 黑色到白色
			//alert(oImg.data[1]); //0 0-255 黑色到白色
			//alert(oImg.data[2]); //0 0-255 黑色到白色
			//alert(oImg.data[3]); //255 0-255 透明到不透明
			//也就是说第一个像素的rgba是0, 0, 0, 255，也就是不透明的黑色
			
			for(var i=0; i<oImg.width*oImg.height; i++){
				oImg.data[4*i] = 255;
				oImg.data[4*i+1] = 0;
				oImg.data[4*i+2] = 0;
				oImg.data[4*i+3] = 100;
			} //通过循环更改了像素颜色
			oGC.putImageData(oImg, 100, 100); //把oImg这样的像素信息添到了位于100,100的位置
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
</body>
</html>
~~~

**createImageData**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
	<style>
		body {background: #000;}
		#c1 {background: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d');

			var oImg = oGC.createImageData(100, 100);
			
			for(var i=0; i<oImg.width*oImg.height; i++){
				oImg.data[4*i] = 255;
				oImg.data[4*i+1] = 0;
				oImg.data[4*i+2] = 0;
				oImg.data[4*i+3] = 100;
			} 
			oGC.putImageData(oImg, 100, 100); 
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
</body>
</html>
~~~

**像素显字；让文字中随机的10%的像素显示**

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
					var arr = randomArr(w*h, w*h/10);
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

**像素显字动画版**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>像素显字升级版</title>
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
					var timer = null;
					clearInterval(timer);
					var iNow = 0;

					oGC.clearRect(0, 0, oC.width, oC.height);
					oGC.font = h + 'px impact';
					oGC.fillStyle = 'red';
					oGC.textBaseline = 'top';
					var w = oGC.measureText(str).width;
					oGC.fillText(str, (oC.width - w) / 2, (oC.height - h) / 2);

					var oImg = oGC.getImageData((oC.width - w) / 2, (oC.height - h) / 2, w, h);
					oGC.clearRect(0, 0, oC.width, oC.height);
					var arr = randomArr(w*h, w*h/10);
					var newImg = oGC.createImageData(w, h);
					timer = setInterval(function(){

						for(var i = 0; i<arr[iNow].length; i++){
							newImg.data[arr[iNow][i]*4] = oImg.data[4*arr[iNow][i]];
							newImg.data[arr[iNow][i]*4+1] = oImg.data[4*arr[iNow][i]+1];
							newImg.data[arr[iNow][i]*4+2] = oImg.data[4*arr[iNow][i]+2];
							newImg.data[arr[iNow][i]*4+3] = oImg.data[4*arr[iNow][i]+3];
						}

						oGC.putImageData(newImg, (oC.width - w) / 2, (oC.height - h) / 2);

						if(iNow == 9){
							iNow = 0;
							clearInterval(timer);
						} else {
							iNow++;
						}
					}, 200)
						

						
				}
			}

			function randomArr(iAll, iNow){ //从iAll个数里面随机取出iNow个数
				var arr = [];
				var allArr = [];

				for(var i=0; i<iAll; i++){
					arr.push(i);
				}

				for(var j=0; j<iAll/iNow; j++){
					var newArr = []
					for(var i=0; i<iNow; i++){
						newArr.push(arr.splice(Math.floor(Math.random()*arr.length), 1));
					}
					allArr.push(newArr);
				}

					
				return allArr;
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

**获取和设置指定坐标 封装函数getXY和setXY**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>getXY、setXY</title>
	<style>
		body {background: #000; color: white; font-size: 30px;}
		#c1 {background: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d');

			oGC.fillRect(0, 0, 100, 100);

			var oImg = oGC.getImageData(0, 0, 100, 100);

			alert(getXY(oImg, 3, 5)); //得到坐标为3、5的rgba

			//setXY(oImg, 3, 5, [255, 0, 0, 255]); //设置坐标为3、5的rgba
			
			for(var i=0; i<oImg.width; i++){
				setXY(oImg, i, 5, [255, 0, 0, 255]);
			}

			oGC.putImageData(oImg, 100, 100);

			function getXY(obj, x, y){
				var w = obj.width;
				var h = obj.height;
				var d = obj.data;

				var color = [];

				color[0] = d[4*(y*w+x)];
				color[1] = d[4*(y*w+x)+1];
				color[2] = d[4*(y*w+x)+2];
				color[3] = d[4*(y*w+x)+3];

				return color;
			}

			function setXY(obj, x, y, color){
				var w = obj.width;
				var h = obj.height;
				var d = obj.data;

				d[4*(y*w+x)] = color[0];
				d[4*(y*w+x)+1] = color[1];
				d[4*(y*w+x)+2] = color[2];
				d[4*(y*w+x)+3] = color[3];

			}
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
</body>
</html>
~~~

**图片的像素操作——反色、倒影、渐变**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>图片的像素操作</title>
	<style>
		body {background: #000; color: white; font-size: 30px;}
		#c1 {background: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d');

			var yImg = new Image();
			yImg.onload = function(){
				draw(this);
			}
			yImg.src = 'img/2.png';

			function draw(obj){
				oC.width = obj.width;
				oGC.drawImage(obj, 0, 0);

				var oImg = oGC.getImageData(0, 0, obj.width, obj.height);
				var w = oImg.width;
				var h = oImg.height;
				var newImg = oGC.createImageData(obj.width, obj.height);

				//反色效果+倒影效果+渐变效果开始
				//反色，就是用255减去每个值
				for(var i=0; i<h; i++){ //循环每一列
					for(var j=0; j<w; j++){ //循环每一行
						var result = [];
						var color = getXY(oImg, j, i);
						result[0] = 255 - color[0];
						result[1] = 255 - color[1];
						result[2] = 255 - color[2];
						result[3] = 255*i/h;

						setXY(newImg, j, h-i, result);
					}
				}
				oGC.putImageData(newImg, 0, obj.height);
				//反色效果+倒影效果+渐变效果结束
			}

			function getXY(obj, x, y){
				var w = obj.width;
				var h = obj.height;
				var d = obj.data;

				var color = [];

				color[0] = d[4*(y*w+x)];
				color[1] = d[4*(y*w+x)+1];
				color[2] = d[4*(y*w+x)+2];
				color[3] = d[4*(y*w+x)+3];

				return color;
			}

			function setXY(obj, x, y, color){
				var w = obj.width;
				var h = obj.height;
				var d = obj.data;

				d[4*(y*w+x)] = color[0];
				d[4*(y*w+x)+1] = color[1];
				d[4*(y*w+x)+2] = color[2];
				d[4*(y*w+x)+3] = color[3];

			}
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
</body>
</html>
~~~

**马赛克效果**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>图片的像素操作</title>
	<style>
		body {background: #000; color: white; font-size: 30px;}
		#c1 {background: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d');

			var yImg = new Image();
			yImg.onload = function(){
				draw(this);
			}
			yImg.src = 'img/2.png';

			function draw(obj){
				oC.width = obj.width;
				oC.height = obj.height * 2;
				oGC.drawImage(obj, 0, 0);

				var oImg = oGC.getImageData(0, 0, obj.width, obj.height);
				var w = oImg.width;
				var h = oImg.height;
				var newImg = oGC.createImageData(obj.width, obj.height);

				var num = 10;
				var stepW = w/num;
				var stepH = h/num;

				//马赛克效果就是在num×num的像素里面随机取一个颜色，把这个num×num的区域都改成这个颜色

				for(var i=0; i<stepH; i++){
					for(var j=0; j<stepW; j++){
						var color = getXY(oImg, j*num+Math.floor(Math.random()*num), i*num+Math.floor(Math.random()*num));
						for(var k=0; k<num; k++){
							for(var l=0; l<num; l++){
								setXY(newImg, j*num+l, i*num+k, color);
							}
						}
					}
				}

				oGC.putImageData(newImg, 0, obj.height);
			}

			function getXY(obj, x, y){
				var w = obj.width;
				var h = obj.height;
				var d = obj.data;

				var color = [];

				color[0] = d[4*(y*w+x)];
				color[1] = d[4*(y*w+x)+1];
				color[2] = d[4*(y*w+x)+2];
				color[3] = d[4*(y*w+x)+3];

				return color;
			}

			function setXY(obj, x, y, color){
				var w = obj.width;
				var h = obj.height;
				var d = obj.data;

				d[4*(y*w+x)] = color[0];
				d[4*(y*w+x)+1] = color[1];
				d[4*(y*w+x)+2] = color[2];
				d[4*(y*w+x)+3] = color[3];

			}
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
</body>
</html>
~~~

##合成

- 全局阿尔法值
	- globalAlpha
- 覆盖合成
	- 源：新的图形
	- 目标：已经绘制过的图形
	- globalCompositeOperation属性
		- source-over destination-over source-atop
		- destination-atop source-in destination-in
		- source-out destination-out lighter
		- copy xor

**globalAlpha**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>合成</title>
	<style>
		body {background: #000; color: white; font-size: 30px;}
		#c1 {background: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d');

			oGC.fillRect(0, 0, 100, 100);
			oGC.fillStyle = 'red';
			oGC.globalAlpha = 0.5; //在此之后操作的图形的透明度都会是半透明的
			oGC.fillRect(50, 50, 100, 100);
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
</body>
</html>
~~~

**元素与元素叠加**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>合成</title>
	<style>
		body {background: #000; color: white; font-size: 30px;}
		#c1 {background: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d');

			oGC.fillRect(0, 0, 100, 100);
			oGC.fillStyle = 'red';

			//source就是新画的，destination就是先画的
			//oGC.globalCompositeOperation = 'destination-over';
			//oGC.globalCompositeOperation = 'source-atop';
			oGC.globalCompositeOperation = 'xor';

			oGC.fillRect(50, 50, 100, 100); //默认后画的会盖在先画的前面。改变覆盖顺序用globalCompositeOperation属性
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
</body>
</html>
~~~

##将画布导出为图像

- toDataURL
	- 火狐右键可以直接导出成图片

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>画布导出为图像</title>
	<style>
		body {background: blue; color: white; font-size: 30px;}
		#c1 {background: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oImg = document.getElementById('img1');
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d');

			oGC.fillRect(0, 0, 100, 100);
			oGC.fillStyle = 'red';
			oGC.globalCompositeOperation = 'xor';

			oGC.fillRect(50, 50, 100, 100);
			//alert(oC.toDataURL());
			oImg.src = oC.toDataURL();
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
	<img id="img1" src="">
</body>
</html>
~~~

##事件操作

- isPointInPath
	- 是否在点击范围内
	- jCanvaScript(canvas中的jquery)：
		- http://jcscript.com

**isPointInPath方法**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>事件操作</title>
	<style>
		body {background: #000; color: white; font-size: 30px;}
		#c1 {background: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d');

			oGC.beginPath();
			oGC.arc(100, 100, 50, 0, 360*Math.PI/180, false);
			oGC.closePath();
			oGC.fill();

			oGC.beginPath();
			oGC.arc(200, 200, 50, 0, 360*Math.PI/180, false);
			oGC.closePath();
			oGC.fill();

			//点击圆以内的部分，弹出123
			oC.onmousedown = function(ev){
				var ev = ev || window.event;
				var x = ev.clientX - oC.offsetLeft;
				var y = ev.clientY - oC.offsetTop;

				if(oGC.isPointInPath(x, y)){
					//isPointInPath方法只针对最后一次画出来的那个图形
					alert(123);
				}
			}
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
</body>
</html>
~~~

**点击不同的图形，执行不同的操作**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>事件操作</title>
	<style>
		body {background: #000; color: white; font-size: 30px;}
		#c1 {background: #fff;}
	</style>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d');

			var c1 = new Shape(100, 100, 50);
			var c2 = new Shape(200, 200, 50);

			oC.onmousedown = function(ev){
				var ev = ev || window.event;
				var point = {
					x : ev.clientX - oC.offsetLeft,
					y: ev.clientY - oC.offsetTop
				}
				c1.reDraw(point);
				c2.reDraw(point);
			}

			c1.click = function(){
				alert(123);
			}
			c2.click = function(){
				alert(456);
			}

			//要通过对象来实现。点击某个图形的时候，先找到这个图形对应的对象，然后再让这个图形重绘一下，然后就可以使用isPointInPath方法了，因为这个方法只能针对最后一个绘制的图形起作用。

			function Shape(x, y, r){
				this.x = x;
				this.y = y;
				this.r = r;

				oGC.beginPath();
				oGC.arc(this.x, this.y, this.r, 0, 360*Math.PI/180, false);
				oGC.closePath();
				oGC.fill();
			}
			Shape.prototype.reDraw = function(point){
				oGC.beginPath();
				oGC.arc(this.x, this.y, this.r, 0, 360*Math.PI/180, false);
				oGC.closePath();
				oGC.fill();

				if(oGC.isPointInPath(point.x, point.y)){
					this.click();
				}
			}
		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
</body>
</html>
~~~

**jCanvaScript的绘制和点击操作**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>jCanvaScript的使用</title>
	<style>
		body {background: #000; color: white; font-size: 30px;}
		#c1 {background: #fff;}
	</style>
	<script src="jCanvaScript.1.5.18.min.js"></script>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d');

			jc.start('c1', true); //开始 把canvas的id传进去 第二个参数代表“重绘”，也就是当有事件的时候，它会重新绘制
			//jc.rect(100, 100, 50, 50, '#ff0000' , true); //画一个方形
			//jc.circle(100, 100, 50, '#ff0000', 1); //画一个圆形
			jc.circle(100, 100, 50, '#ff0000', 1).click(function(){
				alert(123);
			});
			jc.start('c1'); //闭合

		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
</body>
</html>
~~~

**用jCanvaScript实现拖拽**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>jCanvaScript的使用</title>
	<style>
		body {background: #000; color: white; font-size: 30px;}
		#c1 {background: #fff;}
	</style>
	<script src="jCanvaScript.1.5.18.min.js"></script>
	<script>
		window.onload = function(){
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d');

			jc.start('c1', true); 
			jc.circle(100, 100, 50, '#ff0000', 1).draggable();
			jc.start('c1');

		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
</body>
</html>
~~~

**通过jCanvaScript让外部按钮控制画布**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>jCanvaScript的使用</title>
	<style>
		body {background: #000; color: white; font-size: 30px;}
		#c1 {background: #fff;}
	</style>
	<script src="jCanvaScript.1.5.18.min.js"></script>
	<script>
		window.onload = function(){
			var oInput = document.getElementById('input1');
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d');

			jc.start('c1', true); 
			jc.circle(100, 100, 50, '#ff0000', 1).id('circle1');
			jc.start('c1');

			oInput.onclick = function(){
				jc('#circle1').color('#ffff00');
			}

		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
	<input type="button" value="点击" id="input1">
</body>
</html>
~~~

**通过jCanvaScript实现运动效果**

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>jCanvaScript的使用</title>
	<style>
		body {background: #000; color: white; font-size: 30px;}
		#c1 {background: #fff;}
	</style>
	<script src="jCanvaScript.1.5.18.min.js"></script>
	<script>
		window.onload = function(){
			var oInput = document.getElementById('input1');
			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d');

			jc.start('c1', true); 
			jc.circle(100, 100, 50, '#ff0000', 1).id('circle1');
			jc.start('c1');

			oInput.onclick = function(){
				jc('#circle1').color('#ffff00').animate({x: 200, y: 200, radius: 5}, 2000);
			}

		}
	</script>
</head>
<body>
	<canvas id="c1" width="400" height="400"></canvas>
	<input type="button" value="点击" id="input1">
</body>
</html>
~~~

##简易祖玛小游戏

~~~ html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>简易祖玛小游戏</title>
	<style>
		* {margin: 0; padding: 0;}
		body {background: black;}
		#div1 {background: white; width: 600px; margin: 20px auto;}
	</style>
	<script>
		window.onload = function(){

			var oC = document.getElementById('c1');
			var oGC = oC.getContext('2d');
			var i = 0;
			
			var yImg = new Image();
			yImg.src = 'person.png';
			yImg.onload = function(){

				setInterval(function(){

					oGC.clearRect(0, 0, oC.width, oC.height);

					oGC.beginPath();
					oGC.arc(300, 200, 200, -90*Math.PI/180, 180*Math.PI/180, false);
					oGC.stroke();

					oGC.beginPath();
					oGC.arc(250, 200, 150, 180*Math.PI/180, 360*Math.PI/180);
					oGC.stroke();

					oGC.beginPath();
					oGC.arc(400, 200, 20, 0, 360*Math.PI/180);
					oGC.stroke();

					for(var i=0; i<ball.length; i++){
						oGC.beginPath();
						oGC.moveTo(ball[i].x, ball[i].y);
						oGC.arc(ball[i].x, ball[i].y, 20, 0, 360*Math.PI/180, false);
						oGC.fill();
					}

					oGC.save()
					oGC.translate(300, 200);
					oGC.rotate(iRotate);
					oGC.translate(-40, -40);
					oGC.drawImage(yImg, 0, 0);
					oGC.restore();

					for(var i=0; i<bullet.length; i++){

						oGC.save();
						oGC.fillStyle = 'red';
						oGC.beginPath();
						oGC.moveTo(bullet[i].x, bullet[i].y);
						oGC.arc(bullet[i].x, bullet[i].y, 20, 0, 360*Math.PI/180, false);
						oGC.fill();
						oGC.restore();
					}

					oGC.save();
					oGC.font = '60px impact';
					oGC.textBaseline = 'top';
					oGC.fillStyle = 'red';
					oGC.shadowOffsetX = 10;
					oGC.shadowOffsetY = 10;
					oGC.shadowColor = 'green';
					oGC.shadowBlur = 5;
					var w = oGC.measureText('简易祖玛').width;
					var h = 60;
					oGC.fillText('简易祖玛', (oC.width-w)/2, 450);
					oGC.restore();

				}, 1000/60);

				setInterval(function(){
					for(var i=0; i<ball.length; i++){
						ball[i].num++;
						if(ball[i].num == 270){
							ball[i].r = 150;
							ball[i].startX = 250;
							ball[i].startY = 50;
						}

						if(ball[i].num == 270 + 180){
							alert('游戏结束');
							window.location.reload(); //刷新一下页面
						}
						ball[i].x = Math.sin(ball[i].num*Math.PI/180) * ball[i].r + ball[i].startX;
						ball[i].y = ball[i].r - Math.cos(ball[i].num*Math.PI/180) * ball[i].r + ball[i].startY;
					}

					for(var i=0; i<bullet.length; i++){
						bullet[i].x = bullet[i].x + bullet[i].sX;
						bullet[i].y = bullet[i].y + bullet[i].sY;
					}

					for(var i=0; i<bullet.length; i++){
						for(var j=0; j<ball.length; j++){
							if(pz(bullet[i].x, bullet[i].y, ball[j].x, ball[j].y)){
								bullet.splice(i, 1);
								ball.splice(j, 1);
								break;
							}
						}
					}

				}, 30)

				var ball = [];
				ball[0] = {
					x : 300,
					y : 0,
					r : 200,
					num : 0, //角度
					startX : 300,
					startY : 0
				};

				setInterval(function(){
					ball.push({
						x : 300,
						y : 0,
						r : 200,
						num : 0, //角度
						startX : 300,
						startY : 0
					})
				}, 350);

				var iRotate = 0;
				oC.onmousemove = function(ev){

					var ev = ev || window.event;
					var x = ev.clientX - oC.offsetLeft;
					var y = ev.clientY - oC.offsetTop;

					var a = x - 300;
					var b = y - 200;

					var c = Math.sqrt(a*a + b*b);
					if(a>0 && b>0){
						iRotate = Math.asin(b/c) + 90*Math.PI/180;
					} else if(a>0){
						iRotate = Math.asin(a/c);
					}


					if(a<0 && b>0){
						iRotate = -(Math.asin(b/c) + 90*Math.PI/180);
					} else if(a<0){
						iRotate = Math.asin(a/c);
					}
				}

				var bullet = [];
				oC.onmousedown = function(ev){

					var ev = ev || window.event;
					var x = ev.clientX - oC.offsetLeft;
					var y = ev.clientY - oC.offsetTop;

					var a = x - 300;
					var b = y - 200;

					var c = Math.sqrt(a*a + b*b);
					var speed = 5;
					var sX = speed * a/c;
					var sY = speed * b/c;

					bullet.push({
						x : 300,
						y : 200,
						sX : sX,
						sY : sY
					});
				}
			}

			function pz(x1, y1, x2, y2){ //球的碰撞检测 检测两个圆心之间的距离是否小于两个圆半径之和
				var a = x1 - x2;
				var b = y1 - y2;
				var c = Math.sqrt(a*a + b*b);

				if(c<40){
					return true;
				} else {
					return false;
				}
			}

		}
	</script>
</head>
<body>
	<div id="div1">
		<canvas id="c1" width="600" height="600"></canvas>
	</div>
</body>
</html>
~~~

