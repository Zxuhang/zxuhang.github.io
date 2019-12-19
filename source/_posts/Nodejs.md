---
title: Nodejs
date: 2019-12-12 16:35:07
tags: nodejs
---
#一些nodejs知识
	基于 Chrome V8 引擎的 JavaScript 运行环境
	特点：单线程 异步非阻塞I/O 事件驱动 
	适合处理I/O不适合大量计算 容易阻塞
<!--more-->
	服务器 	npm install http-server -g  

	关于npm错误  ---->	npm ERR! Cannot read property 'resolve' of undefined

						npm ERR! A complete log of this run can be found in:

						解决方法：卸载nodejs 并清空nodejs安装目录所以文件从新安装

	事件
		var events = require('events');//事件模块
		//var util = require('util');//工具库

		//var Person = function(name) {
		//    this.name = name
		//}

		//util.inherits(Person, events.EventEmitter);//工具库里的继承  可用es6类class代替

		var myEmitter = new events.EventEmitter();//注册事件对象

		myEmitter.on('someEvent',function(msg){//绑定事件
			console.log(msg)
		})

		myEmitter.emit('someEvent','holl world!')//触发事件
		

	读文件   
		fs.readFile('路径','utf8',callback(err,data){})  //异步
		var a = fs.readFileSync('路径','utf8')  //同步
	写文件
		fs.writeFile('路径','内容',callback)  //异步
		fs.writeFileSync('路径','内容','utf8')  //同步
	创建目录
		fs.mkdir('目录名称', callback)
	删除目录&文件
		fs.unlink("删除", callback)

	流 和 管道（输入输出ye是流 ）

	//流可以是可读的、可写的、或者可读可写的。 所有的流都是 EventEmitter 的实例

		// 流和管道
		var fs = require('fs');

		var myReadStream = fs.createReadStream(__dirname + '/readMe.txt');//创建可读流
		var myWriteStream = fs.createWriteStream(__dirname + '/writeMe.txt');//创建可写流
		myReadStream.pipe(myWriteStream);

		var writeData = "hello world";
		myWriteStream.write(writeData);
		myWriteStream.end();
		myWriteStream.on('finish', function() {
		    console.log('finished');
		})

		myReadStream.setEncoding('utf8');

		var data = ""

		myReadStream.on('data', function(chunk) {
		    // data += chunk;
		    myWriteStream.write(chunk);
		})

		myReadStream.on('end', function() {
		    // console.log(data);
		})

		// 压缩 
		var crypto = require('crypto');
		var fs = require('fs');
		var zlib = require('zlib');

		var password = new Buffer(process.env.PASS || 'password');
		var encryptStream = crypto.createCipher('aes-256-cbc', password);

		var gzip = zlib.createGzip();
		var readStream = fs.createReadStream(__dirname + "/readMe.txt"); // current file
		var writeStream = fs.createWriteStream(__dirname + '/out.gz');

		readStream // reads current file
		    .pipe(encryptStream) // encrypts
		    .pipe(gzip) // compresses
		    .pipe(writeStream) // writes to out file
		    .on('finish', function() { // all done
		        console.log('done');
		    });
		// 解压
		var crypto = require('crypto');
		var fs = require('fs');
		var zlib = require('zlib');

		var password = new Buffer(process.env.PASS || 'password');
		var decryptStream = crypto.createDecipher('aes-256-cbc', password);

		var gzip = zlib.createGunzip();
		var readStream = fs.createReadStream(__dirname + '/out.gz');

		readStream // reads current file
		    .pipe(gzip) // uncompresses
		    .pipe(decryptStream) // decrypts
		    .pipe(process.stdout) // writes to terminal
		    .on('finish', function() { // finished
		        console.log('done');
		    });
