---
layout: post
title: 妙味课堂——JavaScrip中级课程笔记
category: study
tags:
- js
- 妙味课堂
- 前端基础
- 学习笔记
---

每日坚持，渐入佳境。

- 目录
{:toc}

## DOM基础概念、操作

### DOM的概念及节点类型

DOM：Document Object Model 文档对象模型

- 文档：html页面
- 文档对象：html页面当中的元素
- 文档对象模型：一套定义、准则 为了能够让程序（js）去操作页面中的元素而定义出来的一套标准

DOM会把文档看作是一棵树，页面中的每个元素就是树上的一个一个节点；同时DOM定义了很多方法、属性等来操作这棵树中的每一个元素（节点）——每个节点称为DOM节点。

**DOM节点**

- childNodes \ children
    - 获取第一级子元素
    - 有兼容性问题（空白节点），nodeType属性
- firstChild \ firstElementChild
    - 获取子元素里的第一个
- lastChild \ lastElementChild
    - 获取子元素里的最后一个

####childNodes
    
元素.childNodes：只读属性 子节点列表集合

childNodes至包含一级子节点，不包含后辈孙级以下的节点

childNodes的兼容性问题：

- 标准浏览器下：childNodes包含了文本和元素类型的节点，并且也会包含非法嵌套的子节点；
- 非标准浏览器下，至包含元素类型的节点，IE7及以下不包含非法嵌套的子节点

~~~ html
<ul id="ul1">
    <li>1111</li>
    <li>1111</li>
    <li>1111</li>
    <li>1111</li>
</ul>
~~~

~~~ js
oUl = document.getElementById('ul1');
alert(oUl.childNodes.length); //在标准浏览器下弹出9；在IE6、7弹出4。因为标准浏览器下，文本元素（在这里是换行符）也包含在childNodes里面了。

for (var i=0; i<oUl.childNodes.length; i++){
    oUl.childNodes[i].style.background = 'red'; //在标准浏览器下会报错，因为文本元素（这里是换行符）没有是没有style属性的。
}

//可以通过下面这种方式来解决：

for (var i=0; i<oUl.childNodes.length; i++){
    if (oUl.childNodes[i].nodeType == 1) {
        oUl.childNodes[i].style.background = 'red';
    }
}
~~~

####children

元素.children：只读 属性 子节点列表集合

- 标准下： 只包含元素类型的节点，并且包含非法嵌套的子节点
- 非标准下：只包含元素类型的节点，IE7及以下不包含非法嵌套的子节点

这样，如果把childNodes换为children的话，就不用进行nodeType的判断了。

~~~ js
for (var i=0; i<oUl.children.length; i++){
    oUl.children[i].style.background = 'red';
    }
~~~

####nodeType

元素.nodeType：只读 属性 当前元素的节点类型

