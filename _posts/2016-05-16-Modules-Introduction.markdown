---
layout: post
title: JS中的模块的基础知识
category: study
description: 主要内容来自于《Eloquent Javascript》一书的第10章
tags:
- 学习笔记
- js
- moduel
- 模块
---

##使用function作为命名空间

function是在JS中唯一能够创建新的作用域的东西（暂不考虑ES6）。因此，如果想让我们的module有自己的作用域，那么就需要利用function来实现。

看看下面这个很小的module，它将一周的日子的名称与数字对应起来了：

```js
var names = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];

function dayName(number){
	return names[number];
}

console.log(dayName(1));
//Monday
```

`dayName`函数就是这个模块接口的一部分，但是变量`names`不是。我们最好不要污染全局空间。于是，我们可以这么做：

```js
var dayName = function(){
	var names = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
	return function(number){
		return names[number];
	}
}();

console.log(dayName(3));
//Wednesday
```

这时候，`names`是一个（匿名）函数的局部变量。这个函数一经创建就立即执行了，而且返回了值（返回了真正的dayName函数）存储在变量中。

我们可以用类似的模式将代码与外边的世界彻底隔绝开来。下面的模块在控制台里面打出一个值来，但实际上没有供任何其他模块利用的值：

```js
(function(){
	function square(x){
		return x*x;
	}
	var hundred = 100;
	console.log(square(hundred));
})();
//10000
```

这一段代码只是输出了100的平方，但现实世界中，它可以是一个用来为prototype添加方法的模块，或者在网页上设置widget的模块。它是包裹在一个函数里面，以免在内部使用的变量污染到全局空间。

##object作为接口

现在，想象我们想为前面的有关一周每天的名称的模块添加另一个函数，这个函数是要把每天的名称转换为对应数字。我们不能再简单地返回函数了，而必须要将两个函数包在一个对象里面。

```js
var weekDay = function(){
	var names = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
	return {
		name: function(numbers){ return names[number]; },
		number: function(name){ return names.indexOf(name); }
	}
}();

console.log(weekDay.name(WeekDay.number("Sunday")));
//Sunday
```

对于更大的模块来说，把所有exported（输出的）值都集中在一个函数结尾处的一个object里会变得很奇怪，因为很多输出的函数可能会很复杂，我们倾向于把它们写在别处，靠近相关内部代码的地方。另外一种更方便的方式就是声明一个object（通常名为exports），然后每当我们定义了某些需要输出的东西，就把属性添加到这个对象里面。在下面的例子中，模块函数将其接口对象（exports）用作参数，这样就可以让函数外面的代码创建它并且把它保存在一个变量里了。（在函数外面，`this`指的是全局对象）。

```js
(function(exports){
	var names = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
	exports.name = function(number){
		return names[number];
	};
	exports.number = function(name){
		return names.indexOf(name);
	};
})(this.weekDay = {});

console.log(weekDay.name(weekDay.number("Saturday")));
//Saturday
```

##从全局范围内解脱出来

上面那个模式经常被用作Javascript用于浏览器的模块。这个模块只会声明一个全局变量，并且将其代码包在一个函数里面，以便让它有自己私有的命名空间。但这种模式还是会造成问题，如果多个模块声明了同一个名称或者你想一个接一个地加载同一模块的两个版本，就会发生问题。

接下来进行一点调整，我们可以让一个模块直接去用另一个模块的接口对象，而不需要通过全局。我们的目标是构成一个`require`函数，给它一个模块名称，它就会加载那个模块的文件（从硬盘或网络，基于我们所在的平台），然后将合适的接口值返回来。

这种方法解决了我们之前提到的问题，而且还让我们程序的依赖关系表达得更清楚，使你不太容易不小心用到某个模块，却没有说明你需要它。

对于这样一个require函数，我们需要两个事情。首先是一个readFile函数，它能把一个指定文件的内容作为字符串返回回来。（在标准JavaScript中，没有这样一个单独的函数，但是不同的JS环境，比如浏览器和Node.js，都有它们自己处理文件的方式。现在，我们先假装有这么一个函数）。第二，我们需要能够将这个字符串作为JS代码执行。


##将数据作为代码运行

有很多方式能够将数据（一段代码的字符串）运行起来。

最明显的一种方式就是用eval这个运算符，它能够在*当前*作用域下把字符串作为代码运行。但eval并不是一个被提倡使用的方法。另一种是使用Function构造函数。这个构造函数最后一个参数是函数体的内容，是字符串格式；前面的参数都是这个构造函数构造出来的函数的参数，例如：

