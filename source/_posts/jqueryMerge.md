---
title: jquery源码分析之merge()
date: 2016-07-17 20:31:09
tags: 
  - javascript
  - jquery
categories:
  - 学习笔记
  - 前端学习
---
jquery中的merge
作用：合并两个数组，返回的结果会修改第一个数组的内容——第一个数组的元素后面跟着第二个数组的元素
<!-- more -->

	merge: function( first, second ) {
			var i = first.length,
				j = 0;
            //对于类数组对象
			if ( typeof second.length === "number" ) {
				for ( var l = second.length; j < l; j++ ) {
					first[ i++ ] = second[ j ];
				}

            //对于非类数组对象
			} else {
				while ( second[j] !== undefined ) {
					first[ i++ ] = second[ j++ ];
				}
			}
		   //手动修正数组的length
			first.length = i;

			return first;	
		}
typeof second.length === "number" 很好理解，下面举个else中的例子：

	var people = {
	   	name:"xiaohua",
	   	age:"26"
	}
	console.log(people.length); => undefined
	console.log($.merge([1,2,3], people)); => 1,2,3

但是对于键为数值的对象，如果是从0开始往后依次加1的情况（如果不是从0开始，second[0]就为undefined，则退出循环），仍然可以加入到数组中，如：

	var people = {
	   	0:"xiaohua",
	   	1:"26"
	}
	console.log(people.length); => undefined
	console.log($.merge([1,2,3], people)); => 1,2,3,xiaohua,26
		
需要注意的是第一个元素的length一定要为数值。
最后解释下为什么需要修正length值。当第一个参数是类数组时，如：

	<ul>
	<li></li>
	</ul>
	var first = [1,2,3,4,5,6];
	console.log($.merge($("li"), first).length); =>7

如果不进行修正的话，则

   $.merge($("li"), first).length => 1


