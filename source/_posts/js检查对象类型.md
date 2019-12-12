---
title: js检查对象类型
date: 2019-12-12 11:05:16
tags: js
categories: JavaScript
---
# js检查对象类型
<!--more-->
```bash
hasOwnProperty 此方法无法检查该对象的原型链中是否具有该属性
	object.hasOwnProperty(proName)

constructor 属性返回对创建此对象的数组函数的引用 属性值是指向创建当前实例的对象的	
	[].constructor == Array //true
	Object.constructor == Object //false
	原型链被改变会报错
		var arr = [];
		arr.__proto__ = String
		arr.constructor == Array //false

instanceof 检测这个实例对象是不是这个方法new出来的
	[] instanceof Array //true
	Number instanceof Number //false
	String instanceof String //false
	Object instanceof Object //true
	Function instanceof Function //true
	Function instanceof Object //true
	function Foo(){}
	Foo instanceof Function //true
	Foo instanceof Foo //false
	原型链改变会报错
		var arr = []
		arr.__proto__ = String
		arr instanceof Array //false

typeof 用于检测基本类型
	typeof undefined;//=> undefined
	typeof 'a';//=> string
	typeof 1;//=> number
	typeof true;//=> boolean
	typeof {};//=> object
	typeof [];//=> object
	typeof function() {};//=> function
	typeof null;//=> object


```