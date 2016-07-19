---
title: JavaScript事件
date: 2016-07-19 14:17:02
tags: 
  - javascript事件
categories:
  - 学习笔记
  - 前端学习
---
# 事件介绍

1. JavaScript和html的交互是通过事件完成的。事件就是文档或浏览器窗口中发生的一些特定的交互瞬间。
2. 事件流是指从页面中接收事件的顺序
3. IE是事件冒泡流：事件开始时从具体的元素接收，逐级向上传播到较为不具体的节点（文档）
   Netscape是事件捕获流：不太具体的节点更早接收到事件，而最具体的节点应该最后接收到事件
4. 所有现代浏览器都支持事件冒泡，可以放心的使用事件冒泡，在有特殊需要时再使用事件捕获。
<!-- more -->

# DOM事件流

“DOM2级事件”规定事件流包括三个阶段：事件捕获阶段，出于目标阶段和事件冒泡阶段。
第一阶段是事件捕获，为截获事件提供了机会，最后一个阶段是冒泡阶段，可以在这阶段对事件作出响应。
在DOM事件流中，实际的目标在捕获阶段不会接收到事件。下一阶段是“出于目标”阶段，于是事件在目标上发生，并在事件处理中被看成冒泡阶段的一部分。

# 事件处理程序

响应某个事件的函数叫做事件处理程序（或事件侦听器）。

一 DOM0级事件处理程序：
将一个函数赋值给一个事件处理程序属性。这种方式有两个优点：
1. 简单
2. 具有跨浏览器的优势
使用DOM级方法指定的事件处理程序被认为是元素的方法。因此，这时的事件处理程序是在元素的作用域中运行的，即，程序中的this指向当前元素。以这种方式添加的事件处理程序会在事件流的冒泡阶段被处理。

二 DOM2级事件处理程序
addEventListener()和removeEventListener()
有三个参数，要处理的事件名，作为事件处理程序的函数和一个布尔值，true是在捕获阶段调用，false是在冒泡阶段调用。
优点：
可以添加多个事件处理程序，同一事件的事件处理程序按添加的顺序执行。

三 ie中的事件处理程序(ie8及以前)
attachEvent()和detachEvent()

在ie中使用attachEvent()添加事件处理程序与DOM0级方法添加的方式的主要区别在于：
1. 在使用DOM0级方法添加的时候，事件处理程序的作用域是其所属的元素作用域，而使用attachEvent方式添加，事件处理程序会在全局作用域中运行。
2. 也可以添加多个事件处理程序，不过<font color="red">*不以添加的顺序执行，而以相反的顺序执行*</font>

# 事件对象Event

在触发DOM上的某个事件时，会自动产生一个Event对象，这个对象包含着所有与事件有关的信息，兼容DOM的浏览器会将一个event对象传入事件处理程序中，无论指定事件处理程序时使用的是什么方法。

在事件处理程序内部，对象this的值始终等于currentTarget的值。

currentTarget 只读，其事件处理程序当前正在处理事件的那个元素。我觉得就是绑定事件处理程序的元素。
target 只读，事件的目标
stopPropagation()方法用于立即停止事件在DOM中的传播，即取消进一步的事件捕获或冒泡。如

	document.getElementsByTagName('ul')[0].onclick=function(e){
			console.log(this.nodeName);
			// e.stopPropagation();
		}
		document.getElementsByTagName('body')[0].onclick=function(e){
			console.log(this.nodeName);
		}

输出UL BODY，但是

	document.getElementsByTagName('ul')[0].onclick=function(e){
			console.log(this.nodeName);
			e.stopPropagation();
		}
		document.getElementsByTagName('body')[0].onclick=function(e){
			console.log(this.nodeName);
		}
只输出UL，事件在ul之后不会继续向上传播。

eventPhase()输出事件正在处于事件流的哪个阶段，1代表事件捕获阶段，2代码处于目标对象，3代表冒泡阶段

# 可以冒泡的事件和不能冒泡的事件
不能冒泡的事件
abort
blur
error
focus
load
mouseenter
mouseleave
resize
unload
可以冒泡的事件
beforeinput
click
compositionstart
compositionupdate
compositionend
dblclick
focusin
focusout
input
keydown
keyup
mousedown
mousemove
mouseout	
mouseover
mouseup
scroll
select
wheel