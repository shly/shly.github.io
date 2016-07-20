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