---
layout: post
title: 妙味课堂——NodeJS分享视频
category: study
tags:
- js
- 妙味课堂
- nodejs
- 学习笔记
---

#NodeJS分享视频

##模块的使用和加载机制

```js
var a = 100;
console.log(a); //100
console.log(global.a); //undefined 因为这个a是定义在模块下面的变量，不属于全局变量
```

在nodejs中
- 一个文件就是一个模块
- 同时每个模块都有自己的作用域。

我们使用var声明的变量并不是全局的，而是属于当前模块下面的。

```js
var a = 100;
console.log(a); //100
global.a = 200;
console.log(a); //还是100
console.log(global.a); //200
```

```js
//一些看似全局的属于当前模块的变量

//__filename 当前文件被解析后的绝对路径；其实这个变量是属于当前模块的
console.log(__filename);
```

模块加载机制-require方法

```js
//require("模块路径");

//require('./2.js');
```

require方法中的路径可以填写相对路径和绝对路径

```js
//当前模块在硬盘当中的绝对路径
require('b:/录制视频/nodejs/课件/module/2.js');
//跟当前模块的相对路径
require('./2.js'); //在nodejs中千万不能写成 require('2.js') 因为它将会去加载node中的核心模块，或者是node_modules目录下的模块
```

模块的文件查找机制：

首先按照加载的模块文件名称进行查找 → 如果没有找到，会自动在模块文件名称后面加上.js 的后缀进行查找 → 如果还没有找到，则会在文件名称后加上 .json 的后缀进行查找 → 如果还没有找到，则会在文件名称后加上 .node 的后缀进行查找 → 
还没找到则弹出错误

在一个模块中通过var定义的变量，其作用域范围是当前模块，外部模块不能够直接访问。如果想一个模块能够访问另外一个模块中定义的变量，可以这么做：

- 方法1：把变量作为global对象的一个属性（这样的做法不推荐，应尽量减少对全局变量的定义）

```js
//当前模块为4
//在模块5中为global对象添加一个属性 global.a = 100;
require('./5');
console.log(a); //100
```

- 方法2：使用一个模块对象 module 对象（也是模块作用域下的，而不是全局的）

module保存并提供与当前模块相关的一些信息（可以用 console.log(module); 把它打出来）

在module对象中有一个子对象：exports。我们可以通过这个对象把一个模块中的局部变量对象进行对外提供访问

```js
//5模块
var a = 100;
module.exports.a = a;
```

```js
//4模块
//require('./5'); //返回值就是被加载模块当中的exports
var m5 = require('./5');
console.log(m5.a); //100
```

在模块作用域内，还有一个内置的模块对象——exports——它其实就是module.exports

```js
//5模块
var a = 100;

//console.log(module.exports === exports); //true
exports.a = a;
```

exports与module.exports指向相同，在使用的时候，尽量不要破坏两者的指向关系

```js
module.exports = [1, 2, 3]; //直接这样对module.exports进行操作，这时候exports和module.exports的指向关系已经断开了

exports.a = 200; //这时候这个a已经加不到module.exports中了，所以在其他模块中引用它也引用不到了，因为这个模块的返回值已经变成了[1, 2, 3]
```

##global对象

```js
//__filename：返回当前模块文件解析后的绝对路径，该属性并非全局，而是模块作用域下的
console.log(global.__filename); //undefined
console.log(__filename);

//__dirname：返回当前模块文件所在目录解析后的绝对路径，该属性也并非全局，而是模块作用域下的
console.log(__dirname);

var d = new Date();
var arr = new Array(1, 2, 3);

//命令行形式的时钟
setInterval(function(){
	var d = new Date();
	console.log('现在是：' + d.getFullYear() + '年' + (d.getMonth()+1) + '月' + d.getDate() + '日' + d.getHours() + " : " + d.getMinutes() + ' : ' + d.getSeconds());
}, 1000);
```

##process对象、输入输出流

