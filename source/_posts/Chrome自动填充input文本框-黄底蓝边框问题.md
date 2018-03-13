---
title: Chrome自动填充input文本框,黄底蓝边框问题
date: 2018-03-09 13:48:49
tags: [Chrome,CSS]
categories: CSS
---
#### 谷歌浏览器（Chrome）在开启自动填充账号密码功能时，input文本框会变成黄色背景，获取焦点时，变成蓝色边框，如下图：
> <img src="https://s1.ax1x.com/2018/03/09/9RihjA.png" alt="9RihjA.png" border="0" />
#### 这个背景是Chrome强制加的样式（-webkit-autofill）：
> <img src="https://s1.ax1x.com/2018/03/09/9Rijjs.png" alt="9Rijjs.png" border="0" />
#### 蓝色边框其实不是边框，是outline；
> outline （轮廓）是绘制于元素周围的一条线，位于边框边缘的外围，可起到突出元素的作用。
#### 取消黄色背景？
这个背景已经是加了!important，CSS样式处于最高优先级，所以替换是不可能的；
可以用阴影（box-shadow）来覆盖这个效果。
``` css
.loginInput:-webkit-autofill {
	-webkit-box-shadow: 0 0 0px 1000px white inset!important;
}
```
效果如下：
> <img src="https://s1.ax1x.com/2018/03/09/9RkQZq.png" alt="9RkQZq.png" border="0" />
不过你也可以按自己的喜好，将white换成其他颜色。
#### 取消蓝色边框
outline直接设置获取焦点是为 0 或 none 就可以取消蓝色的轮廓了。
``` css
.loginInput:focus{
    outline: 0;
}
```