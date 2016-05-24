---
layout: post
title: 写一个你自己的编程语言
category: study
description: 主要内容来自于《Eloquent Javascript》一书的第11章
tags:
- 学习笔记
- js
---

##先定义这个语言是个什么样子

作者想要写一个名为Egg的语言。没错，就是Egg，虽然小但却能孵出小鸡的蛋，也可以被看成一种雏形吧。我感觉这一章值得译一遍，然后反复地看几遍。最好能达到自己也能不参照书本，也能写出来一个！

Egg这门语言中全都是表达式。表达式可能是一个variable、number、string或application。

- string：一串不是双引号的字符，并且是被双引号引起来的
- number：一串数字
- variable；可以包含任何非空白字符和其他在Egg中有特殊意义的字符
- application就相当于Egg中的函数，或者是if、while。applicatio的写法就是：后面加上括号，括号里面可以有任意数量的变量，变量之间用逗号隔开。这与javascript中的函数的写法很类似（就是去掉了后面的大括号）

举个栗子：

```js
do(define(x, 10),
	if(>(x, 5),
		print("large"),
		print("small")))
```

其中：
- do、define、>、if、print都是application
- 出现的两个x都是variable，因为它没有双引号，所以不是string；10和5都是number；"large"和"small"都是string
- define的变量是x, 10；>的变量是x, 5；print的变量分别是"large"和"small"

从中我们可以看到，原本在js中的操作符，例如">"在这里直接是作为application使用的，也就是后面也跟着括号和参数。

##解析（Parsing）

接下来，我们要为这门语言写一个解析器。解析器其实就是一个程序，它读取一段文字，然后产生一个数据结构。这个数据结构要体现这段文字所包含的程序的结构。如果这段文字不符合程序的要求，那么解析器就要报错。

为了让解析器不至于太复杂，我们假设Egg中的string不支持反斜线这样的转义符号。

Egg的数据结构是这样的：

- 首先，每个表达式都是一个对象
- 每个表达式对象都包含一个type属性。type属性的值目前有三种：word、value和apply。
- value类型的表达式具有另外一个value属性，里面放的是string或number
- word类型的表达式具有另外一个name属性，里面放的是一个标识符，这个标识符本身是个string
- apply类型的表达式具有另外两个属性：一个是operator，它里面放的是一个表达式对象，用来保存执行了什么application；另一个是args属性，它是一个数组，里面放的是一个个参数，每个参数又都是表达式。

再举个栗子：>(x, 5) 的数据结构就是下面这种形式：

```js
{
	type: "apply",
	operator: {type: "word", name: ">"},
	args: [
		{type: "word", name: "x"},
		{type: "value", value: 5}
	]
}
```

要解析下面这整段Egg代码：

```js
do(define(x, 10),
	if(>(x, 5),
		print("large"),
		print("small")))
```

很明显要用到递归，名为do的application中包着两个参数：define和if。define包着两个参数x和10；if包着三个参数 > 和两个print，然后它们由各自包着两个或一个参数。

这是一个很明显的语法树：

```
do
 |--define
     |--x
     |--10
 |--if
     |-->
        |--x
        |--5
     |--print
        |--"large"
     |--print
        |--"small"
```

首先，我们先写一个parseExpression的函数来解析单个表达式。它以一串string作为参数，然后返回一个对象，这个对象包含这串string一开始的表达式的数据结构以及string在解析了这个表达式之后剩下来的部分。然后再解析子表达式（比如一个application的参数）时，就可以再调用这个函数。以此类推，实现递归。

```js
function parseExpression(program){
	program = skipSpace(program);
	var match, expr;
	if(match = /^"([^"]*)"/.exec(program)){
		//任何双引号中非双引号字符的都是string
		expr = {type: "value", value: match[1]};
	} else if(match = /^\d+\b/.exec(program)){
		//任何从头到尾都是数字的都是number
		expr = {type: "value", value: Number(match[0])};
	} else if(match = /^[^\s(),"]+/.exec(program)){
		//任何非空白、非括号、非逗号、非双引号的字符
		expr = {type: "word", name: match[0]};
	} else {
		throw new SyntaxError("Unexpected syntax: " + program);
	}

	return parseApply(expr, program.slice(match[0].length));
}

function skipSpace(string){
	var first = string.search(/\S/);
	if(first == -1) {
		return "";
	}
	return string.slice(first);
}
```

