---
title: Angular路由ng-controller中as的作用
date: 2018-03-15 17:35:34
tags: [AngularJS,route]
categories: AngularJS
---
## 作用域
> $scope 会从父级controller创建的作用域进行原型继承，但又不会被覆盖,如下;

``` javascript
	function firstCtrl($scope){
		$scope.value = "123456";
	}；
	function secondCtrl($scope){
		$scope.value = "654321"；
	}
```
``` html
	<div ng-controller = "firstCtrl">
		{{value}}
		<div ng-controller = "secondCtrl">
			{{value}}
		</div>
	</div>
```
显示结果：
``` html
	<div ng-controller = "firstCtrl">
		123456
		<div ng-controller = "secondCtrl">
			654321
		</div>
	</div>
```
当secondCtrl中$scope.value被注释后：
``` javascript
	function firstCtrl($scope){
		$scope.value = "123456";
	}；
	function secondCtrl($scope){
		// $scope.value = "654321"；
	}
```
``` html
	<div ng-controller = "firstCtrl">
		123456
		<div ng-controller = "secondCtrl">
			123456
		</div>
	</div>
```
> 在secondCtrl中没有定义value，但是会继承firstCtrl中的 value 显示“123456”；
> 进行原型继承即意味着父作用域在子作用域的原型链上，这是JavaScript的特性；
> 所以在angular 1.2以后有了controller as；

``` html
	<div ng-controller = "firstCtrl as first">
		{{first.value}}
		<div ng-controller = "secondCtrl as second">
			{{second.value}}
		</div>
	</div>
```