---
title: 简单搭建一个Node本地服务器
date: 2018-03-09 10:59:36
tags: [NodeJS]
categories: NodeJS
---
用node搭建一个简单的本地http服务器很容易，功能相当于apache服务器；
## 1.首先安装nodejs服务
（上篇文章有详细介绍，可移步查看）；

## 2.创建一个新目录，并新建 server.js
（我在E:\wwwroot\NodeServer下创建了server.js文件）；
<img src="https://s1.ax1x.com/2018/03/09/92veBD.png" alt="92veBD.png" border="0" />
### 在 server.js 中写入如下代码：
``` javascript
var http=require('http');
//开启服务
var server=http.createServer(function(req,res){
    console.log('有客户端连接');//创建连接成功显示在后台
    res.writeHeader(200,{
        'content-type' : 'text/html;charset="utf-8"'
    });
    res.write('这是正文部分');//显示给客户端
    res.end();
}).listen(8888);
console.log('服务器开启成功');
```
---------------------
这样，一个简单的node服务器就搭建完成了；
Win + R 打开运行 输入 cmd 打开命令行工具，
<img src="https://s1.ax1x.com/2018/03/09/92Xlad.png" alt="92Xlad.png" border="0" />
## 3.在cmd控制台中cd切换进server.js所在的目录，然后执行node server.js命令 
<img src="https://s1.ax1x.com/2018/03/09/92vrvV.png" alt="92vrvV.png" border="0" />
当提示“服务器开启成功”时，在浏览器端输入127.0.0.1:8888；
显示“这是正文内容”；
## 4.进阶-添加 index.html

### 修改 server.js 中代码：（记得将 root 路径改为自己的文件路径）
``` javascript
var http=require('http');
var fs=require('fs'); //引入文件读取模块
var root="E:/wwwroot/NodeServer/" //本地文件夹路径
//开启服务，监听8888端口
var server=http.createServer(function(req,res){
    console.log('有客户端连接'); //创建连接成功显示在后台
	var url=req.url;
	 	var file = root+url;
	fs.readFile(file,function(err,data){
    	if(err){
       	 res.writeHeader(404,{
        	    'content-type' : 'text/html;charset="utf-8"'
        	});
       		res.write('<h1>404错误</h1><p>你要找的页面不存在</p>');
        	res.end();
    	}else{
        	res.writeHeader(200,{
            	'content-type' : 'text/html;charset="utf-8"'
        	});
        	res.write(data); //将index.html显示在客户端
        	res.end();
    	}
	})
}).listen(8888);
console.log('服务器开启成功');
```
在该文件夹下再建一个 index.html，内容为“hello world”；
然后以刚才的方式，命令行运行 node server.js；
浏览器 输入 http://localhost:8888/index.html 即可看见 “hello world”；
<img src="https://s1.ax1x.com/2018/03/09/92xjwF.png" alt="92xjwF.png" border="0" />
一个node服务器搭建完成。