上面的parseExpressions最后将解析过的表达式，与切掉了匹配该表达式的字符剩下的字符串传给了parseApply函数。parseApply函数用于检查这个表达式究竟是不是一个application。如果是的话，parseApply就解析括号中一组参数。

```js
function parseApply(expr, program){
	program = skipSpace(program);
	if(program[0] != "("){
		//这说明不是一个expr不是一个application
		return {expr: expr, rest: program};
	}
	
	//如果expr是一个application，那么就将program开头的括号去掉，然后给expr重新赋值成application类型的表达式对象，原来传入的expr就成了新的表达式对象的operator属性
	program = skipSpace(program.slice(1));
	expr = {type: "apply", operator: expr, args: []};

	while(program[0] != ")"){
		var arg = parseExpression(program);
		expr.args.push(arg.expr);
		//arg为解析好的一个参数，然后解析好的参数与剩余的string就被传入parseApply里面来了。如果args后面不是左括号，则返回{expr: expr, rest: program}对象，这时候可以看到arg.rest就是解析完arg之后剩余的字符串
		program = skipSpace(arg.rest);
		//在参数括号里面，每解析完一个表达式，剩余的在去掉空白之后，都应该是逗号或右括号，否则就语法出错了。
		if(program[0] == ","){
			program = skipSpace(program.slice(1));
		} else if(program[0] != ")"){
			throw new SyntaxError("Expected ',' or ')'");
		}
	}
	return parseApply(expr, program.slice(1));
}
```

这里的递归并非直接递归，是通过parseApply与parseExpression的互相调动实现的。

由于application表达式也可以自己是一个application表达式（就像multiplier(2)(1)这样，multiplier(2)也是一个application表达式，后面才能跟(1)作为参数）。所以，当parseApply在解析了一个application之后，还是要再次调用parseApply来检查是否后面又跟着括号。

有parseExpression和parseApply这两个函数就足以让我们解析Egg语言了。现在我们把这两个函数包在一个parse函数里面，用它来确认解析了这个表达式（一个Egg程序也是一个单独的表达式）之后，是不是就到了传入的string的结尾，如果到达结尾，就返回给我们整个程序的数据结构：

```js
function parse(program){
	var result = parseExpression(program);
	if(skipSpace(result.rest).length > 0){
		throw new SyntaxError("Unexpected text after program");
	}
	return result.expr;
}

console.log(parse("+(a, 10)"));
//{
//	type: "apply",
//	operator: {type: "word", name: "+"},
//	args: [{type: "word", name: "a"},
//		{type: "value", value: 10}]
//}
```

##求值程序（Evaluator）

现在，我们能对一个程序的语法树进行怎样的处理呢？当然是要运行它！这就是求值程序做的事情。你给这个求值程序传入一个语法树以及一个环境对象（这个环境对象将name与值关联起来），这个求值程序就会为这个语法树所代表的表达式求值，然后返回所得的值。

```js
function evaluate(expr, env){
	switch(expr.type){
		case "value":
			return expr.value;
		case "word":
			if(expr.name in env){
				return env[expr.name];
			} else {
				throw new ReferenceError("Undefined variable: " + expr.name);
			}
		case "apply":
			if(expr.operator.type == "word" && expr.operator.name in specialForms){
				//如果在specialForms中定义过了，那么就直接以expr.operator.name为函数名，将参数和环境变量传入执行，返回数值。
				return specialForms[expr.operator.name](expr.args, env);
			}
			
			//如果没有在specialForms中定义，那么就将expr.operator作为第一个参数，环境变量作为第二个参数传入evaluate，由于expr.operator的type应该是word，所以又走到了evaluate的case "word“这里，返回env[expr.name]给op。如果expr.name不在env中，就报Undefined variable的错。
			var op = evaluate(expr.operator, env);
			//如果在env中找到了expr.name，那么看这个expr.name是否定义为了函数。如果不是函数的话，就根本apply不了，执行不下去了，所以要报Applying a non-function的错。
			if(typeof op != "function"){
				throw new TypeError("Applying a non-function.");
			}
			//如果在env中找到了expr.name，并且expr.name在env中确实被定义为了函数，那么就利用apply，将expr.args转化为实际的参数值，传入这个函数。
			return op.apply(null, expr.args.map(function(arg){
				return evaluate(arg, env);
			}))
	}
}
var specialForms = Object.create(null);
```