```js
//process全局对象，通过这个对象提供的属性和方法，使我们可以对当前运行的程序的进程进行访问

console.log(process);
console.log(global.process);

//argv: - Array 一组包含命令行参数的数组，第一个元素是node，第二个元素是js文件的名称，接下来的元素依次是命令行传入的参数
//execPath: - 开启当前进程的绝对路径
//env: - 返回用户环境信息

console.log(process.argv);
console.log(process.env);

//version: - 返回版本信息
//versions: - 返回node以及node依赖包版本信息
//pid: - 当前进程的pid
//title: - 当前进程的显示名称（Getter/Setter）
//arch: - 返回当前CPU处理器框架 arm/ia32/x64
//platform: - 返回当前操作系统平台
//cwd(): - 返回当前进程的工作目录
//chdir(directory): - 改变当前进程的工作目录
//memoryUsage(): - 返回node进程的内存使用情况，单位是byte
//exit(code): - 退出
//kill(pid): - 向进程发送信息
```

```js
//process对象的stdin（标准输入流）和stdout（标准输出流）

process.stdout.write('hello');
function log(data){
	process.stdout.write(data);
}
log('你好');

//默认情况下，输入流是关闭的，要监听处理输入流数据，首先要开启输入流
process.stdin.resume();
//用于监听用户的输入数据
process.stdin.on('data', function(chunk){
	console.log('用户输入了: ' + chunk);
});

```

```js
process.stdin.resume();
var a;
var b;
process.stdout.write('请输入a的值：');
process.stdin.on('data', function(chunk){
	if (!a){
		a = Number(chunk);
		process.stdout.write('请输入b的值：');
	} else {
		b = Number(chunk);
		process.stdout.write('结果是：'+ (a + b));
	}
})
```

##Buffer

Buffer是全局对象，用于操作二进制数据流

- new Buffer(size); size [number] 创建一个Buffer对象，并为这个对象分配一个大小
- new Buffer(array);
- new Buffer(string, [encoding]);

```js
//当我们为一个Buffer对象分配空间大小之后，其长度是固定的，不能更改
var bf = new Buffer(5);
console.log(bf);
bf[6] = 10;
console.log(bf); //bf没有任何变化
bf[1] = 2;
console.log(bf); //bf的第二个位置上的字符会变成02
```

```js
var bf = new Buffer([1, 2, 3]);
console.log(bf);
bf[10] = 10;
console.log(bf); //bf也没有变化，因为bf的长度没有改变。bf只要初始化了，那么它的长度就是没有变化的
```

```js
var bf = new Buffer('miaov', 'utf-8');
console.log(bf);

for(var i=0; i<bf.length; i++){ //Buffer的length是字节长度，而不是字符长度
	//console.log(bf[i]);
	//console.log(bf[i].toString(16));
	console.log(String.fromCharCode(bf[i]));
}

var str1 = 'miaov';
var bf1 = new Buffer(str1);
console.log(str1.length); //5
console.log(bf1.length); //5

var str2 = '妙味';
var bf2 = new Buffer(str2);
console.log(str2.length); //2
console.log(bf2.length); //6
```

Buffer类
- buf.length: buffer的bytes大小
- buf[index]: 获取或者设置在指定index索引位置的8位字节内容
- buf.write(string, [offset], [length], [encoding]): 根据参数offset偏移量和指定的encoding编码方式，将参数string数据写入buffer
- buf.toString([encoding], [start], [end]): 根据encoding参数（默认是‘utf8’）返回一个解码的string类型
- buf.toJSON(): 返回一个JSON表示的Buffer实例。JSON.stringify将会默认调用来字符串序列化这个Buffer实例
- buf.slice([start], [end]): 返回一个新的buffer，这个buffer将和老的buffer引用相同的内存地址，注意：修改这个新的buffer实例slice切片，也会改变原来的buffer
- buf.copy(targetBuffer, [targetStart], [sourceStart], [sourceEnd]): 进行buffer的拷贝
```js
var str = 'miaov';
console.log(new Buffer(str));

var bf = new Buffer(5);

bf.write(str); 
console.log(bf);

bf.write(str, 1);
console.log(bf);

bf.write(str, 1, 3);
console.log(bf);
```

