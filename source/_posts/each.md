---
title: jQuery each方法
date: 2016-06-16 15:59:50
tags: 
  - jquery
categories:
  - 学习笔记
  - 前端学习
---

jQuery中有两个each方法，一个是$().each(callback),一个是$.each();
API中对$().each(callback)的描述如下：
以每一个匹配的元素作为上下文来执行一个函数。
<!-- more -->
意味着，每次执行传递进来的函数时，函数中的this关键字都指向一个不同的DOM元素（每次都是一个不同的匹配元素）。而且，在每次执行函数时，都会给函数传递一个表示作为执行环境的元素在匹配的元素集合中所处位置的数字值作为参数（从零开始的整型）。 返回 'false' 将停止循环 (就像在普通的循环中使用 'break')。返回 'true' 跳至下一个循环(就像在普通的循环中使用'continue')。
callback是对每个匹配元素要执行的函数。

对jQuery.each(object, [callback])的描述如下：
通用例遍方法，可用于例遍对象和数组。
不同于例遍 jQuery 对象的 $().each() 方法，此方法可用于例遍任何对象。回调函数拥有两个参数：第一个为对象的成员或数组的索引，第二个为对应变量或内容。如果需要退出 each 循环可使回调函数返回 false，其它返回值将被忽略。
两个参数：
object:需要例遍的对象或数组。
callback:每个成员/元素执行的回调函数。

为了更好的理解两个方法，来看一下jQuery-1.11.3中两个方法的实现：

	jQuery.fn = jQuery.prototype = {
		each: function( callback, args ) {
			return jQuery.each( this, callback, args );
		}
	}

	jQuery.extend({
				each: function( obj, callback, args ) {
				var value,
					i = 0,
					length = obj.length,
					isArray = isArraylike( obj );

				if ( args ) {
					if ( isArray ) {
						for ( ; i < length; i++ ) {
							value = callback.apply( obj[ i ], args );

							if ( value === false ) {
								break;
							}
						}
					} else {
						for ( i in obj ) {
							value = callback.apply( obj[ i ], args );

							if ( value === false ) {
								break;
							}
						}
					}

				// A special, fast, case for the most common use of each
				} else {
					if ( isArray ) {
						for ( ; i < length; i++ ) {
							value = callback.call( obj[ i ], i, obj[ i ] );

							if ( value === false ) {
								break;
							}
						}
					} else {
						for ( i in obj ) {
							value = callback.call( obj[ i ], i, obj[ i ] );

							if ( value === false ) {
								break;
							}
						}
					}
				}

				return obj;
			}
		})
