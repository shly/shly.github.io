---
title: jquery中的prop和attr
date: 2016-07-19 21:26:27
tags: 
  - jquery
categories:
  - 学习笔记
  - 前端学习
---
之前分析了HTML中的属性（property）和特性attribute，在jquery中也有两个类似的方法，prop()和attr(),那么这两个方法有什么区别呢？
首先看下api中介绍的功能差别：

 prop(name|properties|key,value|fn)

获取在匹配的元素集中的第一个元素的属性值。
随着一些内置属性的DOM元素或window对象，如果试图将删除该属性，浏览器可能会产生错误。jQuery第一次分配undefined值的属性，而忽略了浏览器生成的任何错误。

源代码如下：

	prop: function( name, value ) {
		return jQuery.access( this, name, value, true, jQuery.prop );
	}

 attr(name|properties|key,value|fn)

设置或返回被选元素的属性值。

	attr: function( name, value ) {
		return jQuery.access( this, name, value, true, jQuery.attr );
	}

两者的差别在于
jQuery.access()的最后一个参数。来看一下jQuery.access()的实现

	// Mutifunctional method to get and set values to a collection
		// The value/s can optionally be executed if it's a function
		access: function( elems, key, value, exec, fn, pass ) {
			var length = elems.length;

			// Setting many attributes
			if ( typeof key === "object" ) {
				for ( var k in key ) {
					jQuery.access( elems, k, key[k], exec, fn, value );
				}
				return elems;
			}

			// Setting one attribute
			if ( value !== undefined ) {
				// Optionally, function values get executed if exec is true
				exec = !pass && exec && jQuery.isFunction(value);

				for ( var i = 0; i < length; i++ ) {
					fn( elems[i], key, exec ? value.call( elems[i], i, fn( elems[i], key ) ) : value, pass );
				}

				return elems;
			}

			// Getting an attribute
			return length ? fn( elems[0], key ) : undefined;
		}
这个方法首先判断key是不是object，如果是，则遍历object中的每个key，对每个key执行access方法。
其次，判断value是否给定，如果给定，则为set操作
判断value是不是函数，如果是则exec为true，否则为false，即如果value不是函数则直接赋值，如果value为函数则要先执行函数。
