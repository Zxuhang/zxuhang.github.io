---
title: Taro
date: 2019-12-17 11:33:23
tags: React
categories: React
---
使用Taro，我们可以只书写一套代码，再通过 Taro 的编译工具，将源代码分别编译出可以在不同端（微信/百度/支付宝/字节跳动/QQ小程序、快应用、H5、React-Native 等）运行的代码
<!--more-->
	遇到的问题
	1  Taro.request()跨域问题 h5 发请求会报跨域问题，需要使用代理转换请求 
```bash
			//例子：config/index.js 
	
				//h5：添加
				devServer: {
			        host: 'localhost',
			        port: 10086,
			        proxy: {
			            '/api': {
			                target: 'http://tujia.diandou.com',  // 服务端地址
			                changeOrigin: true
			            }
			        }
			    }
			    //请求：
				Taro.request({
			        url: '/api/ouse',
			        data: {
			            user_id: '1'
			        },
			        method:'GET',
			        mode:'no-cors', 
			        header: {
			          'content-type': 'application/json'
			        },
			        success(res){}
			    }）
```