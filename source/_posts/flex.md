---
title: FlexBox学习笔记
date: 2016-05-13 15:41:17
tags: 
  - css3
  - flex
categories:
  - 学习笔记
  - 前端学习
---
Flex的出现是为了解决布局问题，使用flex布局很灵活，容器子元素的排列方式，对齐方式，显示顺序等都可以很方便的指定。目前处于非正式标准，但是新的浏览器基本上都支持。本文参考 https://segmentfault.com/a/1190000002910324
<!-- more -->
FlexBox是一个布局模块，不是一个简单的布局属性，它包含父元素和子元素的属性。flex布局主要依赖于flex direction。
## 主要术语

1. 主轴、主轴方向(main axis |main dimension)：用户代理沿着一个伸缩容器的主轴配置伸缩项目，主轴是主轴方向的延伸。
2. 主轴起点、主轴终点(main-start |main-end)：伸缩项目的配置从容器的主轴起点边开始，往主轴终点边结束。
3. 主轴长度、主轴长度属性(main size |main size property)：伸缩项目的在主轴方向的宽度或高度就是项目的主轴长度，伸缩项目的主轴长度属性是width或height属性，由哪一个对着主轴方向决定。
4. 侧轴、侧轴方向(cross axis |cross dimension)：与主轴垂直的轴称作侧轴，是侧轴方向的延伸。
5. 侧轴起点、侧轴终点(cross-start |cross-end)：填满项目的伸缩行的配置从容器的侧轴起点边开始，往侧轴终点边结束。
6. 侧轴长度、侧轴长度属性(cross size |cross size property)：伸缩项目的在侧轴方向的宽度或高度就是项目的侧轴长度，伸缩项目的侧轴长度属性是"width"或"height"属性，由哪一个对着侧轴方向决定。

## 主要属性

1. display(flex container)

		display: other values | flex | inline-flex;
2. flex-direction(flex container)

		flex-direction: row | row-reverse | column | column-reverse
3. order（flex items）
默认情况下，伸缩项目是按照文档流出现先后顺序排列。然而，“order”属性可以控制伸缩项目在他们的伸缩容器出现的顺序。

		order: <integer> 
4. flex-wrap（flex container）
这个主要用来定义伸缩容器里是单行还是多行显示，侧轴的方向决定了新行堆放的方向。

		flex-wrap: nowrap | wrap | wrap-reverse
5. flex-flow（flex container）
这个是“flex-direction”和“flex-wrap”属性的缩写版本。同时定义了伸缩容器的主轴和侧轴。其默认值为“row nowrap”。

		flex-flow: <‘flex-direction’> || <‘flex-wrap’>
6. justify-content（flex container）
这个是用来定义伸缩项目沿着主轴线的对齐方式。当一行上的所有伸缩项目都不能伸缩或可伸缩但是已经达到其最大长度时，这一属性才会对多余的空间进行分配。当项目溢出某一行时，这一属性也会在项目的对齐上施加一些控制。

		justify-content: flex-start | flex-end | center | space-between | space-around;
7. align-content（flex container）
这个属性主要用来调准伸缩行在伸缩容器里的对齐方式。类似于伸缩项目在主轴上使用“justify-content”一样。（侧轴方向的对齐方式）

		align-content: flex-start | flex-end | center | space-between | space-around | stretch;
8. align-items（flex container）

		align-items: flex-start | flex-end | center | baseline | stretch
9. align-self（flex items）
用来在单独的伸缩项目上覆写默认的对齐方式。

		align-self: auto | flex-start | flex-end | center | baseline | stretch;
10. flex-grow（flex items）
根据需要用来定义伸缩项目的扩展能力。它接受一个不带单位的值做为一个*比例*。主要用来决定伸缩容器剩余空间按比例应扩展多少空间。

		flex-grow: <number>; /* default 0 */
如果所有伸缩项目的“flex-grow”设置了“1”，那么每个伸缩项目将设置为一个大小相等的剩余空间。如果你给其中一个伸缩项目设置了“flex-grow”值为“2”，那么这个伸缩项目所占的剩余空间是其他伸缩项目所占剩余空间的两倍。
11. flex-shrink(flex items)
根据需要用来定义伸缩项目收缩的能力。[注意：负值同样生效。]

		flex-shrink: <number>; /* default 1 */
12. flex-basis（flex items）
这个用来设置伸缩基准值，剩余的空间按比率进行伸缩。

		flex-basis: <length> | auto; /* default auto */
如果设置为“0”，不考虑剩余空白空间。如果设置为自动，则按照flex-grow值分配剩余空白空间。
13. flex（flex items）
这是“flex-grow”、“flex-shrink”和“flex-basis”三个属性的缩写。其中第二个和第三个参数（flex-shrink、flex-basis）是可选参数。默认值为“0 1 auto”。

		flex: none | [ <'flex-grow'> <'flex-shrink'>|| <'flex-basis'> ]
## justify-content,align-content,align-items,flex-basis 区别

演示链接
http://shly.github.io/shly/IFE/task_10/index.html