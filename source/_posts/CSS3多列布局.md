---
title: CSS3多列布局
date: 2016-05-18 17:21:45
tags: 
  - css3
  - css3多列布局
categories:
  - 学习笔记
  - 前端学习
---
# 主要属性
## 1 break-after、break-before、break-inside
描述页面、列或者区域形成一个盒子后的中断行为（即是否中断以及如何中断），如果没有形成一个盒子，这个实行将会被忽略。
每一个可能的断点（即每一个元素的边界）都是受三个属性的影响：前一个元素的break-after值，下一个元素的break-before值，以包含元素的break-inside值。
<!-- more -->
规定断点要遵循以下的规则：
1. 如果三个值中的任何一个值是强制中断值，即left, right, page, column 或者region，这个值具有优先级，如果有多个强制型的中断值同时出现，那么在流中最后一个出现的值生效。（即break-before的值的优先级高于break-after, break-after的优先级高于break-inside）
2. 这三个值中的任意一个是避免中断的值，即avoid, avoid-page, avoid-region, avoid-column，那么应用的地方就不会被中断。

一旦应用了强制中断，当需要的时候可以添加软中断，但是不能应用在一个使用了aviod值的元素边界上。

	Initial value	auto
	Applies to	block-level elements
	Inherited	no
	Media	paged
	Computed value	as specified
	Animatable	no
	Canonical order	the unique non-ambiguous order defined by the formal grammar
### values

	auto | avoid | avoid-page | page | left | right | recto | verso | avoid-column | column | avoid-region | region

## 2 columns-count
column-count属性描述元素列的个数。

	Initial value	auto
	Applies to	non-replaced block elements (except table elements), table-cell or inline-block elements
	Inherited	no
	Media	visual
	Computed value	as specified
	Animatable	yes, as an integer
	Canonical order	the unique non-ambiguous order defined by the formal grammar
## 3 column-fill
column-fill属性描述内容是如何被分配到各列中的。
### values

	auto | balance
balance:每行高度相同。
auto:只占据内容需要的空间。

	Initial value	balance
	Applies to	multicol elements
	Inherited	no
	Media	visual, but, in continuous media, has no effect in overflow columns
	Computed value	as specified
	Animatable	no
	Canonical order	the unique non-ambiguous order defined by the formal grammar
## 4 column-gap
描述列之间的间距。
### values

	<length> | normal
normal:浏览器默认间距

	Initial value	normal
	Applies to	multicol elements
	Inherited	no
	Media	visual
	Computed value	the absolute length or the keyword normal
	Animatable	yes, as a length
	Canonical order	the unique non-ambiguous order defined by the formal grammar
## 5 column-row
在多列布局中column-row指定指定列之间的分割线，是 column-rule-width, column-rule-style and column-rule-color.的简写形式。

	Initial value	as each of the properties of the shorthand:
	column-rule-width: medium
	column-rule-style: none
	column-rule-color: currentColor
	Applies to	multicol elements
	Inherited	no
	Media	visual
	Computed value	as each of the properties of the shorthand:
	column-rule-color: If the value is translucent, the computed value will be the rgba() corresponding one. If it isn't, it will be the rgb() corresponding one. The transparent keyword maps to rgba(0,0,0,0).
	column-rule-style: as specified
	column-rule-width: the absolute length; 0 if the column-rule-style is none or hidden
	Animatable	as each of the properties of the shorthand:
	column-rule-color: yes, as a color
	column-rule-style: no
	column-rule-width: yes, as a length
	Canonical order	order of appearance in the formal grammar of the values
### values

		<'column-rule-width'>
		<length>|thin|medium|thick
		<'column-rule-style'>
		none | hidden | dotted | dashed | solid | double | groove | ridge | inset | outset
		<'column-rule-color'>
		Is a <color> value.

*取值相当于border*

## 6 column-span
当一个元素的column-span属性被设置为all时，它可以让这个元素跨越所有列，当一个元素跨越超过一个列时，这个元素叫spanning element。

	Initial value	none
	Applies to	in-flow block-level elements
	Inherited	no
	Media	visual
	Computed value	as specified
	Animatable	no
	Canonical order	the unique non-ambiguous order defined by the formal grammar

### values
	none | all
如：

	h1, h2 {
	  column-span: all;
	}
## 7 column-width
column-width在没有column-count的情况下用来计算应该有多少列。比如容器的宽度为500px，column-gap为0，column-width设为400，则只能显示一列，且列的实际宽度为500px。如果column-width设为250px,则显示两列，每列宽度为250px。这时候将column-count设为1则显示一列，设为2显示两列，设为3还是显示两列。（所以应该是每列的最小宽度）
## 8 columns
column-width，column-count的缩写

	Initial value	as each of the properties of the shorthand:
	column-width: auto
	column-count: auto
	Applies to	non-replaced block elements (except table elements), table-cell or inline-block elements
	Inherited	no
	Media	visual
	Computed value	as each of the properties of the shorthand:
	column-width: the absolute length, zero or larger
	column-count: as specified
	Animatable	as each of the properties of the shorthand:
	column-width: yes, as a length
	column-count: yes, as an integer
	Canonical order	order of appearance in the formal grammar of the values

<'column-width'> || <'column-count'>

演示 http://shly.github.io/shly/IFE/task_12/index.html