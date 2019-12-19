---
title: Vue安装总结
date: 2019-12-17 11:46:53
tags: Vue
categories: Vue
---
vue cli 环境搭建
<!--more-->
	1.必须安装nodejs 使用node中的npm包管理工具下载vue-cli
		1.安装完nodejs后可下载国内cnpm淘宝镜像

	2.新建项目文件夹 打开cmd cd到刚新建项目文件夹中 （cd..返回上一层目录）
		例如：d盘下新建了一个vue1文件夹输入cmd中输入以下命令
		C:\Users\Administrator>d: //进入d盘
		D:\>cd vue1 //进入项目文件夹

	

	3.D:\vue1>cnpm install vue-cli -g //安装vue-cli
	
	4.D:\vue1>vue init <template-name> <project-name> //表示我要用vue-cli来初始化项目
		
		<template-name>：表示模板名称，vue-cli官方为我们提供了5种模板，

				webpack - 全面的webpack+vue-loader的模板，功能包括热加载，linting,检测和CSS扩展。

				webpack - simple 简单webpack+vue-loader的模板，不含其他功能，快速的搭建vue的开发环境。

				browserify - 全面的Browserify+vueify 的模板，功能包括热加载，linting,单元检测。

				browserify - simple - 简单Browserify+vueify的模板，不包含其他功能，让你快速的搭建vue的开发环境。

				simple - 最简单的单页应用模板。
		
		<project-name>：标识项目名称

	5.D:\vue1>npm install  //安装项目依赖包，也就是安装package.json里的包

	6.npm run dev //运行程序