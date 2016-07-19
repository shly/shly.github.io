---
title: cookie
tags:
  - cookie
categories:
  - 学习笔记
  - 前端学习
date: 2016-07-19 13:55:58
---

# cookie定义
cookie 是存储于访问者的计算机中的变量。每当同一台计算机通过浏览器请求某个页面时，就会发送这个 cookie。你可以使用 JavaScript 来创建和取回 cookie 的值。
# 设置和读取cookie
通过设置document.cookie设置cookie如

	document.cookie='name=sly';
	document.cookie="age=23"

<!--  more -->
cookie设置之后就是一个字符串，通过document.cookie读取，如

	document.cookie  => "name=sly; age=23"

还可以设置cookie的有效期，如

	document.cookie='name=sly;expires=date';

下面是完整的设置cookie和获取cookie的方法，来自w3c

	function setCookie(c_name,value,expiredays)
	{
		var exdate=new Date()
		exdate.setDate(exdate.getDate()+expiredays)
		document.cookie=c_name+ "=" +escape(value)+
		((expiredays==null) ? "" : ";expires="+exdate.toGMTString())
	}

	function getCookie(c_name)
	{
	if (document.cookie.length>0)
	  {
	  c_start=document.cookie.indexOf(c_name + "=")
	  if (c_start!=-1)
	    { 
		    c_start=c_start + c_name.length+1 
		    c_end=document.cookie.indexOf(";",c_start)
		    if (c_end==-1) c_end=document.cookie.length
		    return unescape(document.cookie.substring(c_start,c_end))
	    } 
	  }
		return ""
	}

# cookie和webstorage的区别
1. cookie有大小限制，每个cookie所存放的数据不能超过4kb，如果cookie字符串的长度超过4k，则该属性返回空字符串。webstorage大概可以存储5Mb，不同浏览器不同
2. cookie是http协议的一部分，cookie数据始终在同源的http请求中携带，浪费带宽，webstorage不会把数据传到服务器端，仅保存在本地。
3. cookie可以设置过期时间，到了过期时间浏览器就会将cookie删除，如果不设置过期时间则浏览器窗口关闭则删除。
   localstorage会一直保存在本地，除非手动删除
   sessionstorage仅在当前浏览器窗口关闭前有效
4. sessionStorage不在不同的浏览器窗口中共享，即使是同一个页面；
   localStorage 在所有同源窗口中都是共享的；
   cookie也是在所有同源窗口中都是共享的。
