---
title: Cookie的添加、获取、删除
date: 2018-03-12 15:54:46
tags: [JavaScript,Cookie]
categories: JavaScript
---
> 常用的会话跟踪技术是Cookie与Session。
> Cookie是客户端保存用户信息的一种机制，用来记录用户的一些信息，服务器端可以对其进行处理;
> session是存在服务器的,用于区分会话和不同用户的访问
## 设置Cookie
``` javascript
	function SetCookie(name,value,expires){	//cookie的名字、值、存储时间
		var Days = expires? expires :30; 
		//此 cookie 将被保存 expires(调用时自定义保存天数) 或者30 天
		var exp  = new Date();    //new Date("December 31, 9998");
		exp.setTime(exp.getTime() + Days*24*60*60*1000);
		document.cookie = name + "="+ escape (value) + ";expires=" + exp.toGMTString();
	}
```
## 获取Cookie
``` javascript
	function getCookie(name){	//取cookies函数        
		var arr = document.cookie.match(new RegExp("(^| )"+name+"=([^;]*)(;|$)"));
	 	if(arr != null) return unescape(arr[2]); return null;
	}
```
## 删除Cookie
``` javascript
	function delCookie(name){	//删除cookie
		var exp = new Date();
		exp.setTime(exp.getTime() - 1);
		var cval=getCookie(name);
		if(cval!=null) document.cookie= name + "="+cval+";expires="+exp.toGMTString();
	}
```
## 具体用法
``` javascript
SetCookie('UserName','Admin',30);
getCookie('UserName');
delCookie('UserName');
```