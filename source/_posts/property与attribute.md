---
title: property与attribute
date: 2016-07-19 15:13:22
tags: 
  - JavaScript
categories:
  - 学习笔记
  - 前端学习
---
本文对html中的property和attribute进行区分：

1. DOM对象的是属性（property），HTML标签的是特性（Attribute）

2. 每一个HTML标签(tag)都对应一个DOM接口HTMLXxxElement,比如Span标签对应的是HTMLSpanElement。这些标签的DOM接口都继承自HTMLElement接口，而HTMLElement又继承自Element。我们知道所有的标签都是一个元素结点,因此Element接口又继承自Node接口。其实HTML文档树中的所有东西都是结点,只不过有不同的结点类型而已。
<!-- more -->
3. HTML标签的attribute以类数组的形式存储在对应DOM对象的属性attributes中,attributes属性的类型为NamedNodeMap对象。
DOM对象提供了方法setAttribute，getAttribute和removeAttribute来操纵HTML标签的特性，包括自定义的特性。如下面的代码：

	var id1=elem.id;
	var id2=elem.getAttribute('id');
获取元素的id可以通过上面的两种方式，第一行代码中的方式是通过获取DOM的属性（property）获取的，而第二行代码中getAttribute获取的是HTML标签的特性（attribute）

* 这一点很重要，可以看出，特性，只是DOM中的一个属性而已，而这个属性本身是一个类数组对象-NamedNodeMap对象。

4. HTML标签attribute的名字和值都必须为字符串类型，而DOM对象的property没有此限制，可以是任何类型。

5. 有些HTML标签的attribute有对应的DOM对象property,但它们的取值却不一定是相同的。一般来说相对应的attribute与property其名字是一样的，但是class特性有所不同，因为class在javascript中为关键字，所以其所对应的property名字为className。

6. 对于input的value,使用getAttribute获取的永远是写HTML标签时指定的那个值,而value属性则获取到的是input当前输入的值。

7. 另一些特性比如checked,只要checked特性存在，无论其值是什么，DOM对象的checked属性的值都是true。这里checked属性已经不是字符串而是布尔类型了。

8. 还有一些特性比如style和onclick,其对应的DOM属性完全是返回一个对象了,比如elem.style属性就返回一个CSSStyleDeclaration对象。

9. HTML自定义attribute没有对应的DOM对象property。



参考文章：
DOM对象属性(property)与HTML标签特性(attribute)：http://openwares.net/linux/dom_property_element_attribute.html 
attribute和property的区别：http://stylechen.com/attribute-property.html
SD9006: IE 混淆了 DOM 对象属性（property）及 HTML 标签属性（attribute），造成了对 setAttribute、getAttribute 的不正确实现：
http://www.w3help.org/zh-cn/causes/SD9006
DOM元素的特性（Attribute）和属性（Property）：http://www.cnblogs.com/wangfupeng1988/p/3631853.html


