---
layout: post
title: 循环事件的闭包
category: study
description: 《Eloquent Javascript》第14章书后练习
tags:
- 学习笔记
- js
---

题目很实用，就是实现一个Tab页。写一个函数asTabs，这个函数的参数是一个dom节点。这个dom节点的子节点是每个tab页的内容。并且要动态生成一个`button`的列表，点击对应的button，可以显示tab页的内容。

这个题目总结如下：

```html
<div id="wrapper">
  <div data-tabname="one">Tab one</div>
  <div data-tabname="two">Tab two</div>
  <div data-tabname="three">Tab three</div>
</div>
<script>
  function asTabs(node) {
    // Your code here.
  }
  asTabs(document.querySelector("#wrapper"));
</script>
```

这个题目牵扯到为button循环添加点击事件。首先看看问题所在。

```js
//假设buttons节点就是wrapper中添加的button的nodeList，如果用for循环来添加点击事件的话：
for(var i = 0; i < buttons.length; i++){
    buttons[i].addEventListener("click", function(event){
        alert(i);
    });
}
//最终所有button点击之后，弹出的都是3
```

先看作者答案中的解决办法：

```html
<div id="wrapper">
  <div data-tabname="one">Tab one</div>
  <div data-tabname="two">Tab two</div>
  <div data-tabname="three">Tab three</div>
</div>
<script>
  function asTabs(node) {
    var tabs = [];
    for (var i = 0; i < node.childNodes.length; i++) {
      var child = node.childNodes[i];
      if (child.nodeType == document.ELEMENT_NODE)
        tabs.push(child);
    }

    var tabList = document.createElement("div");
    tabs.forEach(function(tab, i) {
      var button = document.createElement("button");
      button.textContent = tab.getAttribute("data-tabname");
      button.addEventListener("click", function() { selectTab(i); });
      tabList.appendChild(button);
    });
    node.insertBefore(tabList, node.firstChild);

    function selectTab(n) {
      tabs.forEach(function(tab, i) {
        if (i == n)
          tab.style.display = "";
        else
          tab.style.display = "none";
      });
      for (var i = 0; i < tabList.childNodes.length; i++) {
        if (i == n)
          tabList.childNodes[i].style.background = "violet";
        else
          tabList.childNodes[i].style.background = "";
      }
    }
    selectTab(0);
  }
  asTabs(document.querySelector("#wrapper"));
</script>
```

通过将nodeList转化为array，作者可以利用forEach高阶函数。该高阶函数的第二个变量就是当前元素在array中的index，这样就避开了for循环中变量问题。值得注意的是，作者在创建button的时候，就addEventListener了。也就是说，在为第一个button添加eventlistener的时候，后面的button还没有生成。但是因为addEventListener的回调函数中的tabList.childNodes是live的，所以添加eventlistener的时候，button是否添加完全并不成问题。当点击的时候，tabList.childNodes就包含了所有的button了。

第二种方法是通过闭包的方法，将for循环中的i冻住，方法如下：

```html
<div id="wrapper">
  <div data-tabname="one">Tab one</div>
  <div data-tabname="two">Tab two</div>
  <div data-tabname="three">Tab three</div>
</div>
<script>
  function asTabs(node) {
    var wrapper = document.querySelector("#wrapper");
    var tabs = wrapper.querySelectorAll("div");
    var tabCount = tabs.length;
    var buttons, button;
    var tabList = document.createElement("div");
    
    for(var i = 0; i < tabCount; i++){
        button = document.createElement("button");
        button.textContent = tabs[i].getAttribute("data-tabname");
        tabList.appendChild(button);
    }
    wrapper.insertBefore(tabList, tabs[0]);
    buttons = tabList.querySelectorAll("button");
    
    function selectTab(index){
        for(var i = 0; i < tabCount; i++){
            if(i == index){
                buttons[i].style.background = "violet";
                tabs[i].style.display = "";
            } else {
                buttons[i].style.background = "";
                tabs[i].style.display = "none";
            }
        }
    }
    
    selectTab(0);
    
    for(var i = 0; i < tabCount; i++){
        buttons[i].addEventListener("click", (function(index){
            return function(event){
                selectTab(index);
            }
        })(i));
    }
  }
  asTabs(document.querySelector("#wrapper"));
</script>
```

通过闭包的方式，在addEventListener的回调函数处设置一个立即调用的匿名函数，通过这种方式，该匿名函数内部的函数就锁定了外部的变量。

第三种方式是通过在for循环中的每个元素添加自定义属性的方式来实现：

```html
<div id="wrapper">
  <div data-tabname="one">Tab one</div>
  <div data-tabname="two">Tab two</div>
  <div data-tabname="three">Tab three</div>
</div>
<script>
  function asTabs(node) {
    var wrapper = document.querySelector("#wrapper");
    var tabs = wrapper.querySelectorAll("div");
    var tabCount = tabs.length;
    var buttons, button;
    var tabList = document.createElement("div");
    
    for(var i = 0; i < tabCount; i++){
        button = document.createElement("button");
        button.textContent = tabs[i].getAttribute("data-tabname");
        tabList.appendChild(button);
    }
    wrapper.insertBefore(tabList, tabs[0]);
    buttons = tabList.querySelectorAll("button");
    
    function selectTab(index){
        for(var i = 0; i < tabCount; i++){
            if(i == index){
                buttons[i].style.background = "violet";
                tabs[i].style.display = "";
            } else {
                buttons[i].style.background = "";
                tabs[i].style.display = "none";
            }
        }
    }
    
    selectTab(0);
    
    for(var i = 0; i < tabCount; i++){
        buttons[i].index = i; //为每一个button添加自己的属性index，不同button对应的index不同
        buttons[i].addEventListener("click", function(event){
            selectTab(this.index); //通过this来调用button本身具有的index属性值
        });
    }
  }
  asTabs(document.querySelector("#wrapper"));
</script>
```