```js
var bf = new Buffer('miaov');
console.log(bf.toString()); //miaov
console.log(bf.toString('utf-8', 1, 3)); //ia 

var bf2 = new Buffer('妙味');
console.log(bf2);
console.log(bf2.toString('utf-8', 1)); //乱码

console.log(bf.toJSON()); //{type: 'Buffer', data: [109, 105, 97, 111, 118]}
```

```js
var bf = new Buffer('miaov');
var bf2 = bf.slice();
console.log(bf);
console.log(bf2);
var bf3 = bf.slice(2,4);
console.log(bf3);

bf3[0] = 2;
console.log(bf3); //第0位变成了02
console.log(bf); //bf相应位置也变成了02

var bf4 = new Buffer(10);
bf.copy(bf4);
console.log(bf4);
bf4[0] = 2;
console.log(bf4); //发生了改变
console.log(bf); //bf没有受到影响

var bf5 = new Buffer(10);
bf.copy(bf5, 1, 2, 4);
console.log(bf5);
```

Buffer的一些类方法（静态方法）

- Buffer.isEncoding(encoding): 如果给定的编码encoding是有效的，返回true，否则返回false
- Buffer.isBuffer(obj): 测试这个obj是否是一个Buffer
- Buffer.byteLength(string, [encoding]): 将会返回这个字符串真实byte长度。encoding编码默认是utf8。
- Buffer.concat(list, [totalLength]): 返回一个保存着将传入buffer数组中所有buffer对象拼接在一起的buffer对象

```js
console.log(Buffer.isEncoding('utf-8')); //true
console.log(Buffer.isEncoding('gbk')); //false
console.log(Buffer.isEncoding('hex')); //true

var arr = [1, 2, 3];
var bf = new Buffer(10);
console.log(Buffer.isBuffer(arr)); //false
console.log(Buffer.isBuffer(bf)); //true

var str1 = '妙味';
console.log(str1.length); //2
console.log(Buffer.byteLength(str1)); //6
console.log(Buffer.byteLength(str1, 'ascii')); //2
```

```js
var str1 = 'miaov';
var str2 = '妙味';
var list = [new Buffer(str1), new Buffer(str2)];
console.log(list); //list是一个字节数组
var bf = Buffer.concat(list, 11);
console.log(bf);
```

```js
process.stdout.write('请输入内容：');
process.stdin.resume();
process.stdin.on('data', function(chunk){
	console.log(chunk); //这个chunk其实是个buffer对象
	console.log(chunk.toString());
	console.log('输入的内容是：'+ chunk); //内部Buffer自动拼接为string，不需要手动显式地toString了
});
```

##FileSystem

File System - 文件系统模块 - require('fs')

该模块提供了操作文件的一些api

- fs.open(path, flags, [mode], callback) 异步版的打开一个文件
- fs.openSync(path, flags, [mode]) 这是fs.open()的同步版
- fs.read(fd, buffer, offset, length, position, callback) 从指定的文档标示符fd读取文件数据
- fs.readSync(fd, buffer, offset, length, position) 这是fs.read函数的同步版本。返回bytesRead的个数

```js
var fs = require('fs');
/*
 * fs.open(path, flags, [mode], callback)
 * path: 要打开文件的路径
 * flags: 打开文件的方式 读/写
 * mode: 设置文件的模式 读/写/执行 4/2/1
 * callback: 回调
 *     err: 文件打开失败的错误保存在err里面，如果成功，err为null
 *     fd: 被打开文件的标识，和定时器都点像
 */

fs.open('1.txt', 'r', function(err, fd){
	//console.log(err);
	//console.log(fd);

	if(err){
		console.log('文件打开失败');
	} else {
		console.log('文件打开成功');
		console.log(fd); 
	}
})

fs.open('1.txt', 'r', function(err,fd){
	console.log(fd); //会发现这个fd跟上面的不一样了，这个地方的fd累加了
})
```