evaluator函数针对每一个表达式类型都进行了处理。字面值（string或者number）就直接返回。对于变量，我们必须检查它有没有在环境中被定义过，如果定义了，那么就返回变量的值。

对于application就更加复杂。如果是特殊形式（specialForm），例如if，那么我们不需要evaluate任何东西，只是将参数表达式连同环境对象传给一个处理这个form的函数。如果是一个普通的调用，那么我们就要evaluate这个operator，证实它确实是一个function，那么就把求过值的参数传给它。

我们会用普通的js函数值来代表Egg的函数值。当我们在后面定义fun这个special form的时候，会再来讲这一点。

evaluate函数也是递归的，这一点与解析器的结构类似。两者有都与Egg语言本身的结构类似。当然，将解析器和求值器结合起来，在解析的时候求值也未尝不可，但是把两者分开来，程序上会更容易读一些。

其实要解释Egg语言，这些就够了，就这么简单。但是如果不定义几个special form或者往环境里添加几个有用的值，你目前就不能用这个语言做任何事情。

##特殊形式 Special forms

specialForm对象是用来定义Egg中的特殊语法的。它将word与对这些special form进行求值的function联系起来。现在这个specialForm还是空的。让我们往里面添加几种形式：

```js
specialForms["if"] = function(args, env){
	if(args.length != 3){
		throw new SyntaxError("Bad number of args to if");
	}

	if(evaluate(args[0], env) !== false){
		return evaluate(args[1], env);
	} else {
		return evaluate(args[2], env);
	}
}
```

这一部分对if的定义很简单，Egg中的if需要三个参数，第一个参数是条件，如果不为假，就返回第二个参数的求值，否则就返回第三个参数的求值。

之所以我们要将 if 作为一个specialForm来看待，而不是作为一个普通函数来看待，这是因为普通函数的所有变量在函数调用**之前**就被evalutate了，而if这种结构只需要根据第一个参数evaluate之后的值，再evaluate第二个或第三个参数其中一个就可以了。

对于while形式也是类似的：

```js
specialForms["while"] = function(args, env){
	if(args.length != 2){
		throw new SyntaxError("Bad number of args to while");
	}

	while(evaluate(args[0], env) !== false){
		evaluate(args[1].env);
	}

	//由于Egg语言中不存在undefined，所以如果没有有意义的结果时，我们返回false
	return false;
}
```

另一个基本的形式是 do，它从上向下执行它所有的参数。它的值就是最后一个参数所求得的值。

```js
specialForms["do"] = function(args, env){
	var value = false;
	args.forEach(function(arg){
		value = evaluate(arg, env);
	});

	return value;
}
```

为了能够创建变量并且为它们赋新值，我们要创建一种名为define的形式。它需要一个word类型作为第一个参数，另一个参数是一个表达式，它能产生值赋给那个word。既然define也是一个表达式，那么它也必须返回一个值。我们让这个返回值就是那个被赋的值（就像js中的 = 运算符一样）：

```js
specialForms["define"] = function(args, env){
	if(args.length != 2 || args[0].type != "word"){
		throw new SyntaxError("Bad use of define");
	}
	var value = evaluate(args[1], env);
	env[args[0].name] = value;
	return value;
};
```

##环境对象

被传入evaluate中的env是一个对象，里面放着变量名和对应的值。让我们来定义一个环境对象来表示全局作用域。

为了能够用上我们刚刚定义的 if，我们必须能够处理布尔值。既然布尔值只有两种，那么我们不需要为它们定义特殊语法。只需要将两个变量的值绑到true和false上，然后用起来就可以了。

```js
var topEnv = object.create(null);

topEnv["true"] = true;
topEnv["false"] = false;
```

现在我们可以为一个简单的表达式求值了：

```js
var prog = parse("if(true, false, true");
console.log(evaluate(prog, topEnv));
// false
```

要进行基本的数字和比较运算，我们还可以为环境变量里面添加一些函数值。为了让代码更简短，我们使用new Function来定义一系列运算符：

```js
["+", "-", "*", "/", "==", "<", ">"].forEach(function(op) {
  topEnv[op] = new Function("a, b", "return a " + op + " b;");
});
```

另外，输出值也是很有用的，因此我们将console.log包在一个函数里面，把这个函数成为print：

