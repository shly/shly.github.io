---
title: javascript作用域
date: 2016-07-31 14:35:58
tags: 
  - javascript
  - 作用域
categories:
  - 学习笔记
  - 前端学习
---
在此篇文章中，针对变量的作用域，执行环境等问题，通过一些小demo进行了对比分析
我们来看下面的几个小例子
<!-- more -->

1. 首先来个最简单的：

		var a = 1;
		function test1(){
		  console.log(a);
		}
		test1();   //=>1
这个程序输出1肯定没什么问题了，函数局部作用域内没有局部变量a，因此沿着作用域链向上查找，找到了全局变量a，于是输出。

2. 接下来添加个局部变量：

		var a = 1;
		function test1(){
		  var a = 2;
		  console.log(a);
		}
		test1();   //=>2
这段程序输出2，因为沿着作用域链向上查找时，首先找到的是局部变量a是2，于是将2输出.

3. 继续变形

		var a = 1;
		function test1(){
		  console.log(a);
		  var a = 2;
		  console.log(a);
		}
		test1();   //=>undefined 2
这时第一个console.log(a)输出undefined，第二个输出2，第二个其实不难理解，但是有可能有人不能理解第一个为什么会输出undefined。其实主要是变量声明提升（javascript引擎在执行时，会把所有的变量的声明都提升到当前作用域的最前端）的问题，即上面的代码相当于

		var a = 1;
		function test1(){
		  var a;
		  console.log(a);
		  a = 2;
		  console.log(a);
		}
		test1();
这时，当第一次要输出a时，程序会首先在局部作用域中查找a，在这个函数中，程序找到了变量a，故不会继续沿着作用域链向上查找，但是这里的a只声明了并没有进行初始化，故默认为undefined。

4. 接下来，看一下下面的代码会输出什么

		var a = 1;
		function test2(){
		  console.log(a);
		}
		function test1() {
		  var a = 2;
		  test2();
		}
		test1();
输出的是1 ，为什么呢，我们要清楚，在test1中，我们只是让test2函数执行了，而test2仍在全局环境中，并不是test1的局部环境，故test2根本不会访问到位于test1局部环境中的a。

5. 对4中的代码进行修改，我们来看一下将test2定义在test1中的情况

		var a = 1;
		function test1() {
		  var a = 2;
		  function test2(){
		    console.log(a);
		  }
		  test2();
		}
		test1();
这样一来，test2在test1的局部环境中，a自然就会输出2。

6. 接下来我们来看看对象中的方法

		var a = 1;
		var b = {
		    a: 	2,
		    show:function(){
			console.log(a);
		   }
		}
		b.show();  //=>1
单纯的这样看这段代码为什么会输出1可能会不太明显，但是如果稍微转换一下，就很好明白了。

		var b = {
		    a: 	2,
		    show:function(){
			console.log(a);
		   }
		}
其实是相当于

		var b = {};
		b.a = 2;
		b.show = function(){
		  console.log(a);
		}
这样很明显就看出a应该是全局环境中的a了.

7. 与上面例子类似的，看下面的代码：

		var a = 1;
		var b = {
		    a: 	2,
		    show:function(){
			console.log(this.a);
		   }
		}
		b.show();  //=>2
上面是经常使用的，定义对象的方式，使用了this关键字，将a与当前的执行对象绑定，输出的是当前执行对象的a属性，故输出2.

8. 再继续对上面的例子进行变形

		var a = 1;
		var b = {
		    a: 	2,
		    show:function(){
			console.log(this.a);
		   }
		}
		var c = b.show;
		c();  //=> 1
这里是个比较容易出问题的地方，需要注意的是，this指向的是执行时的当前对象，在上个例子中，直接调用b.show()，show方法的执行环境是b，故输出的是b.a,但是在这个例子中，c指向的是function(){console.log(this.a)}，相当于你在全局环境中定义c

		var c = function(){
		  console.log(this.a);
		}
这里c的执行环境是全局环境，故应输出window.a。
关于this的指向的问题，请参看http://shly.github.io/2016/07/17/this/