```js
var fs = require('fs');

//异步方式处理
fs.open('1.txt', 'r', function(err, fd){
	console.log(fd);
})
console.log('ok');

//同步方式
var fd = fs.openSync('1.txt', 'r');
console.log(fd);
```

```js
var fs = require('fs');
fs.open('1.txt', 'r', function(err, fd){
	if (err){
		console.log('文件打开失败');
	} else {
		//读取文件
		/*
		 * fs.read(fd, buffer, offset, length, position, callback)
		 *   fd: 通过open方法成功打开一个文件返回的编号
		 *   buffer: buffer对象
		 *   offset: 偏移量，新的内容添加到buffer中的起始位置
		 *   length: 长度，添加到buffer中的内容的长度
		 *   position:位置，读取的文件中的起始位置
		 *   callback: 回调
		 *      err
		 *      buffer的长度
		 *      buffer
		 */
		var bf1 = new Buffer('123456789');
		console.log(bf1);
		fs.read(fd, bf1, 0, 4, null, function(err, len, newBf){
			console.log(bf1);
			console.log(len);
			console.log(newBf);
		});
	}
});
```

- fs.write(fd, buffer, offset, length[, position], callback) 通过文件标识fd，向指定的文件中写入buffer
- fs.write(fd, data[, position[, encoding]], callback) 把data写入到文档中，通过指定的fd，如果data不是buffer对象的实例，则会把值强制转化成一个字符串
- fs.writeSync(fd, buffer, offset, length[, position]) 这是fs.write()的同步版本
- fs.writeSynd(fd, data[, position[, encoding]]) 这是fs.write()的同步版本
- fs.close(fd, callback) 关闭一个打开的文件
- fs.closeSync(fd) 这是fs.close()的同步版本

```js
var fs = require('fs');

fs.open('1.txt', 'r+', function(err, fd){
	/*
	 * 当我们要对打开的文件进行写操作的时候，打开方式就不能是只读r，而是读写r+
	 * fs.write(fd, buffer, offset, length[, position], callback)
	 * fd: 打开的文件
	 * buffer: 要写入的数据
	 * offset: buffer对象中要写入的数据的起始位置
	 * length: 要写入的buffer数据的长度
	 * position: fd中的起始位置
	 * callback: 回调
	 */
	
	if (err){
		console.log('打开文件失败');
	} else {

		/*var bf = new Buffer('123');
		fs.write(fd, bf, 0, 3, 5, function(){
			console.log(arguments); //第一个参数是错误信息；第二个参数是写入的长度；第三个参数是写入的buffer信息
		});*/

		fs.write(fd, '1234', 5, 'utf-8');

		fs.close(fd, function(){

		});
	}
})
```

- fs.writeFile(filename, data, [options], callback) 异步的将数据写入一个文件，如果文件不存在则新建，如果文件原先存在，会被替换。data可以是一个string，也可以是一个原生buffer
- fs.writeFileSync(filename, data, [options]) 这是fs.writeFile的同步版本。注意：没有callback，也不需要
- fs.appendFile(filename, data, [options], callback) 异步的将数据添加到一个文件的尾部，如果文件不存在，会创建一个新的文件。data可以是一个string，也可以是原生buffer
- fs.appendFileSync(filename, data, [options]) 这是fs.appendFile的同步版本
- fs.readFile(filename, [options], callback) 异步读取一个文件的全部内容
- fs.readFileSync(filename, [options]) 这是fs.readFile的同步版本
- fs.exists(path, callback) 检查指定路径的文件或者目录是否存在
- fs.existsSync(path) 这是fs.exists的同步版本
- fs.unlink(path, callback) 删除一个文件
- fs.unlinkSync(path) 这是fs.unlink()的同步版本

