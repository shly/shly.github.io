---
title: ajax使用
date: 2016-07-20 12:32:50
tags: 
  - ajax
categories:
  - 学习笔记
  - 前端学习
---
AJAX = Asynchronous JavaScript and XML（异步的 JavaScript 和 XML）。
<!-- more -->

	function getMethod(){
		var xhr;
		if(window.XMLHttpRequest){
			xhr = new XMLHttpRequest();
		}
		else{
			xhr = new ActiveXObject("Microsoft.XMLHTTP");
		}
		xhr.open("POST","test.js",true);
		xhr.send();
        xhr.onreadystatechange = function(){
        	if(xhr.readState==4&&xhr.status==200){
        		alert(xhr.responseText);
        	}
        }
	}
	function postMethod(){
		var xhr;
		if(window.XMLHttpRequest){
			xhr = new XMLHttpRequest();
		}
		else{
			xhr = new ActiveXObject("Microsoft.XMLHTTP");
		}
		xmlhttp.open("POST","ajax_test.asp",true);
		xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded");
		xmlhttp.send("fname=Bill&lname=Gates");
        xhr.onreadystatechange = function(){
        	if(xhr.readState==4&&xhr.status==200){
        		alert(xhr.responseText);
        	}
        }
	}

XMLHttpRequest 的状态。从 0 到 4 发生变化。
0: 请求未初始化
1: 服务器连接已建立
2: 请求已接收
3: 请求处理中
4: 请求已完成，且响应已就绪
HTTP status
1xx 消息
2xx 成功
3xx 重定向
4xx 请求错误
5xx 服务器错误

Ajax的优点：
1）页面无刷新，用户体验非常好。
2）使用异步方式与服务器通信，具有更加迅速的响应能力。
3）可以把一些服务器负担的工作转到客户端，利用客户端闲置的能力来处理，减轻服务器负担，节约空间和宽带租用成本。并且减轻服务器的负担，ajax的原则是“按需取数据”，可以最大程度的减少冗余请求和响应对服务器造成的负担。
4）基于标准化并被广泛支持的技术，不需要下载插件或者小程序。
Ajax的缺点:
1）Ajax不支持浏览器back按钮。
2）安全问题， Ajax暴露了与服务器交互的细节。
3）对搜索引擎的支持比较弱。
4）破坏了程序的异常机制。
5）不容易调试。
