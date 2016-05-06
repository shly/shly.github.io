---
title: html标签学习
date: 2016-05-06 10:36:02
tags:
---
# a标签
## 属性
1. href
2. target 
规定在何处打开新链接。
3. media
 属性规定目标URL是为什么媒介/设备优化的。可接受多个值。且只能在href属性存在时使用。
   *html5 中的新属性*
   <!--more-->
4. download
 规定被下载的超链接目标。只有firefox和Chrome支持。
 *html5新属性*。
		<a download="filename"> 
filename 为下载之后文件的名字。没有指定filename时只下载不重命名。
5. type
 规定被链接文档的MIMI类型。
*html5新属性*
6. hreflang
 规定被链接文档的语言。仅在使用href属性时才使用。和 lang 属性不同的是，hreflang 属性不会指定标签中的内容所使用的语言，而是指定被 href 属性调用的文档所使用的语言。
\* 主流的浏览器几乎都不支持 hreflang 属性。
7. rel
 指定当前文档与被链接文档之间的关系。所有浏览器都支持。尽管浏览器不会以任何方式使用该属性，不过搜索引擎可以利用该属性获得更多有关链接的信息。
8. rev
 指定当前文档与被链接文档之间的关系。rel是指定从源文档到目标文档之间的关系，rev指定从目标文档到源文档之间的关系。
*几乎没有浏览器支持，html 5废除*
9. charset
 规定被链接文档的字符集
*主流的浏览器几乎都不支持 charset 属性。html 5废除*
10. shape
 规定链接的形状。只有 Firefox 和 Opera 支持 shape 属性。
*html 5废除*
11. coords
 coords 属性与 shape 属性配合，可以规定 object 或 img 元素中链接的尺寸、形状和位置。
*只有 Firefox 和 Opera 支持 coords 属性。html 5废除*
12. name
 描述锚的名称。主流浏览器都支持。id出现之前用的name，后id出现为了保证兼容性而保留。
*html 5废除*

## 总结
共12个属性，html 5新添属性有download，media，type三个。html 5 废除属性有charset,coords,name,rev,shape五个，剩下 href,target,rel,hreflang四个。其中hreflang主流浏览器都不支持。
# abbr标签
缩写，所有浏览器都支持。

		The <abbr title="People's Republic of China">PRC</abbr> was founded in 1949.
# acronym标签
首字母缩写。所有浏览器支持。html 5 废除，使用abbr代替。
# address标签
&lt;address>标签定义文档或文章的作者/拥有者的联系信息。
如果 &lt;address> 元素位于 &lt;body> 元素内，则它表示文档联系信息。
如果 &lt;address> 元素位于 &lt;article> 元素内，则它表示文章的联系信息。
&lt;address> 元素中的文本通常呈现为斜体。大多数浏览器会在 address 元素前后添加折行。
*所有主流浏览器支持，html 5新添*
# applet标签
定义嵌入的java applet。
*html 5废除，使用object代替。html 4.01中也不赞成使用*
# area标签
定义图像映射中的区域。area元素总是嵌套在map标签中。所有主流浏览器都支持。
&lt;img> 标签中的 usemap 属性与 map 元素 name 属性相关联，创建图像与映射之间的联系。
&lt;img> 中的 usemap 属性可引用 &lt;map> 中的 id 或 name 属性（由浏览器决定），所以我们需要同时向 &lt;map> 添加 id 和 name 两个属性。
## 必需属性 
alt，定义此区域的替换文本。
## 可选属性
 1. shape
定义区域的形状。可选值：圆形（circ 或 circle）、多边形（poly 或 polygon）、矩形（rect 或 rectangle）和default。未规定shape时会假定使用default。意味着该区域会覆盖整个图像。可以识别 shape 属性的 default 值的浏览器，可以提供一个包括全部热点的区域，以用于在超过其他热点定义的范围之外单击的情况。由于区域在 <map> 标签中是采用“先来先得”的顺序，所有必须将默认区域放置在后面。否则，默认区域会覆盖其他的图像映射中出现的所有区域。
所有浏览器都支持。
 2. coords
坐标值，定义可点击区域的坐标。与shape属性配合使用。
圆形：shape="circle"，coords="x,y,z"
这里的 x 和 y 定义了圆心的位置（"0,0" 是图像左上角的坐标），r 是以像素为单位的圆形半径。
多边形：shape="polygon"，coords="x1,y1,x2,y2,x3,y3,..."
每一对 "x,y" 坐标都定义了多边形的一个顶点（"0,0" 是图像左上角的坐标）。定义三角形至少需要三组坐标；高纬多边形则需要更多数量的顶点。
多边形会自动封闭，因此在列表的结尾不需要重复第一个坐标来闭合整个区域。
矩形：shape="rectangle"，coords="x1,y1,x2,y2"
第一个坐标是矩形的一个角的顶点坐标，另一对坐标是对角的顶点坐标，"0,0" 是图像左上角的坐标。请注意，定义矩形实际上是定义带有四个顶点的多边形的一种简化方法。
 3. href
href 属性规定区域中连接的目标。
 4. nohref
nohref 属性规定该区域没有相关的链接。
 5. target

# article标签
规定独立的自包含内容。
一篇文章应该具有其自身的意义。应该有可能独立于站点的其他部分对齐进行分发。
&lt;article> 元素的潜在来源：
 论坛帖子
 报纸文章
 博客条目
 用户评论
*html 5新添*
# aside标签
定义其所处内容之外的内容，应该与附近的内容相关。&lt;aside> 的内容可用作文章的侧栏。
*html 5新添*
# audio标签
	<audio src="someaudio.wav">
	您的浏览器不支持 audio 标签。
	</audio>
*Internet Explorer 8 以及更早的版本不支持 &lt;audio> 标签,html 5新添*
## 属性
1. autoplay
2. controls
3. loop
4. muted 规定音频输出应该被静音
5. preload 如果出现该属性，则音频在页面加载时进行加载，并预备播放。如果使用autoplay则忽略改属性。
6. src 

# b标签
加粗显示。

根据 HTML5 规范，在没有其他合适标签更合适时，才应该把 &lt;b> 标签作为最后的选项。HTML5 规范声明：应该使用 &lt;h1> - &lt;h6> 来表示标题，使用 &lt;em> 标签来表示强调的文本，应该使用 &lt;strong> 标签来表示重要文本，应该使用 &lt;mark> 标签来表示标注的/突出显示的文本。

# base标签
## 必须属性
   href
## 可选属性
  target

# basefont
规定页面上默认的字体和颜色。

	<basefont color="red" size="5" />
*只有ie支持*。
# bdi
bdi 指的是 bidi 隔离。
&lt;bdi> 标签允许您设置一段文本，使其脱离其父元素的文本方向设置。
在发布用户评论或其他您无法完全控制的内容时，该标签很有用。
## 属性
dir 取值：ltr,rtl,auto
*目前只有 Firefox 和 Chrome 支持 &lt;bdi> 标签。html5新添*
# bdo
bdo 元素可覆盖默认的文本方向。
## 可选属性
dir 取值：ltr,rtl
