---
title: 配置Hexo
date: 2016-04-26 23:39:40
tags: 
  - hexo
  - hexo配置
categories:
  - 学习笔记
  - hexo学习
---

hexo要在node环境下部署。
主要命令：
1. 装置hexo
		$ npm install -g hexo
2. 部署hexo
		$ hexo init
<!-- more -->
3. 生成html页面
		$ hexo g
4. 运行测试环境
		$ hexo s
接下来就可以在浏览器中输入 localhost:4000 查看了
6. 安装部署插件
		$ npm install hexo-deployer-git--save
7. 配置_config.yml文件，在文件的最后一行加上
		deploy:
		  type: git
 		 repo: https://github.com/XXX/XXX.github.io.git(你的git地址)
 		 branch: master

8. 部署
		$ hexo d

另外type的值也有可能为github。

当然，在进行第五步部署到git上之前，必须得有一个git地址。

以下是有关Hexo配置的两篇文章

http://blog.csdn.net/poem_of_sunshine/article/details/29369785/

http://www.jianshu.com/p/465830080ea9