DOM节点的类型nodeType一种有12种，可以查看[这里](http://www.w3.org/TR/2000/REC-DOM-Level-2-Core-20001113/DOM2-Core.txt)。

常用的节点类型包括：元素节点、文本节点、属性节点：

- 元素节点 ELEMENT_NODE：1
- 属性节点 ATTRIBUTE_NODE ：2
- 文本节点 TEXT_NODE：3
    
~~~ html
<ul id="ul1" style="color: green">
    <li>1111</li>
    <li>1111</li>
    <li>1111</li>
    <li>1111</li>
</ul>
~~~

~~~ js
oUl = document.getElementById('ul1');
alert(oUl.nodeType); // 弹出1
alert(oUl.childNodes[0].nodeType); //弹出3
alert(oUl.attributes[0].nodeType); //弹出2
alert(oUl.attributes[0].name); //弹出'id'
alert(oUl.attributes.length); //弹出2
alert(oUl.attributes[0].value); //弹出'ul1'
~~~

####attributes

元素.attributes：只读 属性 属性列表集合

具体代码可以查看NodeType中js代码中alert的部分。

### 子节点和兄弟节点的操作

####firstChild

元素.firstChild：只读 属性 第一个子节点

- 标准下：firstChild会包含文本类型的节点
- 非标准下： 只包含元素节点

####firstElementChild

元素.firstElementChild：只读 属性

- 标准下获取第一个元素类型节点的子节点
- 非标准浏览器不支持

因此要进行判断：

~~~ js
if (oUl.firstElementChild){
    oUl.firstElementChild.style.background = 'red';
} else {
    oUl.firstChild.style.background = 'red';
}

//更为简洁的写法：

var oFirst = oUl.firstElementChild || oUl.firstChild;
oFirst.style.background = 'red';
~~~

可能存在的问题：

~~~ html
<ul id="ul1">
</ul>
~~~

~~~ js
var oUl = document.getElementById('ul1');
var oFirst = oUl.firstElementChild || oUl.firstChild; 
if(oFirst){
    oFirst.style.background = 'red';
} else {
    alert('没有子节点可以设置');
}
~~~

以上这段代码会报错。因为在oUl下面没有子元素节点，因此oUl.firstElementChild会返回为null，null不会传给变量oFirst，所以oFirst等于oUl.firstChild，而在标准浏览器下，oUl.firstChild是存在的，是一个文本节点，因此在下面的判断中，oFirst存在，因此走if语句的第一句，但是oFirst是文本节点，没有style可以设置，因此会报错。因此最好的做法是如下：

~~~ js
oUl.children[0].style.background = 'red';
~~~

####lastChild、lastElementChild

元素.lastChild || 元素.lastElementChild 最后一个子节点

原理与firstChild || firstElementChild相似，不再赘述

####nextSibling、previousSibling

元素.nextSibling || 元素.nextElementSibling 下一个兄弟节点

元素.previousSibling || 元素.previousElementSibling 上一个兄弟节点

###父节点

####parentNode

~~~ html
<ul id="ul1">
    <li>1111 <a href="javascript:;">隐藏</a></li>
    <li>2222 <a href="javascript:;">隐藏</a></li>
    <li>3333 <a href="javascript:;">隐藏</a></li>
    <li>4444 <a href="javascript:;">隐藏</a></li>
</ul>
~~~

~~~ js
var oA = document.getElementsByTag('a');
for (var i=0; i<oA.length; i++){
    oA[i].onclick = function(){
        this.parentNode.style.display = 'none';
    }
}
~~~

元素.parentNode： 只读 属性 只有一个 当前节点的父级节点

####offsetParent

~~~ html
<head>
    <style>
        div {padding: 40px 50px;}
        #div1 {background: red;}
        #div2 {background: green;}
        #div3 {background: orange;}
    </style>
</head>
<body id="body1">
    <div id="div1">
        <div id="div2">
            <div id="div3"></div>
        </div>
    </div>
</body>
~~~

~~~ js
var oDiv3 = document.getElementById('div3');
alert(oDiv3.parentNode.id); //弹出div2
alert(oDiv3.offsetParent.id); //弹出body1
~~~

上面的代码，如果给div1的style里面加上position: relative; 那么div3的offsetParent就变成了div1

元素.offsetParent：只读 属性 离当前元素最近的一个有定位的父节点

- 如果没有定位父级，默认是body
- IE7及以下， 如果当前元素没有定位，默认为body；如果当前元素有定位则是html
- IE7及以下，如果当前元素的某个父级触发了layout，那么offsetParent就会被指向到这个触发了layout特性的父节点

如果给div2的style中添加了zoom: 1，并且其他所有div都没有设置position样式，在IE下，alert(document.getElementById('div2').currentStyle.hasLayout); 会弹出true。这时候div3的offsetParent就会变成div2

###元素位置宽高

#### offsetLeft、offsetTop

元素.offsetLeft\offsetTop：只读 属性 当前元素到定位父级的距离（偏移值）

可以理解为到当前元素的offsetParent的距离

IE7及以下：

- 如果自己没有定位，那么offsetLeft\offsetTop是到body的距离；
- 如果当前元素有定位的情况下，那么offsetLeft\offsetTop是到它定位父级的距离
- 如果当前元素没有定位父级的情况下，那么offsetLeft\offsetTop是到html的距离（但是IE8以上，是到body的距离）

如果没有定位父级：

- IE7及以下： offsetLeft \ offsetTop => html
- 其他：offsetLeft \ offsetTop => body

如果有定位父级：

- IE7及以下：
    - 如果自己没有定位，那么offsetLeft \ offsetTop 是到body的距离
    - 如果自己有定位，那么就是到定位父级的距离
- 其他：到定位父级的距离

#### offsetWidth、offsetHeight

- 元素.style.width：样式宽：就是给元素的style中设置的width的值，带单位
- clientWidth：可视区宽：样式宽 + padding，不带单位
- offsetWidth：占位宽：样式宽 + padding + border = 可视区宽 + border


高度同理，不再赘述。

### getPos()

~~~ html
<head>
    <style>
        div {padding: 40px 50px;}
        #div1 {background: red; position: relative;}
        #div2 {background: green; position: relative;}
        #div3 {background: orange; position: relative;}
    </style>
</head>
<body id="body1">
    <div id="div1">
        <div id="div2">
            <div id="div3"></div>
        </div>
    </div>
</body>
~~~

~~~ js
//通过以下方法可以获得一个元素到达页面的绝对距离，通过各级元素与其offsetParent之间的距离累加的方式得到。

var iTop = 0;
var obj = oDiv3;

while(obj){
    iTop += obj.offsetTop;
    obj = obj.offsetParent;
}
~~~

body的offsetTop是0；body的offsetParent是null。

下面是获取一个元素到达页面的绝对距离的方式，getPos函数。注意，一般工作中，把body的margin值清掉，这样可以避免IE6、7与其他标准浏览器在getPos上的差异。

~~~ js
function getPos(obj){
    var pos = {left: 0, top: 0};
    while(obj){
        pos.left += obj.offsetLeft;
        pos.top += obj.offsetTop;
        obj = obj.offsetParent;
    }
    return pos;
}
~~~

###操作元素属性的多种方式

####点的形式和中括号形式

- 通过.点的形式：oText.value
- 通过中括号[]的形式：oText['value'] （当属性名用变量来表示的时候，用中括号）

####getAttribute、setAttribute、removeAttribute

- 元素.getAttribute(属性名称); 方法 获取指定元素的指定属性的值
- 元素.setAttribute(属性名称, 属性值); 方法 给指定元素指定的属性设置值
- 元素.removeAttribute(属性名称); 方法 移除指定的元素的指定的属性

set/get与用点.的区别：

1. 用.和[]的形式无法操作元素的自定义属性；getAttribute可以操作元素的自定义属性
2. 用.和[]的形式来获取src的时候，获取的是一长串绝对路径，但是在IE8以上以及标准浏览器中，用getAttribute('src')可以获取到相对路径（但是在IE7及以下，获取的src还是绝对路径）
3. 如果给oImg设置了style = "width: 100px;"的属性，那么通过oImg.style.getAttribute('width'); 在IE浏览器下是可以取到值的，但是在标准浏览器下是取不到值的。

###元素的创建操作

####document.createElement(); 

document.createElement(标签名);

- 动态创建元素
- 不会直接显示在页面当中
- 前面必须是document，不能是其他

####appendChild()

父级.appendChild(要追加的元素)

- 方法
- 在指定父级子节点最后一个后面追加子元素

####insertBefore()

父级.insertBefore(新的元素，指定的被插入的元素);

- 方法
- 在父级的指定子元素前面插入一个新元素
- 在IE下，如果第二个参数的节点不存在，会报错
- 在其它标准浏览器下，如果第二个参数的节点不存在，则会以appendChild的方式进行添加

为了兼容，应做以下判断：

~~~ html
<input type="text" id="text1" /><input type="button" value="留言" id="btn" />
<ul id="ul1"></ul>

~~~

~~~ js
var oText = document.getElementById('text1');
	var oBtn = document.getElementById('btn');
	var oUl = document.getElementById('ul1');
	
	oBtn.onclick = function() {
		
	    var oLi = document.createElement('li');
		oLi.innerHTML = oText.value;
		
		if ( oUl.children[0] ) {
			oUl.insertBefore( oLi, oUl.children[0] );
		} else {
			oUl.appendChild( oLi );
		}
		
		var oA = document.createElement('a');
		oA.innerHTML = '删除';
		oA.href = 'javascript:;';
		oLi.appendChild( oA );
		
		oA.onclick = function() {
		    oUl.removeChild( this.parentNode );
		}
	}

~~~

####removeChild()

父级.removeChild(要删除的节点); 

####replaceChild()

父级.replaceChild(新节点、被替换节点) 替换子节点

appendChild，insertBefore，replaceChild可以操作静态节点，也可以操作动态生成的节点。

##DOM、BOM相关方法及属性

###getElementsByClassName

~~~ js
function getElementsByClassName (parent, tagName, className){
    var aEls = parent.getElementsByTagName(tagName);
    var arr = [];
    
    for(var i=0; i<aEls.length; i++){
        /* 以下注释中的这种方法对于拥有多个class的元素不适用
        if(aEls[i].className == className){
            arr.push(aEls[i]);
        }
        */
        var aClassName = aEls[i].className.split(' ');
        
        for(var j=0; j<aClassName.length; j++){
            if(aClassName[j] == className){
                arr.push(aEls[i]);
                break; //当在某一个元素中找到了对应class马上就进行下一个循环，避免一个元素拥有多个重复class的时候，在数组中添加多次
            }
        }
    }
    
    return arr;
}
~~~

###addClass、removeClass

~~~ js
function addClass(obj, className){
    if(obj.className == ''){
        obj.className = className;
    } else {
        var arrClassName = obj.className.split(' ');
        var _index ＝ arrIndexOf(arrClassName, className);
        if(_index == -1){
           obj.className += ' ' + className; 
        }
    }
}

function removeClass(obj, className){
    if(obj.className != ''){
        var arrClassName = obj.className.split(' ');
        var _index ＝ arrIndexOf(arrClassName, className);
        if(_index != -1){
            arrClassName.splice(_index, 1);
            obj.className = arrClassName.join(' ');
        }
    }
}

function arrIndexOf(arr, v){
    for(var i=0; i<arr.length; i++){
        if(arr[i] == v){
            return i;
        }
    }
    return -1;
}


~~~


###表格操作

~~~ html
<table width="100%" id="tab1" border="1px">
    <tr>
        <td>1</td>
        <td>leo</td>
        <td>男</td>
        <td><a href="javascript:;">删除</a></td>
    </tr>
    <tr>
        <td>1</td>
        <td>小美</td>
        <td>女</td>
        <td><a href="javascript:;">删除</a></td>
    </tr>
</table>
~~~

~~~ js
    var oTab = document.getElementById('tab1');
    alert(oTab.children[1].children[1].innerHTML); //什么也弹不出来，提示显示oTab.children[1]未定义，这是因为如果在table中没有添加tbody的话，浏览器会自动隐形添加一个tbody出来。因此，写表格结构时，最好添加上tbody。
~~~

~~~ html
<table width="100%" id="tab1" border="1px">
    <thead>
        <tr>
            <th>编号</th>
            <th>姓名</th>
            <th>性别</th>
            <th>操作</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>1</td>
            <td>leo</td>
            <td>男</td>
            <td><a href="javascript:;">删除</a></td>
        </tr>
        <tr>
            <td>1</td>
            <td>小美</td>
            <td>女</td>
            <td><a href="javascript:;">删除</a></td>
        </tr>
    </tbody>
</table>
~~~

~~~ js
    var oTab = document.getElementById('tab1');
    // alert(oTab.children[0].children[1].children[1].innerHTML); //这是就可以弹出“小美”
    alert(oTab.tBodies[0].rows[1].cells[1].innerHTML); //弹出小美，更为直观
~~~

####表格属性####

- tHead：表格头（DOM中规定thead只能有一个）
- tBodies：表格正文（DOM中规定tbody可以有多个）
- tFoot：表格尾（DOM中规定tfoot只能有一个）
- rows：行
- cells：列

####表格数据的操作####

~~~ html
<table width="100%" id="tab1" border="1px">
    <thead>
        <tr>
            <th>编号</th>
            <th>姓名</th>
            <th>性别</th>
            <th>操作</th>
        </tr>
    </thead>
    <tbody></tbody>
</table>
~~~

~~~ js
var data = [
    {id: 1, username: 'leo', sex: '男'},
    {id: 2, username: '小美', sex: '女'},
    {id: 3, username: '王亮', sex: '男'},
    {id: 4, username: '杜鹏', sex: '男'},
];

var oTab = document.getElementById('tab1');
var oTbody = oTab.tBodies[0];

for(var i=0; i<data.length; i++){ //表格的创建
    var oTr = document.createElement('tr');
    
    if(i%2 == 0){ //各行变色
        oTr.style.background = 'white';
    } else {
        oTr.style.background = 'gray';
    }
    
    var oTd = document.createElement('td');
    oTd.innerHTML = data[i].id;
    oTr.appendChild(oTd);
    
    oTd = document.createElement('td');
    oTd.innerHTML = data[i].username;
    oTr.appendChild(oTd);
    
    oTd = document.createElement('td');
    oTd.innerHTML = data[i].sex;
    oTr.appendChild(oTd);
    
    oTd = document.createElement('td');
    // oTd.innerHTML = '&nbsp;'; //如果单元格中的内容为空，那么在IE7及以下，这个td不会被创建，为了好看，给最后一列td里面添加一个空格，这样在IE7下，最后一列td也会被创建
    oTr.appendChild(oTd);
    
    var oA = document.createElement('a');
    oA.innerHTML = '删除';
    oA.href = 'javascript:;';
    oA.onclick = function(){
        oTbody.removeChild(this.parentNode.parentNode);
        
        for(var i=0; i<oTbody.rows.length; i++){
            if(i%2 == 0) {
                oTbody.rows[i].style.background = 'white';
            } else {
                oTbody.rows[i].style.background = 'gray';
            }
        }
    }
    oTd.appendChild(oA);
    
    oTbody.appendChild(oTr);
}
~~~

###表单操作

~~~ html
<form id="form1">
    <input type="text" name="text1" />
    
    <input type="radio" name="sex" value="男" checked />男
    <input type="radio" name="sex" value="女" />女
    
    <input type="checkbox" name="a" value="html" checked />html
    <input type="checkbox" name="a" value="css" />css
    <input type="checkbox" name="a" value="javascript" />javascript
    
    <select name="city">
        <option value="">请选择城市</option>
        <option value="北京">北京</option>
        <option value="上海">上海</option>
    </select>
    
    <input type="button" value="按钮" name="btn" />
</form>
~~~

~~~ js
var oForm = document.getElementById('form1');
oForm.text1.onchange = function(){
    alert(this.value); //注意，文本输入框onchange的触发，是在输入完毕之后，鼠标离开该文本框之后触发
}

oForm.sex[0].onchange = function(){
    // alert(1); 
    // alert(this.value);
} //注意：oForm.sex其实是一个元素集合，因为name为sex的单选按钮有两个

oForm.a[0].onchange = function(){
    alert(2);
}

// alert(oForm.city.value);
oForm.city.onchange = function(){
    alert(this.value);
}

oForm.btn.onclick = function(){
    
    //radio, checkbox 判断当前的选项是否被选中
    //alert(oForm.sex[0].checked);
    
    for(var i=0; i<oFrom.sex.length; i++){
        if(oForm.sex[i].checked){
            alert(oForm.sex[i].value + '被选中了');
        } else {
            alert(oForm.sex[i].value + '未被选中');
        }
    }
    
    for(var i=0; i<oFrom.a.length; i++){
        if(oForm.a[i].checked){
            alert(oForm.a[i].value + '被选中了');
        } else {
            alert(oForm.a[i].value + '未被选中');
        }
    }
}
~~~

####name####

- name：表单中可以通过name来获取元素：父级.name （该方法浏览器都兼容）

####onchange事件####

- onchange事件：当值发生改变的时候触发
    - text：当光标离开的时候，如果内容有变化，就触发
    - radio/checkbox：
        - 标准下点击的时候，只要值发生改变，就会触发；
        - 非标准下，焦点离开的时候，如果值发生改变就触发
    - select：一选择不同的项，就触发


###表单事件

####onsubmit####

- onsubmit：事件 当提交表单的时候触发
- submit()：方法 提交表单


~~~ html
    <form id="form1" action="http://www.baidu.com">
        <input type="text" name="text1" />
        <input type="text" name="text2" value="111" />
        <input type="submit" name="dosubmit" value="提交" />
        <input type="reset" name="doreset" value="重置" />
    </form>
~~~

~~~ js
    oForm.onsubmit = function(){
        if(this.text1.value == ''){
            alert('请输入内容');
            return false; //如果没有在文本框中填写任何内容，就写return false，那么点击“提交”按钮，也不会提交到http://www.baidu.com上
        }
    }
    
    /* 让页面等待一秒钟后自动提交
    setTimeout(function(){
        oForm.submit();
    }, 1000) 
    */
~~~

####onreset####

注意“重置”的概念：不是清空，而是重置为默认值

- onreset：事件 当提交表单重置的时候触发

~~~ js
oForm.reset = function(){
    var re = confirm('你确定要重置吗？');
    /*
    if(re){
        return true;
    } else {
        return false;
    }
    */
    //上面的代码简写如下：
    return re;
    
    //以上所有代码可以简写为：return confirm('您确定要重置吗？');
}
~~~

###BOM

BOM：Browser Object Model 浏览器对象模型

BOM中大部分是对window对象的操作

####open####

- open(页面的地址url, 打开的方式)：方法 打开一个新的窗口（页面） 应该是window.open()，但是JS中默认前面是window的话，window可以不写。最常用的是两个参数：url和打开方式
    - 如果url为空，则默认打开一个空白页面
    - 如果打开方式为空，则默认为新窗口方式
    - open()方法的返回值：返回新打开的窗口的window对象

####close####

- close()：方法 关闭窗口 有兼容性问题
    - firefox：默认无法关闭
    - chrome：默认直接关闭
    - ie：询问用户
    - 可以关闭在本窗口中通过js方法打开的新窗口

~~~ html
<input type="button" value="打开新窗口" />
<input type="button" value="关闭窗口" />
<input type="button" value="关闭新窗口" />
~~~

~~~ js
var aInput = document.getElementsByTagName('input');
var opener = null;

aInput[0].onclick = function(){
    // window.open(); 打开新空白页面
    // window.open('http://www.baidu.com'); 在新窗口打开百度页面
    // window.open('http://www.baidu.com', '_self'); 在本窗口打开百度页面
    
    opener = window.open();
    opener.document.body.style.background = 'red';
}

aInput[1].onclick = function(){
    window.close(); //不同浏览器处理的方式不同，有兼容性问题
}

aInput[2].onclick = function(){
    opener.close(); 
}
~~~

####window.navigator.userAgent

window.navigator.userAgent => 浏览器信息

可以通过该属性判断浏览器

~~~ js
if(window.navigator.userAgent.indexOf('MSIE') != -1){ //如果浏览器信息中有MSIE这几个字就代表是IE
    alert('我是ie');
} else {
    alert('我不是ie');
}
~~~

####window.location

window:location：浏览器地址栏信息

window.location 看似是一串字符串，其实是一个对象。

- window.location.href：地址栏的地址url
- window.location.search：url?后面的内容
- window.location.hash：url#后面的内容

###文档宽高及窗口事件

####可视区尺寸

- document.documentElement.clientWidth //从文档对象的文档元素上取clientWidth
- document.documentElement.clientHeight

####滚动距离

- document.body.scrollTop/scrollLeft //scrollTop是可视区顶部到整个页面顶部的距离（就是滚动条滚动距离）；想要得到谁的滚动距离，scrollTop和scrollLeft的前面就写哪个元素
- document.documentElement.scrollTop/scrollLeft

**兼容性问题**

- chrome浏览器，认为滚动距离是在body上的
- 其他浏览器，认为滚动距离是documentElement上的

可以用如下方式解决兼容性问题：

~~~ js
var scrollTop = document.documentElement.scrollTop || document.body.scrollTop
~~~

####内容高度

- document.body.scrollHeight
- 元素.scrollHeight/scrollWidth

####文档高度

- document.documentElement.offsetHeight
- document.body.offsetHeight

**兼容性问题**

- 在IE下，文档的高document.documentElement.offsetHeight被认为是可视区的高
- 其他浏览器，文档的高并不是可视区的高

在页面中取文档的高，请先在CSS中将body的margin去掉，然后用document.body.offsetHeight来取文档元素的高，因为这时候文档的高与body的高没有差别。

####onscroll


onscroll：当滚动条滚动的时候触发

以一定的时间间隔来计算的。

~~~ js
var i=0;
window.onscroll = function(){
    document.title = i++;
}
~~~

####onresize

onresize：当窗口大小发生改变的时候触发

也是以一定时间间隔来计算的

~~~ js
var i=0;
window.onresize = function(){
    document.title = i++;
}
~~~

##Event事件详解

###焦点事件

焦点：使浏览器能够区分用户输入的对象。当一个元素有焦点的时候，那么它就可以接收用户的输入。

我们可以通过一些方式给元素设置焦点

1. 点击
2. tab
3. js

注意：不是所有元素都能够接收焦点。能够响应用户操作的元素才有焦点（例如输入框、链接a、表单元素）。

- 获取焦点事件onfocus \ 失去焦点事件 onblur (如：输入框提示文字)

- obj.focus(); 方法 给指定的元素设置焦点
- obj.blur(); 方法 取消指定元素的焦点
- obj.select(); 方法 选择指定的元素里面的文本内容

~~~ html
<input type="text" id="text1" value="请输入内容" />
<input type="button" value="全选" id="btn"/>
~~~

~~~ js
var oText = document.getElementById('text1');
var oBtn = document.getElementById('btn');

//onfocus：当元素获取到焦点的时候触发
oText.onfocus = function(){
    if(value='请输入内容'){
        this.value = '';
    }
}

//onblur：当元素失去焦点的时候触发
oText.onblur = function(){
    if(this.value == ''){
        this.value = '请输入内容';
    }
}

oText.focus();

oBtn.onclick = function(){
    oText.select();
}
~~~

###Event对象

- 用来获取事件的详细信息：鼠标位置、键盘按键
- Event对象的兼容：ev = ev || window.event
- Event对象下的获取鼠标位置：clientX clientY （例如：方块跟随鼠标移动）

event：事件对象。当一个事件发生的时候，和当前这个对象发生的这个事件有关的一些详细的信息都会被临时保存到一个指定的地方，这个地方就是event对象，供我们在需要的时候调用。（比喻：飞机-黑匣子）

- Event对象必须在一个事件调用的函数里面使用才有内容。
- 事件函数：事件调用的函数。一个函数是不是事件函数，不是在定义的时候决定，而是取决于这个函数被调用的时候

~~~ js
function fn1(){
    alert(event);
}

fn1(); //不是事件调用的函数，因此这时候event没有内容，显示undefined
document.onclick = fn1; //fn1是事件调用的函数，所以event有内容 这种写法在ff下是弹不出东西的
~~~

####event对象的兼容性问题

- ie/chrome：event是一个内置的全局对象
- 标准下（包括ff）：事件对象是通过事件函数的第一个参数传入（如果一个函数是被事件调用的，那么，这个函数定义的第一个参数就是事件对象）

~~~ js
function fn1(ev){
    alert(ev);
}
document.onclick = fn1; //在火狐、标准ie下、chrome下都可以弹出事件对象（非标准ie会弹出undefined）
~~~

解决兼容性问题的方法：var ev = ev || event;

~~~ js
function fn1(ev) {
    var ev = ev || event;
    alert(ev);
    
    for(var attr in ev){
        console.log(attr + ' = ' + ev[attr]);
    }
}
document.onclick = fn1; //在标准浏览器和非标准浏览器下，都能够正确弹出事件对象
~~~

####clientX \ clientY

- clientX \ clientY：当一个事件发生的时候，鼠标到页面可视区的距离

~~~ js
function fn1(ev) {
    var ev = ev || event;
    alert(ev.clientX);
}
document.onclick = fn1; //弹出当前鼠标到可视区左边的距离
~~~

示例-跟随鼠标移动的div：

~~~ html
<div id="div1" style="width: 100px; height: 100px; background: red; position: absolute;"></div>
~~~

~~~ js
    //onmousemove；当鼠标在一个元素上移动的时候触发
    //触发频率不是以像素记，而是间隔时间。在一个指定时间内（很短），如果鼠标的位置和上一次的位置发生了变化，那么就会触发一次
    var oDiv = document.getElementById('div1');
    document.onmousemove = function(){
        var ev = ev || event;
        var scrollTop = document.documentElement.scrollTop || document.body.scrollTop;
        oDiv.style.left = ev.clientX + 'px';
        oDiv.style.top = scrollTop + ev.clientY + 'px';
    }
~~~

###事件流

- 事件冒泡
    - 取消冒泡：ev.cancelBubble = true
    - 例子：仿select控件
- 事件捕获
    - 非标准IE下是没有的，在绑定事件中，标准下是有的

####事件冒泡

事件冒泡：当一个元素接收到事件的时候，会把它接收到的事件传播给它的父级，一直到顶层window，这也被称为js中的事件冒泡机制。

以前是说给某某加一个点击事件，其实这并不准确。应该说是给元素添加事件（处理）函数。例如：oDiv1.onclick = fn1; 这句代码其实是告诉oDiv1，如果它接收到了一个点击事件，那么他就去执行fn1事件函数。这也称之为：事件函数绑定：就是将事件与一个函数绑定。比如将oDiv1.onclick = fn1;这句代码在文件中注释掉，那么点击oDiv1的时候，oDiv1还是能够接收到点击事件，只不过这时候这个点击事件没有与事件函数绑定，因此没有执行什么东西。

//我在马路边捡到一分钱，把他交给警察叔叔（老师就相当于程序员，让我在捡到一分钱的时候，交给警察）（但是如果老师没有告诉你要交给警察叔叔，也不会影响你捡到一分钱。）

我.on马路边捡到一分钱 = function(){
    把他交给警察叔叔;
}

**阻止冒泡**

在当前要阻止冒泡的事件函数中调用：事件对象.cancelBubble = true;

~~~ html
<input type="button" value="按钮" id="btn" />
<div id="div1" style="width: 100px; height: 200px; border: 1px solid red; display: none"></div>
~~~

~~~ js
var oBtn = document.getElementById('btn');
var oDiv = document.getElementById('div1');

oBtn.onclick = function(ev){
    var ev = ev || event;
    ev.cancelBubble = true; //阻止当前对象的当前事件的冒泡
    oDiv.style.display = 'block';
}
document.onclick = function(){
    /*
    setTimeout(function(){
        oDiv.style.display = 'none';
    }, 1000);
    */
    oDiv.style.display = 'none';
}
~~~

**案例：分享到**

~~~ html
<div id="div1">
    <div id="div2"></div>
</div>
~~~

~~~ css
#div1 {width: 100px; height: 200px; background: red; position: absoute; left: -100px; top: 100px;}
#div2 {width: 30px; height: 60px; position: absolute; right: -30px; top: 70px; background: black; color: white; text-align: center;}
~~~

~~~ js
var oDiv = document.getElementByid('div1');
oDiv.onmouseover = function(){
    this.style.left = '0px';
}
oDiv.onmouseout = function(){
    this.style.left = '-100px';
}
~~~

注意：上面的案例中，事件都是加给div1的，并没有加给div2。但是，当鼠标从div1移入或移出时，都可以触发设置在div2上的事件函数，因此大大地减少了代码量。

####绑定事件的第二种形式

**给一个对象绑定一个事件处理函数的第一种形式**

对象.事件＝事件处理函数（如obj.onclick = fn;)