```js
var fs = require('fs');
var filename = '2.txt';

/*fs.writeFile(filename, 'hello', function(err){
	console.log(arguments);
})*/

/*fs.appendFile(filename, '-leo', function(err){
	console.log(arguments);
})*/

/* 异步方式实现，代码很难看
fs.exists(filename, function(isExists){
	//console.log(isExists);

	if(!isExists){
		fs.writeFile(filename, 'miaov', function(err){
			if(err){
				console.log('出错了');
			} else {
				console.log('创建新文件成功');
			} else {
				fs.appendFile(filename, '-leo', function(err){
					if(err){
						console.log('新内容追加失败');
					} else {
						console.log('新内容追加成功');
					}
				})
			}
		})
	}
});
*/

//以下是同步模式的
if (!fs.existsSync(filename)){
	fs.writeFileSync(filename, 'miaov');
	console.log('新文件创建成功');
} else {
	fs.appendFileSync(filename, '-leo');
	console.log('新文件追加成功');
}

```

```js
var fs = require('fs');

fs.readFile('2.txt', function(err, data){
	//console.log(arguments);

	if(err){
		console.log('文件读取失败');
	} else {
		console.log(data.toString());
	}
})

fs.unlink('2.txt', function(err){
	if(err){
		console.log('删除失败');
	} else {
		console.log('删除成功');
	}
})
```

- fs.rename(oldPath, newPath, callback) 重命名
- fs.renameSync(oldPath, newPath) 这是fs.readname的同步版本
- fs.stat(path, callback) 读取文件信息
- fs.statSync(path, callback) 这是fs.stat()的同步版本
- fs.watch(filename, [options], [listener]) 观察指定路径的改变，filename路径可以是文件或者目录

```js
var fs = require('fs');
fs.rename('2.txt', '2.new.txt', function(err){
	console.log(arguments);
})

fs.stat('2.new.txt', function(err, stat){
	console.log(arguments)
})
```

```js
var fs = require('fs');

var filename = '2.new.txt';
fs.watch(filename, function(ev, fn){
	console.log(ev);
	if(fn){
		console.log(fn + '发生了改变');
	} else {
		console.log('...');
	}
})
```

- fs.mkdir(path, [mode], callback) 创建文件夹
- fs.mkdirSync(path, [mode]) 这是fs.mkdir的同步版本
- fs.readdir(path, callback) 读取文件夹
- fs.readdirSync(path) 这是fs.readdir的同步版本
- fs.rmdir(path, callback) 删除文件夹
- fs.rmdirSync(path) 这是fs.rmdir的同步版本

```js
var fs = require('fs');

fs.mkdir('./1', function(err){
	console.log(arguments);
});

fs.rmdir('./1', function(err){
	console.log(arguments);
})

fs.readdir('./', function(err, fileList){
	//console.log(fileList);
	fileList.forEach(function(f){
		fs.stat(f, function(err, info){
			//console.log(arguments);

			switch(info.mode){
				case 16822:
					console.log('[文件夹]' + f);
					break;
				case 33206:
					console.log('[文件]' + f);
					break;
				default:
					console.log('[其他类型]' + f);
					break;
			}
		});
	})
})
```

##前端项目自动化

完成一个简单的项目初始化过程

```js
var projectData = {
	'name': 'miaov',
	'fileData': [
		{
			'name': 'css',
			'type': 'dir'
		},
		{
			'name': 'js',
			'type': 'dir'
		},
		{
			'name': 'images',
			'type': 'dir'
		},
		{
			'name': 'index.html',
			'type': 'file',
			'content': '<html>\n\t<head>\n\t\t<title>title</title>\n\t</head>\n\t<body>\n\t\t<h1>Hello</h1>\n\t</body>\n</html>'
		},
	]	
};

var fs = require('fs');

if(projectData.name){
	fs.mkdirSync(projectData.name);

	var fileData = projectData.fileData;
	
	if(fileData && fileData.forEach){
		fileData.forEach(function(f){
			f.path = projectData.name + '/' + f.name;
			f.content = f.content || '';
				case 'dir':
					fs.mkdirSync(f.path);
					break;
				case 'file':
					fs.writeFileSync(f.path, f.content);
					break;
				default:
					break;
			}
		})
	}
}

```

自动合并

