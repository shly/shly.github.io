---
title: javascript 中的this
date: 2016-07-17 15:42:30
tags: 
  - javascript
  - this
categories:
  - 学习笔记
  - 前端学习
---
javascript中的this始终指向当前运行的函数所属的对象
一 普通的函数调用中this

	 var x=1;
		function test(){
			alert(this.x);
		}
		test();
当前函数的所属对象是window对象，故this指向window对象
二 当this作为对象的方法被调用时，指向调用该方法的对象。
三 当函数作为构造函数被调用时，this指向由该构造函数创建的对象
四 call和apply可以改变this的指向，使this指向call或apply的第一个参数所代表的对象