第一种事件绑定的形式是赋值形式，后赋的值会把先赋的值覆盖掉：
如：

~~~ js
function fn1(){alert(1);}
function fn2(){alert(2);}
document.onclick = fn1;
document.onclick = fn2; //会覆盖前面绑定的fn1
~~~

为了给一个对象的同一个事件绑定多个不同的事件函数，所以就产生了给一个元素绑定事件函数的第二种形式.第二种形式是采用函数的形式而不是赋值的形式。

**给对象绑定事件处理函数的第二种形式**

兼容问题：

- ie：obj.attachEvent(事件名称, 事件函数);
    - document.onclick = fn1; => document.attachEvent('onclick', fn1);
    - 没有捕获
    - 事件名称有on
    - 事件函数执行的顺序：标准ie -> 正序；非标准ie -> 倒序
    - this指向window
        - 解决方法：利用call方法。如：document.attachEvent('onclick', function(){fn1.call(document)});
- 标准：obj.addEventListener(事件名称, 事件函数, 是否捕获); 注意，这里的事件名称不带on。
    - document.addEventListener('click', fn1, false);
    - 有捕获
    - 事件名称没有on
    - 事件函数执行顺序：正序
    - this指向触发该事件的对象

是否捕获：默认是false。false：冒泡；true：捕获