```js
var plusOne = new Function("n", "return n + 1;");
console.log(plusOne(4));
//5
```

我们正好可以把这种方式利用到我们的module上来。我们可以把一个module的代码包在一个函数里，那么这个函数的作用域就是我们的模块作用域。

##require

下面就是一个require的最小实施的例子：

```js
function require(name){
	var code = new Function("exports", readFile(name));
	var exports = {};
	code(exports);
	return exports;
}

console.log(require("weekDay").name(1));
// Monday
```

由于`new Function`这个构造函数把模块的代码包在一个函数里面了，那么我们就没有必要再在module自己的文件里面写一个用来包裹代码的命名空间函数了。而且因为我们将`exports`作为参数传到了module的函数里面，那么在module本身的代码中就不需要再声明它了。这样就移除了我们module例子中很多不需要的代码。module文件中的代码现在变成了下面这个样子：

```js
var names = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
exports.name = function(number){
	return names[number];
}
exports.number = function(name){
	return names.indexOf(name);
}
```

采用了这种写法的话，使用一个模块通常是先声明变量，并且将其依赖的模块加载到这个变量上。

```js
var weekDay = require("weekDay");
var today = require("today");
console.log(weekDay.name(today.dayNumber()));
```

前面这种简单的使用require的方式会导致很多问题。其中一个问题就是它会加载并运行每一个require了的模块。一次，如果许多模块都依赖同一个库或者require的调用放在了一个要运行多次的函数里面，那么就造成了时间和效率的浪费。

要解决这个问题，可以这样做：把已经加载的模块放到一个对象里面，如果要用到多次的话，就直接从这个对象里取出来。

第二个问题是模块只能直接导出`exports`对象，不能导出其他类型。如果想要导出一个函数就没办法了。例如：一个模块可能只想exports某个对象类型的构造函数。目前，我们没法这么做，因为require始终将exports对象作为导出的值。

解决第二个问题的传统做法是为模块提供另外一个变量module，这个module是一个对象，它的一个属性就是exports。module的exports属性一开始就指向由require创建的空白对象，但是也可以用其他值改写，这样就能返回其他值了。

```js
function require(name){
	//如果名为name的这个模块已经加载过了，就会被储存在require.cache里面，用的时候，直接从require.cache这个对象里面取出来就可以了
	if(name in require.cache){
		return require.cache[name];
	}

	var code = new Function("exports, module", readFile(name));
	var exports = {}, module = {exports: exports}; //module的exports属性一开始就指向exports这个对象，因此后续exports对象更改之后，module的exports属性仍然是指向它的
	code(exports, module);
	
	require.cache[name] = module.exports; //首次加载的module被存到require.cache中。
	return module.exports;
}
require.cache = Object.create(null); //将require.cache设置为一个仅用来保存键值对的对象。没有其他多余的属性。
```

我们现在有了一个模块系统，这个系统只用一个全局变量（require）就能让模块找到并利用其他模块，而不需要经过全局作用域。

这种模块系统被称为CommonJS模块，这也是Node.js系统内置的模块机制。真正实施起来比上面的例子要复杂一些，上面只是基本原理的介绍。

##异步加载模块（AMD）

CommonJS模块形式是阻塞式的。也就是说，其中一个模块没加载好，浏览器就得在那里等着，什么事也干不了。

解决这个问题的一种方式是利用Browserify这样的程序把代码先处理一下再放到网页上。它会先找到require的调用，然后把所有的依赖就加载下来，并且将所需代码集中到一个比较大的文件里面。那样，网站就可以只加载这个文件，就能得到所有需要的模块了。

另一种解决方式就是把模块的代码用函数包起来，使模块加载器首先在后台加载模块代码的依赖，然后当所有的依赖都已经加载好了，再调用这个函数，初始化这个模块。AMD模块系统就是这么干的。

在AMD里面，一个小小的带有依赖的程序长得像下面这样：

```js
define(["weekDay", "today"], function(weekDay, today){
	console.log(weekDay.name(today.dayNumber()));
})
```

上面的程序的意思就是说`console.log...`这一行代码依赖weekDay和today这两个模块，因此将这两个模块名写在define的第一个参数的数组里面。然后，当这两个模块在后台加载好了，就会调用define的第二个参数，也就是一个回调函数，这个回到函数的参数就是加载好的两个模块的接口。

define函数是这种方法的核心。define函数的第一个参数是数组，里面是模块的名称；第二个参数是回调函数，回调函数中的每个参数都是函数内部代码的依赖的接口。