```js
var fs = require('fs');
var filedir = './miaov/source';

fs.watch(filedir, function(ev, file){
	//console.log(ev + '/' + file); //这里不需要判断file是否有内容，因为有可能是删除导致事件的发生

	//只要source文件夹中有一个文件发生了变化，我们就需要对这个文件夹下的所有文件进行读取，然后合并
	fs.readdir(filedir, function(err, dataList){
		var arr = [];
		dataList.forEach(function(f){
			if (f) {
				var info = fs.statSync(filedir + '/' + f);
				//console.log(info);

				if(info.mode == 33206){
					arr.push(filedir + '/' + f);
				}
			}
		})

		//console.log('arr');

		//读取数组中的文件内容，并合并

		var content = '';
		arr.forEach(function(f){
			var c = fs.readFileSync(f);
			//console.log(c);
			content += c.toString() + '\n';
		});

		console.log(content);
		fs.writeFile('./miaov/js/index.js', content);
	})
})
```


##使用node进行web开发

1. 用户通过浏览器发送一个http的请求指定的主机
2. 服务器接收到该请求，对该请求进行分析和处理
3. 服务器处理完成以后，返回对应的数据到用户机器
4. 浏览器接收服务器返回的数据，并根据接收的数据进行分析和处理

客户端  服务端

由客户端发送一个http请求到指定的服务器 → 服务端接收并处理请求 → 返回数据给客户端

http模块 - require('http')

- var http = require('http');
- var server = http.createServer([requestListener])
	- 创建并返回一个HTTP服务器对象
	- requestListener: 监听到客户端连接的回调函数
- server.listen(port, [hostname], [backlog], [callback])
	- 监听客户端连接请求，只有当调用了listen方法以后，服务器才开始工作
	- port: 监听的端口
	- hostname：主机名（IP/域名）
	- backlog：连接等待队列的最大长度
	- callback：调用listen方法并成功开启监听以后，会触发一个listening事件，callback将作为该事件的执行函数

```js
//搭建一个http服务器，用于处理用户发送的http请求

//加载一个http模块
var http = require('http');

//通过http模块下的createServer创建并返回一个web服务器对象
var server = http.createServer();

/*
server.on('error', function(err){
	console.log(err);
})
*/

server.on('listening', function(){
	console.log('listening...');
})

server.listen(52346, 'localhost');

//console.log(server.address());
```

- listening事件：当server调用listen方法并成功开始监听以后触发的事件
- error事件：当服务器开启失败的时候触发的事件
	- 参数err，具体的错误对象
- request事件：当有客户端发送请求到该主机和端口的请求时触发
	- 参数request：http.IncomingMessage的一个实例，通过它，我们可以获取这次请求的一些信息，比如头信息、数据等
	- 参数response：http.ServerResponse的一个实例，通过它，我们可以向该次请求的客户端输出返回响应

```js
var http = require('http');
var server = http.createServer();

server.on('listening', function(){
	console.log('listening...');
})

server.on('request', function(){
	//console.log('有客户端请求了');
})

server.listen(52346, 'localhost');
```

- 参数request对象 - http.IncomingMessage
	- httpVersion: 使用的http协议的版本
	- headers: 请求头信息中的数据
	- url: 请求的地址
	- method：请求方式
- 参数response对象 - http.ServerResponse
	- write(chunk, [encoding])：发送一个数据块到响应正文中
	- end([chunk], [encoding])：当所有的正文和头信息发送完成以后调用该方法告诉服务器数据已经全部发送完成了，这个方法在每次完成信息发送以后必须调用，并且是u自后调用
	- statusCode：该属性用来设置返回的状态码
	- setHeader(name, value)：设置返回头信息
	- writeHead(statusCode, [reasonPhrase], [headers])：这个方法只能在当前请求中使用一次，并且必须在response.end()之前调用


```js
var http = require('http');
var server = http.createServer();

server.on('listening', function(){
	console.log('listening...');
})

server.on('request', function(req, res){
	//console.log(req);

	//res.write('hello');

	res.setHeader('miaov', 'leo');

	res.writeHead(200, 'Nice Day', {
		//'content-type' : 'text/plain'
		'content-type' : 'text/html;charset=utf-8'
	});

	/*
	res.write('<h1>hello</h1>');
	res.end();
	*/

	res.end('<h1>hello</h1>');
})

server.listen(52346, 'localhost');
```

