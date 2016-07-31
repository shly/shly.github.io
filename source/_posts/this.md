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
javascript中的this始终指向当前运行的函数所属的对象。
<!-- more -->
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

另外，关于this的指向的问题，有个很奇怪的例子：
例一：

		var name = "outer";
		var person = {
			name:"inner",
			age:18,
			getName:function(){
				return this.name;
			}
		}
		console.log((person.getName=person.getName)());  //=>outer
而例二：

		var name = "outer";
		var person = {
			name:"inner",
			age:18,
			getName:function(){
				return this.name;
			}
		}
		person.getName=person.getName;
		console.log(person.getName());  //=>inner

解释：在例一中，赋值表达式的结果是函数本身，即（person.getName=person.getName）的结果是一个值，而这个值是函数。

			function(){
				return this.name;
			}

然后直接调用，因此此时this指向的是window对象。
而例二中明确指定是调用person的方法，故this指向的是person对象。