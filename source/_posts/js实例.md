---
title: JavaScript一些知识点实例
date: 2016-12-01 11:21:51
tags: JavaScript
categories: JavaScript
---
# JavaScript一些知识点实例
<!--more-->

## 原型链与继承
```bash

 //基类 原型链 继承
function Person(name,age){//人类 基类
	this.name = name;
	this.age = age;
}

Person.prototype.hi = function(){
	console.log('hi my name is'+this.name+'my age is'+this.age);
}

Person.prototype.LEGS_NUM = 2;
Person.prototype.ARMS_NUM = 2;
Person.prototype.walk = function(){
	console.log(this.name+'is walking..');
}

//工人 构造函数
function Worker(name,age,workerNum){
	//Worker对象执行Person函数
	Person.call(this,name,age);
	this.workerNum = workerNum;
}
//这样继承会造成基类原型中的方法和构造函数原型的方法同名时 基类原型方法会被改变
Worker.prototype = Person.prototype;

Worker.prototype.say = function(){
	console.log(this.name+'say:我是工人')
}



function Student(name,age,className){//学生 构造函数
	Person.call(this,name,age);//Student对象执行Person函数
	this.className = className;
}
// Student.prototype = Person.prototype;//这样继承会造成基类原型被改变
//新建一个空对象复制基类 然后原型在被继承
Student.prototype = Object.create(Person.prototype);
Student.prototype.constructor = Student;
Student.prototype.hi = function(){
	console.log(this.name+'say:"hello"');
}

var xh = new Person('小红',11);
var xq = new Worker('小强',30,120);
var xm = new Student('小明',12,'001');


console.log(Student.prototype.constructor)
xm.hi();
xh.hi();
// xq.hi();
alert(xm.LEGS_NUM)

	
```
## 关于事件委托
```bash
//事件委托 dom结构：#a(#b,#c),只给父级节点绑定事件通过事件冒泡委托给子级元素
var aDiv = document.getElementById('a');

function addEvent(ele,type,callback){
	if(ele.addEventListener){
		//默认false(true事件捕获，false事件冒泡)
		ele.addEventListener(type,callback,false);
		
	}else if(ele.attachEvent){//ie浏览器只支持事件冒泡
	
		ele.attachEvent('on'+type,callback);
	}
}

function handler(e){
	var e = e || window.event;

	console.log(e.target.id);
	switch(e.target.id){
		case 'b':
		alert('hi');
		break;
		case 'c':
		alert('hello');
		break;
	}
	alert('word')
}

addEvent(aDiv,'click',handler);
```
##获取url传的参数
```bash

function getRequest() {   //获取url传的参数
		//获取url中"?"符后的字串
       var url = window.location.search;    
       var theRequest = new Object();   
       if (url.indexOf("?") != -1) {   
          var str = url.substr(1);   
          var strs = str.split("&");   
          for(var i = 0; i < strs.length; i ++) {   
              //就是这句的问题
             theRequest[strs[i].split("=")[0]]=decodeURI(strs[i].split("=")[1]); 
             //之前用了unescape()会出现乱码  
          }   
       }   
       return theRequest;   
    }

var Request = getRequest()

```
##数字效果
```bash
	//数字的效果慢慢变大
function numAnimation(id){ 
	var num = $(id).html();
	var time = 50;
	var i = 0;
	var f = num - parseInt(num);
	var fn = f/20;
	var n = parseInt(num / 20);
	myTime(time)
	function myTime(time){
	  setTimeout(function(){
		  i = i + n;
		  f = f + fn;
		  // debugger
		  if(i < num - n){
			if(i > n*10){
			  time = 80
			}
			if(i > n*15){
			  time = 130
			}
			if(f == 0){
			  $(id).html(i+'.00')
			}else{
			  $(id).html(i+Number(f.toFixed(2)))
			}
			myTime(time)
		  }else{
			$(id).html(num)
		  }
	  },time)
	}
		}

```
##表单验证
```bash

function verification(pattern,value){//表单验证
	switch(pattern)
		  {
			case 'required': pattern = /\S+/i;break;//必填
			case 'email': pattern = /^\w+([-+.]\w+)*@\w+([-.]\w+)+$/i;break;//邮箱
			case 'qq':  pattern = /^[1-9][0-9]{4,}$/i;break;//qq
			case 'id': pattern = /^\d{15}(\d{2}[0-9x])?$/i;break;//身份证
			case 'ip': pattern = /^(([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])\.){3}([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])$/i;break;//IP地址
			case 'zip': pattern = /^\d{6}$/i;break;
			case 'mobi': pattern = /^1[3|4|5|7|8][0-9]\d{8}$/;break;//手机号
			case 'phone': pattern = /^((\d{3,4})|\d{3,4}-)?\d{3,8}(-\d+)*$/i;break;//电话
			case 'url': pattern = /^[a-zA-z]+:\/\/(\w+(-\w+)*)(\.(\w+(-\w+)*))+(\/?\S*)?$/i;break;//网址
			case 'date': pattern = /^(?:(?!0000)[0-9]{4}-(?:(?:0[1-9]|1[0-2])-(?:0[1-9]|1[0-9]|2[0-8])|(?:0[13-9]|1[0-2])-(?:29|30)|(?:0[13578]|1[02])-31)|(?:[0-9]{2}(?:0[48]|[2468][048]|[13579][26])|(?:0[48]|[2468][048]|[13579][26])00)-02-29)$/i;break;//日期
			case 'datetime': pattern = /^(?:(?!0000)[0-9]{4}-(?:(?:0[1-9]|1[0-2])-(?:0[1-9]|1[0-9]|2[0-8])|(?:0[13-9]|1[0-2])-(?:29|30)|(?:0[13578]|1[02])-31)|(?:[0-9]{2}(?:0[48]|[2468][048]|[13579][26])|(?:0[48]|[2468][048]|[13579][26])00)-02-29) (?:(?:[0-1][0-9])|(?:2[0-3])):(?:[0-5][0-9]):(?:[0-5][0-9])$/i;break;//日期和时间
			case 'int': pattern = /^\d+$/i;break;//整形
			case 'float': pattern = /^\d+\.?\d*$/i;break;//浮点数
			case 'percent': pattern = /^[1-9][0-9]*$/;break;//百分数
		  }
	pattern = new RegExp(pattern)
	return pattern.test(value) 
	}

```
## 回到顶部
```bash
	function scroll_up(Obj){//回到顶部
		var a,b,c,$jsObj;
			if(Obj.length){
				$jsObj = Obj[0];
				a = Obj.scrollTop();//滚动条y轴上的距离
				b = $jsObj.clientHeight || document.body.clientHeight;//可视区域的高度
				c = $jsObj.scrollHeight || document.body.scrollHeight;//可视化的高度与溢出的距离（总高度）
			}else{
				$jsObj = this;
				a = document.documentElement.scrollTop || Obj.scrollTop;//滚动条y轴上的距离
				b = document.documentElement.clientHeight || Obj.clientHeight;//可视区域的高度
				c = document.documentElement.scrollHeight || Obj.scrollHeight;//可视化的高度与溢出的距离（总高度）
			}
			var c2 = c/2;

			if(a+b >= c2 && c2 >= b){
				if(document.getElementById('back_top') == null){
					var oDiv = document.createElement('div');
					oDiv.style.width = '40px';
					oDiv.style.height = '40px';
					oDiv.style.borderRadius = '40px';
					oDiv.style.background = 'url({skin:imgs/back_top1.png}) no-repeat 0';
					oDiv.style.backgroundSize = '40px';
					oDiv.style.position = 'fixed';
					oDiv.style.zIndex = 9999;
					oDiv.style.right = '5px';
					oDiv.style.bottom = '80px';
					document.body.appendChild(oDiv);
					var back_top = document.createAttribute('id');
					back_top.nodeValue = 'back_top';
					oDiv.setAttributeNode(back_top)
					oDiv.onclick = function(){
						scrollAnimation(a)
					}
				}else{
					document.getElementById('back_top').style.display = 'block';
				}
			}else if(a+b <= c2 && document.getElementById('back_top') != null){
				document.getElementById('back_top').style.display = 'none';
			}

			function scrollAnimation(a){
				myTimeout()
				// debugger
				function myTimeout(){
					a = parseInt(a - a/10);
					if(parseInt(a/2) >= 4 ){
						$jsObj.scrollTo(0,a)
						setTimeout(myTimeout,10)
					}else{
						$jsObj.scrollTo(0,0)
					}
				}

				
			}
	}
```
## ajax上传文件
``` bash

	// 获取文件
	
	function addFile() {
	   document.getElementById('test1').value = "";
	   var file = document.querySelector('input[type=file]').files[0];//IE10以下不支持
	   var typeStr="image/jpg,image/png,image/gif,image/jpeg";
	   if(typeStr.indexOf(file.type)>=0){
		  document.getElementById('test1').value = file.name;
		  if (file.size > 2097152) {
				alert("上传的文件不能大于2M");
			 return;
		  }else{

	 　　　　upload(path,file)
	　　　　}
	   }else{
		  alert("请上传格式为jpg、png、gif、jpeg的图片");
	   }
	}

	//上传文件
	function upload(path,theFormFile) {

		var fd = new FormData();//使用FormData必须使用form标签

		fd.append('file1', theFormFile);//上传的文件： 键名，键值
		var url = path;//接口
		url = url ? url : '';
		var XHR = null;
		if (window.XMLHttpRequest) {
			// 非IE内核
			XHR = new XMLHttpRequest();
		} else if (window.ActiveXObject) {
			// IE内核，这里早期IE版本不同，具体可以查下
			XHR = new ActiveXObject("Microsoft.XMLHTTP");
		} else {
			XHR = null;
		}
		if (XHR) {
			XHR.open("POST", url);
			XHR.onreadystatechange = function() {
				if (XHR.readyState == 4 && XHR.status == 200) {
					var resultValue = XHR.responseText;
					var data = JSON.parse(resultValue);
					XHR = null;
				}
			}
			XHR.send(fd);
		}
	};
	
```
##上传图片时为图片添加预览图
```bash
jQuery.fn.extend({//上传图片时为图片添加预览图
	uploadPreview: function (opts) {
		var _self = this,//原生file对象
			_this = $(this);//jq file对象
		opts = jQuery.extend({//img对象
			Img: "zz_i",
			Width: 100,
			Height: 100,
			ImgType: ["gif", "jpeg", "jpg", "bmp", "png"],
			Callback: function () {}
		}, opts || {});
		_self.getObjectURL = function (file) {
			var url = null;
			if (window.createObjectURL != undefined) {
				url = window.createObjectURL(file)
			} else if (window.URL != undefined) {
				url = window.URL.createObjectURL(file)
			} else if (window.webkitURL != undefined) {
				url = window.webkitURL.createObjectURL(file)
			}
			return url
		};
		
		_this.change(function () {
			if (this.value) {
				if (!RegExp("\.(" + opts.ImgType.join("|") + ")$", "i").test(this.value.toLowerCase())) {
					alert("选择文件错误,图片类型必须是" + opts.ImgType.join("，") + "中的一种");
					this.value = "";
					return false
				}
				if ($.support.msie) {
					debugger
					try {
						$("#" + opts.Img).attr('src', _self.getObjectURL(this.files[0]))
					} catch (e) {
						var src = "";
						var obj = $("#" + opts.Img);
						var div = obj.parent("div")[0];
						_self.select();
						if (top != self) {
							window.parent.document.body.focus()
						} else {
							_self.blur()
						}
						src = document.selection.createRange().text;
						document.selection.empty();
						obj.hide();
						obj.parent("div").css({
							'filter': 'progid:DXImageTransform.Microsoft.AlphaImageLoader(sizingMethod=scale)',
							'width': opts.Width + 'px',
							'height': opts.Height + 'px'
						});
						div.filters.item("DXImageTransform.Microsoft.AlphaImageLoader").src = src
					}
				} else {
					$("#" + opts.Img).attr('src', _self.getObjectURL(this.files[0]))
				}
				opts.Callback()
			}
		})
	}
});

$(file的id).uploadPreview({ Img: 图片的id , Width: 120, Height: 120 });


```