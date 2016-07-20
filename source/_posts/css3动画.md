---
title: css3动画
tags:
  - CSS3
  - CSS3动画
categories:
  - 学习笔记
  - 前端学习
date: 2016-07-20 16:40:44
---

# 什么是 CSS3 中的动画？

动画是使元素从一种样式逐渐变化为另一种样式的效果。
您可以改变任意多的样式任意多的次数。
-W3School
<!-- more -->
请用百分比来规定变化发生的时间，或用关键词 "from" 和 "to"，等同于 0% 和 100%。
0% 是动画的开始，100% 是动画的完成。
为了得到最佳的浏览器支持，您应该始终定义 0% 和 100% 选择器。

@keyframes 规则用于创建动画。在 @keyframes 中规定某项 CSS 样式，就能创建由当前样式逐渐改为新样式的动画效果。
Internet Explorer 10、Firefox 以及 Opera 支持 @keyframes 规则和 animation 属性。
Chrome 和 Safari 需要前缀 -webkit-。
Internet Explorer 9，以及更早的版本，不支持 @keyframe 规则或 animation 属性。

# 属性

@keyframes	规定动画。
animation	所有动画属性的简写属性，除了 animation-play-state 属性。	
animation-name	规定 @keyframes 动画的名称。	
animation-duration	规定动画完成一个周期所花费的秒或毫秒。默认是 0。	
animation-timing-function	规定动画的速度曲线。默认是 "ease"。	linear ease ease-in ease-out ease-in-out
animation-delay	规定动画何时开始。默认是 0。	
animation-iteration-count	规定动画被播放的次数。默认是 1。	
animation-direction	规定动画是否在下一周期逆向地播放。默认是 "normal"。	取值 normal或alternate
animation-play-state	规定动画是否正在运行或暂停。默认是 "running"。	取值paused或running
animation-fill-mode	规定对象动画时间之外的状态。

# 例子
	div
		{
			width:100px;
			height:100px;
			position: absolute;
			left: 0px;
			top: 0px;
			background:red;
			animation:myfirst linear 5s;
			/* animation-iteration-count: infinite;
			animation-direction: alternate;
			animation-play-state: running; */
			-moz-animation:myfirst linear 5s; /* Firefox */
			/* -moz-animation-iteration-count: infinite;
			-moz-animation-direction: alternate;
			-moz-animation-play-state: running; */
			-webkit-animation:myfirst linear 5s; /* Safari and Chrome */
			/* -webkit-animation-iteration-count: infinite;
			-webkit-animation-direction: alternate;
			-webkit-animation-play-state: running; */
			-o-animation:myfirst linear 5s; /* Opera */
			/* -o-animation-iteration-count: infinite;
			-o-animation-direction: alternate;
			-o-animation-play-state: running; */
		}

	@keyframes myfirst
	{
		0% {
			background:red;
			left: 0px;
			transform: rotate(0deg);
		}
		30%{
			background:yellow;
			transform: rotate(360deg);
			left: 300px;
		}
		60% {
			background:yellow;
			transform: rotate(720deg);
			left: 600px;
		}
		100% {
			background:red;
			transform: rotate(1080deg);
			left: 1000px;
		}
	}

	@-moz-keyframes myfirst /* Firefox */
	{
	0% {
			background:red;
			left: 0px;
			transform: rotate(0deg);
		}
		30%{
			background:yellow;
			transform: rotate(360deg);
			left: 300px;
		}
		60% {
			background:yellow;
			transform: rotate(720deg);
			left: 600px;
		}
		100% {
			background:red;
			transform: rotate(1080deg);
			left: 1000px;
		}
	}

	@-webkit-keyframes myfirst /* Safari and Chrome */
	{
	0% {
			background:red;
			left: 0px;
			transform: rotate(0deg);
		}
		30%{
			background:yellow;
			transform: rotate(360deg);
			left: 300px;
		}
		60% {
			background:yellow;
			transform: rotate(720deg);
			left: 600px;
		}
		100% {
			background:red;
			transform: rotate(1080deg);
			left: 1000px;
		}
	}

	@-o-keyframes myfirst /* Opera */
	{
	0% {
			background:red;
			left: 0px;
			transform: rotate(0deg);
		}
		30%{
			background:yellow;
			transform: rotate(360deg);
			left: 300px;
		}
		60% {
			background:yellow;
			transform: rotate(720deg);
			left: 600px;
		}
		100% {
			background:red;
			transform: rotate(1080deg);
			left: 1000px;
		}
	}