**call方法**

call：函数下的一个方法，call方法的第一个参数可以改变函数执行过程中的内部this的指向；call方法从第二个参数开始就是原来函数的参数列表；如果call方法传入的第一个参数是null，那么就是不改变函数内部的this指向的。

~~~ js
function fn1(){
    alert(this);
}

//fn1(); //window
fn1.call(); //调用函数 也就是说：fn1() 可视为等同于 fn1.call() 弹出window
fn1.call(1) //弹出1，因为在fn1里面的this变成了1。
~~~

~~~ js
function fn1(a + b){
    alert(this);
    alert(a + b);
}
fn1.call(1, 20, 30); //先弹出1，然后弹出50
fn1.call(null, 10, 20); //先弹出window对象，然后弹出30
~~~

**函数绑定封装函数：**

~~~ js
function bind(obj, evname, fn){
    if(obj.addEventListener){
        obj.addEventListener(evname, fn, false);
    } else {
        obj.attachEvent('on' + evname, function(){
            fn.call(obj);
        })
    }
}
~~~

~~~ html
<div id="div1">
	<div id="div2">
		<div id="div3"></div>
	</div>
</div>
~~~

~~~ js
var oDiv1 = document.getElementById('div1');
var oDiv2 = document.getElementById('div2');
var oDiv3 = document.getElementById('div3');

