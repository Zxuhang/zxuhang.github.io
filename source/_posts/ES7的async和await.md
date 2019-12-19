---
title: ES7的async和await
date: 2019-12-17 11:51:47
tags: 
- 异步
- ES7
categories: ES7
---
	async是让方法变成异步 返回Promise对象
	await等待async方法执行完毕 也可以接受普通方法和promise对象
<!--more-->
```bash
	function getSomething(){
	    return 'something';
	}
	 
	async function testAsync(){
	    return 'Hello async';
	}
	 
	async function test(){

		//await 因为会阻塞所以函数必须在async 函数体内使用

	    const v1=await getSomething();	//等待异步async getSomething完成在执行
	    const v2=await testAsync();
	    console.log(v1,v2);				//something,Hello async
	}	 
	test();
	
	//await接受promise对象
	function takeLongTime() {
	    return new Promise(resolve => {
	        setTimeout(() => resolve("long_time_value"), 1000);
	    });
	}
	 
	async function test() {
	    const v = await takeLongTime();
	    console.log(v);			//long_time_value
	}
	 
	test();
```