---
title: history pushState 实现浏览器前进与后退
date: 2016-03-29 16:24:21
tags: 
  - html5
  - pushState
categories:
  - 学习笔记
  - 前端学习
---
今天做了个界面需要用到ajax进行页面跳转，当然使用ajax进行页面跳转有它的优点，比如降低服务器压力，缩短用户等待时间等，但是一个很明显的缺点就是浏览器的前进和后退按钮失效了，好在HTML5的history对象的出现比较好的解决了这个问题，所以去网上找一些pushState使用的文章，但是大多数都是只讲原理没有实现的实例，理解起来还是不太容易的。现在将我理解的一些内容说一下，不对的地方欢迎大家指出。
<!-- more -->
首先讲一下API：
首先是方法有两个history.pushState()和history.replaceState()
事件有一个window.onpopstate
pushState（）方法，接收三个参数
a state object, a title (which is currentlyignored), and (optionally) a URL

其中，state对象保存的是被pushState页面的信息的一个拷贝，也就是说以后你要用到的信息，都可以放到这个对象中。
url是可选的，负责改变浏览器的地址栏中显示的url，如果没有指定url，你点击前进后退按钮页面还是会变化，只是浏览器的地址栏上显示的url会一直保持不变。
replaceState（）方法，与pushState方法相同，主要用于改变当前历史记录中记录的当前页面的state对象和url信息。
onpopstate事件,每次点击浏览器的前进和后退按钮，就会触发window的Onpopstate事件。
最后使用history.state获取当前所在页面的state对象，也就是在上面pushState中保存的。

下面以一个例子具体说明。

首先，我们一般做一个网站，刚进去的首页是没有pathname的，为了让浏览器能够后退到首页，我们对首页的url进行拦截，即改变首页的url。这里面history.replaceState只是改变网页的url地址，不会改变网页内容。这里面的state保存的是你要在将来获取到的任何信息。

	var url = “blog/index.html”;

	var state = {
	    url:url

	}
	history.replaceState(state,””,"blog/index.html");

接下来,当调用ajax使页面内容发送变化之后，我们将这个变化的页面状态保存起来，如

	var url = “blog/index.html”;

	var state = {

	      url:url

	}

	window.history.pushState(state,"",url);

最后，给window添加监听，当popstate被触发之后，我们通过history.state获取到达页面的信息，通过.操作符获取该页面的信息，如我这里保存了该页面的url，就通过history.state.url获取，然后通过这个url加载页面。

	window.addEventListener("popstate",function() {
	var currentUrl = history.state.url;
		$(".container").load(currentUrl +" #container");
	});