function fn1(){
	alert(this);
}

//通过将addEventListener的第三个参数设置为true，来设置事件捕获
oDiv1.addEventListener('click', fn1, true); //上面这一句告诉oDiv1：如果有一个进去的事件触发了你，你就去执行fn1这个函数
oDiv2.addEventListener('click', fn1, true);
oDiv3.addEventListener('click', fn1, true);
~~~

以上代码，点击oDiv3，弹出顺序是div1 -> div2 ->div3；执行顺序是倒序的。

当点击oDiv3的时候，首先，事件像是一个力一样透过oDiv1、oDiv2到达oDiv3，到达目标对象oDiv3之后，又会像一个反作用力那样，从oDiv3传到oDiv2、oDiv1。也就是说有这个一进一出的过程。如果将addEventListener的第三个参数设置为true，那么进去的那个事件就触发事件函数；相反，如果addEventListener的第三个参数设置为false，那么就是传回来的“反作用力”——传回来的这个事件触发事件函数。

addEventListener的第三个参数true或false监听的就是究竟事件在进去的时候触发，还是返回来冒泡的时候触发。

~~~ js
oDiv1.addEventListener('click', function(){
	alert(1);
}, false)
oDiv1.addEventListener('click', function(){
	alert(3);
}, true)
oDiv1.addEventListener('click', function(){
	alert(2);
}, false)
//弹出顺序是：3 -> 2 -> 1
~~~

