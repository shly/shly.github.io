---
title: CSS中的BFC
date: 2016-05-17 15:49:22
tags: 
  - BFC
categories:
  - 学习笔记
  - 前端学习
---
本文主要参考  http://www.w3cplus.com/css/understanding-block-formatting-contexts-in-css.html

# 什么是BFC
BFC（Block Formatting Context）块级格式化上下文。W3C定义如下：“浮动，绝对定位元素，inline-blocks, table-cells, table-captions,和overflow的值不为visible的元素，（除了这个值已经被传到了视口的时候）将创建一个新的块级格式化上下文。”
<!-- more -->
BFC是一个独立的渲染区域，只有Block-level box参与， 它规定了内部的Block-level Box如何布局，并且与这个区域外部毫不相干。
一个BFC是一个HTML盒子并且至少满足下列条件中的任何一个：

1. float的值不为none；
2. position的值不为static或者relative；（还有absolute和fixed）
3. display的值为 table-cell, table-caption, inline-block, flex, 或者 inline-flex中的其中一个；
4. overflow的值不为visible
*根元素也会生成一个BFC*

# BFC布局规则

1. 内部的Box会在垂直方向，一个接一个地放置。
2. Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠
3. 每个元素的margin box的左边， 与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。
4. BFC的区域不会与float box重叠。
5. BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
6. 计算BFC的高度时，浮动元素也参与计算

# BFC的用处
1. BFC中的盒子对齐  
W3C描述如下：
在BFC中，每个盒子的左外边框紧挨着包含块的左边框（从右到左的格式，则为紧挨右边框）。即使存在浮动也是这样的（尽管一个盒子的边框会由于浮动而收缩），除非这个盒子的内部创建了一个新的BFC浮动，盒子本身将会变得更窄）。
（一个盒子的边框会由于浮动而收缩的意思是，如果将float属性的值设置为left或right，元素就会向其父元素的左侧或右侧靠紧，同时默认情况下，盒子的宽度不在伸展，而是根据盒子里面的内容的宽度来确定。）
所有属于同一个BFC的盒子都左对齐（左至右的格式），他们的左外边框紧贴着包含块的左边框。在最后一个盒子里我们可以看到尽管那里有一个浮动元素（棕色）在它的左边，另一个元素（绿色）仍然紧贴着包含块的左边框。
2. 使用BFC来防止外边距折叠
毗邻块盒子的垂直外边距折叠只有他们是在同一BFC时才会发生。如果他们属于不同的BFC，他们之间的外边距将不会折叠。所以通过创建一个新的BFC我们可以防止外边距折叠。
3. 使用BFC来包含浮动：一个BFC可以包含浮动
4. 使用BFC来防止文字环绕
首先解释为什么会产生文字环绕的现象。当一个元素浮动之后，它就会脱离当前的文档流，它后面的盒子会越过它与前一个盒子对齐，在同一个BFC中，后面这个盒子的左边框会与包含框的左边框重合。而这个浮动的盒子会漂浮在后面盒子的上方，后面的盒子的文本行会进行收缩来为浮动元素提供空间。随着文字的增多，超过了浮动元素的高度时，文本行不需要收缩了，就产生了环绕的效果。当给后面盒子创建一个新的BFC后，它左边框变不需要紧挨着包含框，整个盒子收缩而不只是文本行收缩，所以就不会再产生文字环绕的现象。

5. 在多列布局中使用BFC

		.column{
		    width: 31.33%;
		    background-color: green;
		    float: left;
		    margin: 0 1%;
		}
		.column:last-child{
		    float: none;
		    overflow: hidden; 
		}

# BFC模式的触发

一个新的BFC可以通过给容器添加任何一个触发BFC的CSS样式，如overflow: scroll, overflow: hidden, display: flex, float: left,或者 display: table来创建。但注意：

1. display:table可能会产生一些问题
2. overflow:scroll可能会显示不必要的滚动条
3. float:left将会把元素置于容器的左边，其他元素环绕着它
4. overflow:hidden将会剪切掉溢出的元素