url处理：url模块

```js
var http = require('http');
var url = require('url');

var server = http.createServer();

server.on('request', function(req, res){
	//req.url：访问路径
	//?后面的部分 query string
	//console.log(req.url);

	var urlStr = url.parse(req.url);
	//console.log(urlStr);
	switch(urlStr.path){
		case '/':
			//首页
			res.writeHead(200, {
				'content-type': 'text/html;charset=utf-8'
			})
			res.end('<h1>这是首页</h1>')
			break;
		case '/user':
			//用户
			res.writeHead(200, {
				'content-type': 'text/html;charset=utf-8'
			})
			res.end('<h1>个人</h1>')
			break;
		default:
			//处理其他情况
			res.writeHead(404 {
				'content-type': 'text/html;charset=utf-8'
			})
			res.end('<h1>页面被吃掉了</h1>')
			break;
	}
});

server.listen(8080, 'localhost')
```

使用fs模块实现行为表现分离

```js
var http = require('http');
var url = require('url');
var fs = require('fs');

var server = http.createServer();

var HtmlDir = __dirname + '/html/';

server.on('request', function(req, res){
	var urlStr = url.parse(req.url);

	switch(urlStr.path){
		case '/':
			//首页
			sendData(HtmlDir + 'index.html', req, res);
			break;
		case '/user':
			//用户
			sendData(HtmlDir + 'user.html', req, res);
			break;
		default:
			//处理其他情况
			sendData(HtmlDir + 'err.html', req, res);
			break;
	}
});

function sendData(file, req, res){
	fs.readFile(file, function(err, data){
		if(err){
			res.writeHead(404, {
				'content-type' : 'text/html;charset=utf-8'
			});
			res.end('<h1>页面找不到</h1>')
		} else {
			res.writeHead(200, {
				'content-type' : 'text/html;charset=utf-8'
			});
			res.end(data)
		}
	})
}

server.listen(8080, 'localhost');
```

使用querystring模块方法对get和post提交的数据进行处理

query string是url中的query属性，代表的是url中问号后面的东西

- url模块 - require('url')
	- .parse(request.url)：对url格式的字符串进行解析，返回一个对象
	- 根据不同的url进行处理，返回不一样的数据
	- 使用fs模块实现nodejs代码和html的分离
	- get请求的数据处理
	- post请求的数据处理
		- post发送的数据会被写入缓冲区中，需要通过request的data事件和end事件来进行数据拼接处理
	- querystring模块
		- .parse()：将一个query string反序列化为一个对象

```js
var http = require('http');
var url = require('url');
var fs = require('fs');
var querystring = require('querystring');

var server = http.createServer();

var HtmlDir = __dirname + '/html/';

server.on('request', function(req, res){
	var urlStr = url.parse(req.url);

	switch(urlStr.path){
		case '/':
			//首页
			sendData(HtmlDir + 'index.html', req, res);
			break;
		case '/user':
			//用户

			//get方式可以直接得到
			//console.log(querystring.parse(urlStr.query))
			
			//post方式要用req的data和end事件
			if(req.method.toUpperCase() == 'POST'){
				var str = '';
				req.on('data', function(chunk){
					str += chunk;
				})

				req.on('end', function(){
					//console.log(str);
					console.log(querystring.parse(str));
				})
			}

			sendData(HtmlDir + 'user.html', req, res);
			break;
		default:
			//处理其他情况
			sendData(HtmlDir + 'err.html', req, res);
			break;
	}
});

function sendData(file, req, res){
	fs.readFile(file, function(err, data){
		if(err){
			res.writeHead(404, {
				'content-type' : 'text/html;charset=utf-8'
			});
			res.end('<h1>页面找不到</h1>')
		} else {
			res.writeHead(200, {
				'content-type' : 'text/html;charset=utf-8'
			});
			res.end(data)
		}
	})
}

server.listen(8080, 'localhost');
```