###事件绑定函数的取消

**取消普通形式的事件绑定函数：**

~~~ js
function fn1(){alert(1);}
function fn2(){alert(2);}

document.onclick = fn1;
document.onclick = null; //通过赋值的形式取消了原来的事件绑定函数fn1
~~~

**取消第二种形式的事件绑定函数：**

- IE：obj.detachEvent(事件名称, 事件函数);
- 标准：obj.removeEventListener(事件名称, 事件函数, 是否捕获 );

###键盘事件

####onkeydown

**onkeydown：**当键盘按键按下的时候触发

**事件对象.keyCode：**数字类型 键盘按键的值 键值 （同样功能的按键，键值一样。例如左侧的ctrl和右侧的ctrl的键值相同）

- ctrlKey, shiftKey, altKey 事件对象的三个属性 布尔值
- 当一个事件（不一定是键盘事件）发生的时候，如果ctrl || shift || alt 是按下的状态，返回true，否则返回false。

- onkeydown：如果按下不抬起，那么会连续触发

~~~ js
document.onkeydown = function(ev){
	var ev = ev || event;
	alert(ev.keyCode);
}
~~~

~~~ js
document.onclick = function(ev){
	var ev = ev || event;
	alert(ev.ctrlKey); //当按下ctrl点击的时候，弹出true；没有按ctrl点击的时候，返回false
}
~~~

####onkeyup

**onkeyup：**当键盘按键抬起的时候触发


**仿QQ留言本**

~~~ html
<input type="text" id="text1" />
<ul id="ul1"></ul>
~~~

~~~ js
var oText = document.getElementById('text1');
var oUl = document.getElementById('ul1');

/*
oText.onkeydown = function(){
	alert(this.value); //这里会发现，onkeydown的事件触发是在给oText赋值之前，所以这里应该改为onkeyup才行
}
*/

oText.onkeyup = function(ev){
	
	var ev = ev || event;

	if(this.value != ''){

		if(ev.keyCode == 13 && ev.ctrlKey){ //如果同时按住ctrl + 回车 

			var oLi = document.createElement('li');
			oLi.innerHTML = this.value;

			if(oUl.children[0]){
				oUl.insertBefore(oLi, oUl.children[0]);
			} else {
				oUl.appendChild(oLi);
			}

		}
			
	}
}
~~~

**键盘控制div移动**

~~~ html
<div id="div1"></div>
~~~

~~~ css
#div1 {width: 100px; height: 100px; background: red; position: absolute;}
~~~

~~~ js
var oDiv = document.getElementById('div1');

document.onkeydown = function(ev){
	var ev = ev || event;

	switch(ev.keyCode){
		case 37:
			oDiv.style.left = oDiv.offsetLeft - 10 + 'px;'
			break;
		case 38:
			oDiv.style.top = oDiv.offsetTop - 10 + 'px;'
			break;
		case 39:
			oDiv.style.left = oDiv.offsetLeft + 10 + 'px;'
			break;
		case 40:
			oDiv.style.top = oDiv.offsetTop + 10 + 'px;'
			break;
	}
}
~~~

- 不是所有元素都能够接收键盘事件，能够响应用户输入的元素才可以。能够接收焦点的元素就能够接收键盘事件。

####事件默认行为

**事件默认行为：**当一个事件发生的时候，浏览器自己会默认做的事情

阻止事件默认行为的步骤：

1. 当前这个行为是什么事件触发的
2. 在这个事件的处理函数中使用return false;

~~~ html
<body style="height: 2000px"></body>
~~~

默认情况下，点击空格，滚动条会向下滚动

~~~ js
document.onkeydown = function(){
	return false; //这样就阻止了点击空格，滚动条向下滚动的默认事件
}
document.oncontextmenu = function(){
	//alert(1);
	return false; //阻止了点击右键，弹出右键菜单的默认行为
}
~~~

**oncontextmenu：**右键菜单事件，当右键菜单（环境菜单、上下文菜单）显示出来的时候触发

**自定义右键菜单**

~~~ html
<div id="div1"></div>
~~~

~~~ css
#div1 {width: 100px; height: 200px; border: 1px solid red; position: absolute; display: none;}
~~~

~~~ js
var oDiv = document.ElementById('div1');

document.oncontextmenu = function(ev){
	var ev = ev || event;
	var scrollTop = document.documentElement.scrollTop || document.body.scrollTop;
	var scrollLeft = document.documentElement.scrollLeft || document.body.scrollLeft;
	
	oDiv.style.display = 'block';
	
	oDiv.style.left = scrollLeft + ev.clientX + 'px';
	oDiv.style.top = scrollTop + ev.clientY + 'px';

	return false;
}

document.onclick = function(){
    oDiv.style.display = 'none';
}
~~~

##事件深入应用

###拖拽的原理

**简单拖拽：**

- 鼠标和div的相对距离不变
- 三大事件：onmousedown（选择元素） -> onmousemove（移动元素） -> onmouseup（释放元素）
- 把拖拽加到document上

~~~ html
<div id="div1"></div>
~~~

~~~ css
#div1 { width: 100px; height: 100px; background: red; position: absolute; }
~~~

~~~ js
var oDiv = document.getElementById('div1');

oDiv.onmousedown = function(ev){
    var ev = ev || event;
    var disX = ev.clientX - this.offsetLeft;
    var disY = ev.clientY - this.offsetTop;
    
    document.onmousemove = function(ev){
        var ev = ev || event;
        
        oDiv.style.left = ev.clientX - disX + 'px';
        oDiv.style.top = ev.clientY - disY + 'px';
        
    }
    
    document.onmouseup = function(){
        document.onmousemove = document.onmouseup = null;
    }
}
~~~

###拖拽的问题以及解决办法

1. 拖拽的时候，如果有文字被选中，会产生问题。
    - 原因：当鼠标按下的时候，如果页面中有文字被选中，会触发浏览器的默认拖拽文字的效果。
    - 解决方法：
        - 标准下：在onmousedown事件的函数里面添加return false;
        - 非标准IE下：通过在ie下设置全局捕获，用setCapture()方法曲线救国
2. 拖拽图片会有问题，原因和解决方法同上


~~~ html
<input type="button" value="按钮一" />
<input type="button" value="按钮二" />
~~~

~~~ js
var aInput = document.getElementsByTagName('input');

aInput[0].setCapture(); //设置全局捕获
aInput[0].onclick = function(){
    alert(1);
}
aInput[0].onclick = function(){
    alert(2);
}
~~~

**全局捕获：**

- 方法：元素.setCapture();
- 当我们给一个元素设置全局捕获以后，这个元素就会监听后续发生的所有事件，当有事件发生的时候，就会被当前设置了全局捕获的元素所触发
- 兼容性问题：
    - IE：有，并且有效果
    - ff：有，但是没效果
    - chrome：没有这个方法
- 与之对应的释放全局捕获的方法是：元素.releaseCapture();

~~~ js
var oDiv = document.getElementById('div1');