通过这种方式被加载的模块也必须包含这样一个define调用。被加载模块的接口就是任何define的回调函数所返回的值。下面是用这种方式改写的weekDay模块：

```js
define([], function(){
	var names = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
	return {
		name: function(number){return names[number];},
		number: function(name){return names.indexOf(name);}
	};
});
```

由于weekDay本身这个模块不依赖于其他模块，因此define第一个参数数组为空，回调函数的参数也为空。

为了能够看一下define的一个最简单的实施方法，我们需要假装有一个`backgroundReadFile`的函数，这个函数的参数有两个，第一个是文件名，第二个是一个函数，而且当文件内容一加载完，就用加载好的文件内容作为参数去调用这个函数。

为了在模块加载的时候能够追踪它们的状态，在实施define的时候，要用到描述模块状态的对象，这个对象能告诉你这些模块是不是已经能用了，并且在模块已经加载好的时候，提供他们的接口。

`getModule`函数是这样的，传入一个name，它就返回这样一个module对象，并且确保名为name的这个模块已经被安排加载了。它用一个cache对象来避免重复加载同样的模块。

```js
var defineCache = Object.create(null);
var currentMod = null; //初始currentMod指向一个空对象

function getModule(name){
	//如果名为name的模块已经加载过，在defineCache里面有，那么就直接取出来
	if(name in defineCache){
		return defineCache[name];
	}

	//如果要加载一个新模块，那么一开始设置这个模块的初始状态
	var module = {
		exports: null,
		loaded: false,
		onLoad: []
	};

	//将这个要加载的模块加到defineCache对象里面
	defineCache[name] = module;
	backgroundReadFile(name, function(code){
		//backgroundReadFile函数要做的事情就是后台加载文件名为name的文件，加载好之后，就用这个文件的内容来调用回调函数，也就是说回调函数的参数code的实参就是加载的文件的内容
		//code应该也是一个define函数

		//将currentMod指向这个模块
		currentMod = module;
		new Function("", code)(); //这里的code也是个define函数
	})
	return module;
}
```

我们假设被加载了的文件也包含一个define的调用（也就是假设上面的code也包含一个define函数的调用）。那么currentMod这个变量就是要告诉这个调用目前正在被加载的模块对象（module）是什么。

define函数本身用getModule函数为当前模块的依赖获取或创建模块对象。define函数的任务是当那些依赖都已经加载好时，安排`moduleFunction`（即包含这个模块真正代码的函数）去执行。

为了达到这个目的，define函数中定义了一个whenDepsLoaded函数，并且把这个函数加到所有还没有加载完成的module的onLoad数组里面，这个数组里面放的应该是当module完成加载之后，要执行的一些函数。如果还有没加载的依赖，那么这个函数就立即返回，因此只有当最后一个依赖也加载完成，这个函数才会真正做一次工作。假如没有再需要加载的依赖了，它也是被define立即调用的。

```js
function define(depNames, moduleFunction){
	var myMod = currentMod;
	var deps = depNames.map(getModule); //deps里面放的是每个依赖对应的module对象

	deps.forEach(function(mod){
		if(!mod.loaded){
			mod.onLoad.push(whenDepsLoaded); //如果module没有加载完，那么就往这个module的onLoad数组中加上whenDepsLoaded函数
		}
	})

	function whenDepsLoaded(){
		if(!deps.every(function(m){return m.loaded;})){
			return; //只要deps里面有一个模块没加载好，就直接返回
		}

		//如果都加载好了，那么：
		var args = deps.map(function(m){return m.exports;}); //args里面放的就是每个模块返回的接口
		var exports = moduleFunction.apply(null, args); //exports就是当前define中定义的回调函数以args为参数执行所返回的值

		if(myMod){
			myMod.exports = exports;
			myMod.loaded = true;
			myMod.onLoad.forEach(function(f){f();});
		}
	}
	whenDepsLoaded();
}
```

当所有依赖都可用了，whenDepsLoaded就调用包含module的函数，并且将依赖的接口作为参数传给这个函数。

define函数被调用后，做的第一件事情就是把currentMod中的值保存在了myMod变量中。还记得那个getModule函数吗，在getModule执行`new Function("", code)();`之前，将对应的module对象保存在currentMod当中。在define函数当中国，myMod也指向了这个module对象。这样使whenDepsLoaded函数能够将模块函数moduleFunction返回的值保存在这个module对象的exports属性里，将这个module对象的loaded属性设置为true并且调用所有等待这个module加载完成的函数。



