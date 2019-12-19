---
title: ES6的Promise和import
date: 2019-12-17 11:38:56
tags: 
- ES6
- Promise
- 异步
categories: ES6
---
#ES6的Promise 和 import
	获取异步数据，摆脱无限回调地狱
	是异步编程的一种解决方案
	<!--more-->
	从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。
	Promise 异步操作有三种状态：pending（进行中）、fulfilled（已成功）和 rejected（已失败）。除了异步操作的结果，任何其他操作都无法改变这个状态。

	Promise 对象只有：从 pending 变为 fulfilled 和从 pending 变为 rejected 的状态改变。只要处于 fulfilled 和 rejected ，状态就不会再变了即 resolved（已定型）。

	###回调函数处理异步
	```bash
	function callback() {
		var timeOut = Math.random * 2;//生成一个0-2之间的随机数，如果小于1，打印成功，否失败
		if(timeOut<1){
			console.log('成功');
		}else{
			console.log('失败');
		}
		
	}
	console.log('before setTimeout()');
	setTimeout(callback, 1000); // 1秒钟后调用callback函数
	console.log('after setTimeout()')
	```
	###promise处理异步
	```bash
	var printNum = new Promise(function(resolve,reject){//成功resolve 失败reject
		setTimeout(function(){
			var timeOut = Math.random * 2;//生成一个0-2之间的随机数，如果小于1，打印成功，否失败
			if(timeOut<1){
				resolve('成功');
			}else{
				reject('失败');
			}
		},100)
	})

	printNum.then(function(result){//成功调用 result结果
		console.log(result)
	})
	.catch(function(result){//失败调用 result结果
		console.log(result)
	})
	```
	###promise对象串联
	Promise还可以做更多的事情，比如，有若干个异步任务，需要先做任务1，如果成功后再做任务2，任何任务失败则不再继续并执行错误处理函数。
	job1.then(job2).then(job3).catch(handleError);//job1、job2和job3都是Promise对象。

	###Promise.all 
	方法返回一个 Promise 实例，此实例在参数内所有的 promise 都“完成（resolved）”或参数中不包含 promise 时回调完成（resolve）；
	如果参数中  promise 有一个失败（rejected），此实例回调失败（reject），失败原因的是第一个失败 promise 的结果。
	Promise.all([promise1,promise2...]).then((values)=>{}) 
	
	
#关于import 引入模块

	如果引用相对路径，则直接寻找这个相对路径文件 export 出来的内容。

	如果是绝对路径，则会依次寻找 node_modules 对应的地方。

	如果路径最终是一个文件夹，则会首先观察文件夹下是否有 package.json ,如果有 package.json 则会去加载 main 字段指向的文件，如果没有 package.json ，则会在这个文件夹下寻找 index 文件并加载。