oDiv.onmousedown = function(ev){
    var ev = ev || event;
    var disX = ev.clientX - this.offsetLeft;
    var disY = ev.clientY - this.offsetTop;
    
    if(oDiv.setCapture){ //如果浏览器有setCapture这个方法的话
        oDiv.setCapture();//让oDiv将所有后续事件都捕获到自己身上来
    }
    
    document.onmousemove = function(ev){
        var ev = ev || event;
        
        oDiv.style.left = ev.clientX - disX + 'px';
        oDiv.style.top = ev.clientY - disY + 'px';
        
    }
    
    document.onmouseup = function(){
        document.onmousemove = document.onmouseup = null;
        
        //释放全局捕获
        if(oDiv.releaseCapture){
            oDiv.releaseCapture();
        }
    }
    
    return false; //阻止浏览器的默认行为
}
~~~

###拖拽的封装和应用扩展-限制范围、磁性吸附

~~~ js
function drag(obj){
    obj.onmousedown = function(ev){
        var ev = ev || event;
        var disX = ev.clientX - this.offsetLeft;
        var disY = ev.clientY - this.offsetTop;
        
        if(obj.setCapture){
            obj.setCapture();
        }
        
        document.onmousemove = function(ev){
            var ev = ev || event;
            
            obj.style.left = ev.clientX - disX + 'px';
            obj.style.top = ev.clientY - disY + 'px';
            
        }
        
        document.onmouseup = function(){
            document.onmousemove = document.onmouseup = null;
            
            if(obj.releaseCapture){
                obj.releaseCapture();
            }
        }
        
        return false;
    }   
}
~~~

**限制范围的拖拽：**

~~~ js
function drag(obj){
    obj.onmousedown = function(ev){
        var ev = ev || event;
        var disX = ev.clientX - this.offsetLeft;
        var disY = ev.clientY - this.offsetTop;
        
        if(obj.setCapture){
            obj.setCapture();
        }
        
        document.onmousemove = function(ev){
            var ev = ev || event;
            var L = ev.clientX - disX;
            var T = ev.clientY - disY;
            
            // 限制拖拽范围在页面内
            if(L < 0){
                L = 0;
            } else if( L > document.documentElement.clientWidth - obj.offsetWidth){
                L = document.documentElement.clientWidth - obj.offsetWidth;
            }
            if(T < 0){
                T = 0;
            } else if(T > document.documentElement.clientHeight - obj.offsetHeight){
                T = document.documentElement.clientHeight - obj.offsetHeight;
            }
            
            obj.style.left = L + 'px';
            obj.style.top = T  + 'px';
            
        }
        
        document.onmouseup = function(){
            document.onmousemove = document.onmouseup = null;
            
            if(obj.releaseCapture){
                obj.releaseCapture();
            }
        }
        
        return false;
    }   
}
~~~

**磁性吸附：**

~~~ js
function drag(obj){
    obj.onmousedown = function(ev){
        var ev = ev || event;
        var disX = ev.clientX - this.offsetLeft;
        var disY = ev.clientY - this.offsetTop;
        
        if(obj.setCapture){
            obj.setCapture();
        }
        
        document.onmousemove = function(ev){
            var ev = ev || event;
            var L = ev.clientX - disX;
            var T = ev.clientY - disY;
            
            // 限制拖拽范围在页面内
            if(L < 100){ //只要把原来的0改为一个范围，例如：100，就实现了磁性吸附的效果
                L = 0;
            } else if( L > document.documentElement.clientWidth - obj.offsetWidth){
                L = document.documentElement.clientWidth - obj.offsetWidth;
            }
            if(T < 100){
                T = 0;
            } else if(T > document.documentElement.clientHeight - obj.offsetHeight){
                T = document.documentElement.clientHeight - obj.offsetHeight;
            }
            
            obj.style.left = L + 'px';
            obj.style.top = T  + 'px';
            
        }
        
        document.onmouseup = function(){
            document.onmousemove = document.onmouseup = null;
            
            if(obj.releaseCapture){
                obj.releaseCapture();
            }
        }
        
        return false;
    }   
}
~~~

###碰撞检测

~~~ html
<div id="div1"></div>
<img id="img1" url="1.jpg" />
~~~

~~~ css
#div1 { width: 100px; height: 100px; background: red; position: absolute; z-index: 2 }
#img1 { position: absolute; left: 500px; top: 200px; }
~~~

~~~ js
function drag(obj){
    obj.onmousedown = function(ev){
        var ev = ev || event;
        var disX = ev.clientX - this.offsetLeft;
        var disY = ev.clientY - this.offsetTop;
        
        if(obj.setCapture){
            obj.setCapture();
        }
        
        document.onmousemove = function(ev){
            var ev = ev || event;
            var L = ev.clientX - disX;
            var T = ev.clientY - disY;
            
            //被拖动的元素的四条边
            var L1 = L;
            var R1 = L + obj.offsetWidth;
            var T1 = T;
            var B1 = T + obj.offsetHeight;
            
            //被碰撞的元素的四条边(这个例子里面是img元素)
            var L2 = oImg.offsetLeft;
            var R2 = L2 + oImg.offsetWidth;
            var T2 = oImg.offsetTop;
            var B2 = T2 + oImg.offsetHeight;
            
            if(R1 < L2 || L1 > R2 || B1 < T2 || T1 > B2){
                oImg.src = '1.jpg';
            } else {
                oImg.src = '2.jpg';
            }
            
            obj.style.left = L + 'px';
            obj.style.top = T  + 'px';
            
        }
        
        document.onmouseup = function(){
            document.onmousemove = document.onmouseup = null;
            
            if(obj.releaseCapture){
                obj.releaseCapture();
            }
        }
        
        return false;
    }   
}
~~~

###拖拽改变层大小

~~~ html
<div id="div1"></div>
~~~

~~~ css
#div1 { width: 100px; height: 100px; background: red; position: absolute; left: 500px; top: 200px; }
~~~

~~~ js
var oDiv = document.getElementById('div1');

oDiv.onmousedown = function(ev){
    var ev = ev || event;
    var disW = this.offsetWidth;
    var disX = ev.clientX;
    var disL = this.offsetLeft;
    var b = '';
    
    if(disX > disL + disW - 10){
        b = 'right';
    }
    if(disX < disL + 10){
        b = 'left';
    }
    
    document.onmousemove = function(ev){
        var ev = ev || event;
        switch(b){
            case 'left':
                oDiv.style.width = disW - (ev.clientX - disX) + 'px';
                oDiv.style.left = disL + (ev.clientX - disX) + 'px';
                break;
            case 'right':
                oDiv.style.width = disW + (ev.clientX - disX) + 'px';
                break
        }
    }
    document.onmouseup = function(){
        document.onmousemove = document.onmouseup = null;
    }
    return false;
}
~~~

###滚动条的模拟和扩展运用

~~~ html
<div id="div1">
    <div id="div2></div>
</div>
<div id="div3></div>
~~~

~~~ css
#div1 { width: 30px; height: 500px; background: black; position: absolute; left: 10px; top: 10px; }
#div2 { width: 30px; height: 30px; background: red; position: absolute; left: 0; top: 0 }
#div3 { width: 500px; height: 500px; background: green; position: absolute; left: 50px; top: 10; }
~~~

~~~ js
var oDiv1 = document.getElementById('div1');
var oDiv2 = document.getElementById('div2');
var oDiv3 = document.getElementById('div3');
var iMaxTop = oDiv1.offsetHeight - oDiv2.offsetHeight;