```js
topEnv["print"] = function(value){
	console.log(value);
	return value;
}
```

以上这些基本的工具已经足以让我们写一个简单的程序了。下面的run函数提供了一个编写和运行程序的简便方式。它创建了一个全新的环境，并且将我们传给它的字符串作为一个单独的程序进行解析和求值。

```js
function run(){
	var env = Object.create(topEnv);
	var program = Array.prototype.slice.call(arguments, 0).join("\n");
	return evaluate(parse(program), env);
}
```

使用Array.prototype.slice.call能够将类似数组的对象（例如arguments）转成真正的数组，然后我们就可以在数组上调用join了。run将所有传进去的参数视为一个程序的一行一行的内容。

```js
run("do(define(total, 0),",
    "   define(count, 1),",
    "   while(<(count, 11),",
    "         do(define(total, +(total, count)),",
    "            define(count, +(count, 1)))),",
    "   print(total))");
//55
```

上面的运行结果就是1加到10的和。

##函数

没有程序的编程语言是很破的语言。

幸运的是，不太困难就能加上一个名为fun的构造，这个fun将它的最后一个参数视为函数体，然后将所有前面的参数视为函数的参数：

```js
specialForms["fun"] = function(args, env){
    if(!args.length){
        throw new SyntaxError("Functions need a body");
    }
    //name函数是用来得到一个expr的name。由于参数都应当是word形式，所以不是word类型就应当报错。
    function name(expr){
        if(expr.type != "word"){
            throw new SyntaxError("Arg names must be words");
        }
        return expr.name;
    }
    var argNames = args.slice(0, args.length - 1).map(name);
    //用name这个函数对除最后一个args以外的所有args进行map，也就得到了一个除最后一个args以外的各个arg的name所组成的数组。这个数组中所放的，就是函数的所有参数。
    var body = args[args.length - 1];
    //args的最后一个就是函数体。

    return function(){ //很明显：fun这个函数返回的是一个函数
        if(arguments.length != argNames.length){
            //如果运行这个函数的时候，传入的实参与参数名的个数不匹配，那么就包括
            throw new TypeError("Wrong number of arguments");
        }
        var localEnv = Object.create(env); 
        //注意：上面这一句是利用传入的env为原型，构建了当前的localEnv，因此出现闭包的情况时，内部的局部环境变量localEnv仍然是可以访问到外部的环境变量env的。
        
        for(var i = 0; i < arguments.length; i++){
            //将一个个参数作为环境变量保存在局部环境对象里面。
            localEnv[argNames[i] = arguments[i]];
        }
        return evaluate(body, localEnv);
    };
};
```

Egg中的函数有自己的局部环境，就像在JavaScript中一样。我们使用Object.create来创建一个新对象，这个新对象可以访问到外面环境（它的原型）上的变量，但同时也可以在不修改外部环境的情况下包含新的变量。

通过fun创建的函数创建了这个局部环境，并且将参数变量加到这个局部环境中。然后，在这个局部环境下对这个函数体进行求值操作并返回结果。

```js
run("do(define(plusOne, fun(a, +(a, 1))),",
    "    print(plusOne(10)))");
//11
```

```js
run("do(define(pow, fun(base, exp,",
    "     if(==(exp, 0),",
    "        1,",
    "        *(base, pow(base, -(exp, 1)))))),",
    "   print(pow(2, 10)))");
//1024
```

##编译

我们造的是一个解释器。在求值过程中，这个解释器直接作用于解析器所产生的程序代码上。

*编译*则是在解析与运行程序之间又加了一步，它把程序转换为能够更有效率地进行求值的形式，就是提前把尽可能做的工作都做了。例如，在设计得很充分的语言里面，对于每一个变量的使用，它指的究竟是什么，在程序运行之前就一清二楚。这样就不用每次用到变量的时候再通过变量名去查找变量，并且直接能从预定的内存位置把它取出来。

从传统来说，编译包括将程序转换为机器代码，那是一种电脑的处理器能直接执行的原始格式。但是，将程序转换成另一种表达方式的过程都可以被视为编译。

也可以为Egg写另外一个求值的策略，就是先把程序转换为JS的程序，使用 new Function 来调用JS的编译器来编译它，然后运算出结果。只要写得得当，那会让Egg这门语言运行得非常快，而且实施起来也相当简单。

