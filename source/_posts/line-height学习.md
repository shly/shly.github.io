---
title: line-height学习
date: 2017-05-11 11:42:24
tags:
---
## line-height定义

行高，两行文字基线之间的距离
基线：字母x的下边缘的位置

## line-height与行内框盒子模型

所有的内联样式的表现都与行内框盒子模型有关。
<!-- more -->

    <p>这是一行普通的文字，这里有个<em>em</em>标签。</p>

上面的代码包含的盒子：
1. 内容盒子（content area）
2. 内联盒子（inline boxes）
3. 行框盒子（line boxes）
4. 包含盒子（containing box）

## line-height的高度机理
内联元素的高度是有line-height决定的
1. 行高由于其继承性，影响无处不在，即使单行文本也不例外
2. 行高是幕后黑手，高度的表现不是行高，而是内容区域和行间距
行高 = 内容区域高度+行间距（line-height = content area+vertical spacing）
（1）内容区域高度只与字号和字体有关，与line-height没有任何关系
（2）在simsun（宋体）下，内容区域高度等于文字大小
在simsun字体下 font-size+行间距=line-height

## line-height的属性值
1. 默认属性 normal 与浏览器及字体有关
2. 数值，根绝当前元素的font-size计算。如当前元素font-size为36，line-height为1.5，则实际行高像素为1.5*36
3. &lt;length>
4. &lt;percent>
5. inherit
 
line-height:1.5,line-height:150%,line-height:1.5em有什么区别？
计算上没有差别。应用元素有差别
1. line-height:1.5所有可继承元素根据font-size重计算行高。
2. line-height:150%/1.5em 当前元素根绝font-size计算行高，继承给下面的元素。

## line-height与图片的表现
行高会不会影响图片实际占用的尺寸？
不会！！
消除图片底部间隙的方法
1. 图片块状化-无基线对齐
2. font-size设为0
3. 图片底线对齐
4. 行高足够小-基线位置上移如设为0

小图片和大文字
基本上高度受行高控制
剩下的就是图文的vertical-align垂直对齐了
## 行高的实际应用
1. 大小不固定的图片、多行文字的垂直居中

		.box{line-height:300px;text-align:center;font-size:0px;}
		.box>img{vertical-align:middile;}
		//ie8及其以上支持
   多行文本水平垂直居中
        .box{line-height:300px;text-align:center;font-size:0px;}
		.box>.text{display:inline-block;line-height:normal;vertical-align:middile;text-align:left;max-width:100%;}
2. 代替height避免ie6/7下的haslayout（冲破容器限制）
