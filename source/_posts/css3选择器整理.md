---
title: css3选择器整理
date: 2016-05-03 16:17:58
tags: css3
---
### 一 基本选择器（基本兼容所有浏览器）

通配选择器 *

元素选择器 E

类选择器 .class

ID选择器 #id

组群选择器

### 二 层次选择器

E F 后代选择器 （基本兼容所有浏览器）

E>F 子选择器 （ie7+）

E+F 相邻兄弟选择器（ie7+）

E~F 通用选择器匹配位于元素E之后的所有F元素（ie7+）

### 三 伪类选择器

1. 动态伪类选择器:link,:visited,:hover,:active, :focus

2. 目标伪类选择器:target

3. 语言伪类选择器E:lang(language)（ie8+）

4. UI元素状态伪类选择器E:checked E:enabled E:disabled（ie9+）

5. 结构伪类选择器（ie9+）

 5.1 E:first-child

 5.2 E:last-child

 5.3 E:root在html文档中始终为html

 5.4 E F:nth-child(n) n的起始值为1 F的父元素的第二个子元素

 5.5 E F:nth-last-child(n)

 5.6 E:nth-of-type(n)选择父元素内具有指定类型的第n个E元素

 5.7 E:nth-of-type(n)选择父元素内具有指定类型的倒数第n个E元素

 5.8 E:first-of-type

 5.9 E:last-of-type

 5.10 E:empty

 5.11 E:only-child父元素只包含一个子元素，且该子元素匹配E元素

 5.12 E:only-of-type父元素只包含一个同类型的子元素，且该子元素匹配E元素

6. 否定伪类选择器:not()(ie9+)

### 四 伪元素

:first-line,:first-letter,:before,:after，为了与伪类进行区分，CSS3中对此进行了调整，由单冒号变成了双冒号，

::first-line,::first-letter,::before,::after另外新增加了一个伪元素::selection，用于匹配突出显示的文本。

::selection仅接收两个属性 background和color。 ie系列中只有ie9支持，FireFox需要加上其私有属性-moz

如：

		::selection{
		background-color:red;
		color:#FFFFFF;
		}
		::-moz-selection{
		background-color:red;
		color:#FFFFFF;
		}


### 五  属性选择器（ie7+）

E[attr]具有attr属性的元素

E[attr = val]

E[attr |= val]具有val或者以val-开头

E[attr ~= val] attr有多个空格分隔的值其中一个为val

E[attr*=val]attr的任意位置包含了val

E[attr^=val]属性值以val开头

 E[attr$=val]属性以val结尾

选择器优先级：

 !important>内联>id>class>tag

组合使用选择器的情况下，选择器的权重计算方式为：

标签的权重为1，class的权重为10，id的权重为100

如

		div //权重为1
		.A  //权重为10
		#A //权重为100
		div.A //权重为11
相同权重的情况下后面定义的样式会覆盖前面定义的样式，但与html中class的定义的先后无关。如

		<div>
		    <p class = "B A">这里面是文字</p>
		</div>
		.A{
		color:red;}
		.B{
		color:blue;
		}
这时因为B的样式信息比A后定义，所以样式信息B会覆盖样式信息A，所以p中的文字会显示为蓝色。与AB在class中定义的顺序无关。
