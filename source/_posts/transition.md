---
title: css3中transition用法总结
date: 2016-05-05 13:33:54
tags: 
  - css3
  - css3 transition
categories:
  - 学习笔记
---

以下内容主要出自《图解CSS3-大漠》

### W3C标准中对transition的描述
CSS3的transition允许css的属性值在一定的时间区间内平滑的过渡。这种效果可以在鼠标单击，获得焦点，被点击或者对元素的任何改变中触发，并平滑地以动画的效果改变css的属性值。
<!-- more -->
### css中创建简单过渡的步骤
  （1）在默认样式中声明元素的初始状态样式
  （2）声明过渡元素最终状态样式
  （3）在默认样式中通过添加过渡函数，添加一些不同的样式。 
### transition属性主要包含四个属性值
  （1）transition-property：指定过渡或动态模拟的CSS属性
  （2）transition-duration：指定完成过渡所需的时间
  （3）transition-timing-function：指定过渡函数
  （4）transition-delay:指定过渡开始出现的延迟时间
### 简写形式
      transition: <property> <duration> <animation type> <delay>
### 可以使用过渡的属性
  （1）颜色属性
  （2）具有长度值，百分比的属性
  （3）integer
  （4）number真实的（浮点型）数值
  （5）变形系列属性。如rotate(),rotate3d(),scale(),scale3d(),skew(),translate(),translate3d()等
  （6）reactangle：通过x,y,width,height变形
  （7）visibility：离散步骤，在0~1范围内
  （8）阴影
  （9）渐变
  （10）paint server(SVG)：只支持下面的情况。从gradient到gradient，以及从color到color
  （11）space-separated list of above：如果列表有相同的项目数值，则列表每一项按照上面的规则进行变化，否则无变化
  （12）缩写属性
### 浏览器兼容性
  （1）IE 10+（PP3）（平台预览第三版），Firefox4.0~15.0，Chrome4.0~	20.0，Safari3.1~6.0和Opera10.5~12.0，在使用时需要加上各浏览器的私有属性。
  （2）IE10+，Firefox16.0+，chrome26.0+，Safari 7.0+，Opera 12.1+支持transition的标准语法。
  （3）ios Safari 3.2~6.1、Android browser2.1+，Blackberry browser7.0+和chrome for Android 27.0需要添加浏览器前缀-webkit-,Opero mobile 10.0~12.0中需要添加浏览器前缀-o-。
  （4）ios Safari 7.0+和Firefox for Android 22.0支持transition的标准语法。
### 开关状态的不同过渡方式
		input{
			width: 200px;
			height: 20px;
			border: 1px solid #CCC;
			transition: width 1s;
		}
		input:focus{
			width: 300px;
		}
这样当input获得焦点时和失去焦点时，input宽度的变化都是在1秒内完成的。
但是如果像下面这样写

		input{
			width: 200px;
			height: 20px;
			border: 1px solid #CCC;
			transition: width .2s;
		}
		input:focus{
			width: 300px;
			transition: width 1s;
		}
那么当input获得焦点时，宽度从200px变化到300px是在1s内完成的，失去焦点时宽度从300px变回到200px时则是在0.2s内完成的。
演示见 http://shly.github.io/shly/IFE/task_12/index.html
### css过渡的触发
（1）伪元素触发 :active :focus :checked
（2）媒体查询触发
（3）JavaScript触发，给元素添加新的类，向新的类添加过渡如

		.box{
			width:100px;
			height:100px;
			border:1px solid #000;
			transition: width 2s;
		}
		.box .on{
			width:200px;
		}
### 启用硬件加速使过渡更流畅
   以下内容引自：<http://www.cnblogs.com/rubylouvre/p/3471490.html>
   CSS animations, transforms 以及 transitions不会自动开启GPU加速，而是由浏览器的缓慢的软件渲染引擎来执行。那我们怎样才可以切换到GPU模式呢，很多浏览器提供了某些触发的CSS规则。
   现在，像Chrome, FireFox, Safari, IE9+和最新版本的Opera都支持硬件加速，当它们检测到页面中某个DOM元素应用了某些CSS规则时就会开启，最显著的特征的元素的3D变换。
   例如：

		.cube {
		   -webkit-transform: translate3d(250px,250px,250px)
		   rotate3d(250px,250px,250px,-120deg)
		   scale3d(0.5, 0.5, 0.5);
		}
可是在一些情况下，我们并不需要对元素应用3D变换的效果，那怎么办呢？这时候我们可以使用个小技巧“欺骗”浏览器来开启硬件加速。
虽然我们可能不想对元素应用3D变换，可我们一样可以开启3D引擎。例如我们可以用transform: translateZ(0); 来开启硬件加速。

		.cube {
		   -webkit-transform: translateZ(0);
		   -moz-transform: translateZ(0);
		   -ms-transform: translateZ(0);
		   -o-transform: translateZ(0);
		   transform: translateZ(0);
		   /* Other transform properties here */
		}
   在 Chrome and Safari中，当我们使用CSS transforms 或者 animations时可能会有页面闪烁的效果，下面的代码可以修复此情况：

		.cube {
		   -webkit-backface-visibility: hidden;
		   -moz-backface-visibility: hidden;
		   -ms-backface-visibility: hidden;
		   backface-visibility: hidden;
		 
		   -webkit-perspective: 1000;
		   -moz-perspective: 1000;
		   -ms-perspective: 1000;
		   perspective: 1000;
		   /* Other transform properties here */
		}
   在webkit内核的浏览器中，另一个行之有效的方法是

		.cube {
		   -webkit-transform: translate3d(0, 0, 0);
		   -moz-transform: translate3d(0, 0, 0);
		   -ms-transform: translate3d(0, 0, 0);
		   transform: translate3d(0, 0, 0);
		  /* Other transform properties here */
		}
原生的移动端应用(Native mobile applications)总是可以很好的运用GPU，这是为什么它比网页应用(Web apps)表现更好的原因。硬件加速在移动端尤其有用，因为它可以有效的减少资源的利用(麦时注：移动端本身资源有限)。

只对我们需要实现动画效果的元素应用以上方法，如果仅仅为了开启硬件加速而随便乱用，那是不明智的。
小心使用这些方法，如果通过你的测试，结果确是提高了性能，你才可以使用这些方法。使用GPU可能会导致严重的性能问题，因为它增加了内存的使用，而且它会减少移动端设备的电池寿命。