oDiv2.onmousedown = function(ev){
    var ev = ev || event;
    var disY = ev.clientY - this.offsetTop;
    
    document.onmousemove = function(ev){
        var ev = ev || event;
        var T = ev.clientY - disY;
        
        if(T < 0){
            T = 0;
        } else if(T > iMaxTop){
            T = iMaxTop;
        }
        oDiv2.style.top = T + 'px';
        
        var iScale = T / iMaxTop;
        oDiv3.style.height = 500 * iScale + 'px';
    }
    document.onmouseup = function(){
        document.onmousemove = document.onmouseup = null;
    }
    
    return false;
}
~~~

**控制内容的滚动**

~~~ html
<div id="div1">
    <div id="div2"></div>
</div>
<div id="div3>
    <div id="div4">这里是一段内容。</div>
</div>
~~~

~~~ css
#div1 { width: 30px; height: 500px; background: black; position: absolute; left: 10px; top: 10px; }
#div2 { width: 30px; height: 30px; background: red; position: absolute; left: 0; top: 0 }
#div3 { width: 498px; height: 498px; border: 1px solid green; position: absolute; left: 50px; top: 10; }
#div4 { position: absolute; top: 0; left: 0; }
~~~

~~~ js
var oDiv1 = document.getElementById('div1');
var oDiv2 = document.getElementById('div2');
var oDiv3 = document.getElementById('div3');
var oDiv4 = document.getElementById('div4');
var iMaxTop = oDiv1.offsetHeight - oDiv2.offsetHeight;

oDiv2.onmousedown = function(ev){
    var ev = ev || event;
    var disY = ev.clientY - this.offsetTop;
    
    document.onmousemove = function(ev){
        var ev = ev || event;
        var T = ev.clientY - disY;
        
        if(T < 0){
            T = 0;
        } else if(T > iMaxTop){
            T = iMaxTop;
        }
        oDiv2.style.top = T + 'px';
        
        var iScale = T / iMaxTop;
        oDiv4.style.top = (oDiv3.clientHeight - oDiv4.offsetHeight) * iScale + 'px';
    }
    document.onmouseup = function(){
        document.onmousemove = document.onmouseup = null;
    }
    
    return false;
}
~~~

##鼠标滚轮和COOKIE

###鼠标滚轮事件

- IE/chrome: onmousewheel
    - event.wheelDelta 数字类型
        - 上：120
        - 下：-120
    - 标准浏览器下的event.detail永远都是0；非标准IE的event.detail是undefined
- ff: DOMMouseScroll 必须用addEventListener来实现绑定
    - event.detail
        - 下：3
        - 上：-3

- **return false**阻止的是obj.on事件名称=fn 所触发的默认行为，阻止不了addEventListener绑定的行为
- 用addEventListener绑定的事件需要通过event下面的**preventDefault();**来阻止默认行为
- IE下用attachEvent来绑定的话，还是可以用return false来阻止默认事件

也就是说阻止默认行为不是看事件，而是看事件的绑定形式

~~~ html
<div id="div1"></div>
~~~

~~~ css
body { height: 2000px; }
#div1 { width: 100px; height: 100px; background: red; }
~~~

~~~ js
var oDiv = document.getElementById('div1');

oDiv.onmousewheel = fn;

if(oDiv.addEventListener){
    oDiv.addEventListener('DOMMouseScroll', fn, false);
}

function fn(ev){
    var ev = ev || event;
    
    var b = true;
    if(ev.wheelDelta){
        b = ev.wheelDelta > 0 ? true : false;
    } else {
        b = ev.wheelDelta > 0 ? false : true;
    }
    
    if(b){
        this.style.height = this.offsetHeight - 10 + 'px';
    } else {
        this.style.height = this.offsetHeight + 10 + 'px';
    }
    
    if(ev.preventDefault){
        ev.preventDefault();
    }
    
    return false;
}
~~~

###cookie

- cookie：用来存储数据，当用户访问了某个网站（网页）的时候，我们就可以通过cookie来向访问者的电脑上存储数据。
    - 不同的浏览器存放的cookie位置不一样，也是不能通用的
    - cookie的存储是以域名的形式进行区分的
    - cookie的数据是可以设置名字的
    - 一个域名下存放的cookie的个数是有限制的。不同的浏览器存放的个数不一样
    - 每一个cookie存放的内容大小也是有限制的，不同的浏览器存放的内容大小不一样

我们通过document.cookie来获取当前网站下的cookie的时候，得到的是字符串形式的值，它包含了当前网站下所有的cookie。它会把所有的cookie通过一个分号+空格的形式串联起来。

如果我们想长时间存放一个cookie，需要在设置这个cookie的时候，同时给它设置一个过期的时间(这个时间必须是字符串格式)。cookie默认是临时存储的，当浏览器关闭进程的时候，自动销毁。
 
**有关cookie的操作**

~~~ js
//document.cookie = '名字=值;expires=' + 字符串格式的时间;
var oDate = new Date();
oDate.setDate( oDate.getDate() + 5 ); //5天以后
//oDate.toGMTString(); //将日期对象转换为字符串格式

//内容最好编码存放，encodeURI
//alert(encodeURI('你好'));
//alert(decodeURI('%E4%BD%A0%E5%A5%BD'));

document.cookie = 'username =' + encodeURI('leo\n你好') + ' leo;expires=' + oDate.toGMTString();
document.cookie = 'age = 32';
alert(decodeURI(document.cookie));

function getCookie(key){
    var arr1 = document.cookie.split('; ');
    for(var i=; i<arr1.length; i++){
        var arr2 = arr1[i].split('=');
        if(arr2[0] == key){
            return decodeURI(arr2[1]);
        }
    }
}

alert(getCookie('age'));

function setCookie(key, value, t){
    var oDate = new Date();
    oDate.setDate( oDate.getDate() + t );
    document.cookie = key + '=' + value + ';expires=' + oDate.toGMTString();
}

setCookie('sex', '男', 10);

function removeCookie(key){
    setCookie(key, '', -1);
}

removeCookie('username');
~~~

**cookie的应用-记录登录名**

~~~ html
<input type="text" id="username" />
<input type="button" value="登陆" id="login" />
<input type="button" value="删除" id="del" />
~~~

~~~ js
var oUsername = document.getElementById('username');
var oLogin = document.getElementById('login');
var oDel = document.getElementById('del');

if(getCookie('username')）{
    oUsername.value = getCookie('username');
}

oLogin.onclick = function(){
    alert('登陆网站成功');
    setCookie('username', oUsername.value, 5);
}

oDel.onclick = function(){
    removeCookie('username');
    oUsername.value = '';
}

function getCookie(key){
    var arr1 = document.cookie.split('; ');
    for(var i=; i<arr1.length; i++){
        var arr2 = arr1[i].split('=');
        if(arr2[0] == key){
            return decodeURI(arr2[1]);
        }
    }
}

function setCookie(key, value, t){
    var oDate = new Date();
    oDate.setDate( oDate.getDate() + t );
    document.cookie = key + '=' + value + ';expires=' + oDate.toGMTString();
}

function removeCookie(key){
    setCookie(key, '', -1);
}

~~~



