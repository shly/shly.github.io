---
title: npm笔记(修改npm镜像站)
date: 2016-07-26 15:42:24
tags:
---
方法一 命令行输入npm config edit可以调出.npmrc文件（npm userconfig file）。通过修改里面的register可以修改npm镜像站点。
<!-- more -->

方法二 使用nrm（NPM registry manager） 
nrm 
NPM registry manager can help you easy and fast switch between different npm registries, now include: cnpm, taobao, nj(nodejitsu), rednpm, edunpm


Install

$ npm install -g nrm

Example
	$ nrm ls
	 
	* npm -----  https://registry.npmjs.org/
	  cnpm ----  http://r.cnpmjs.org/
	  taobao --  https://registry.npm.taobao.org/
	  nj ------  https://registry.nodejitsu.com/
	  rednpm -- http://registry.mirror.cqupt.edu.cn
	  skimdb -- https://skimdb.npmjs.com/registry
	 
	$ nrm use cnpm  //switch registry to cnpm
	 
	    Registry has been set to: http://r.cnpmjs.org/
 
Usage
Usage: nrm [options] [command]
 
  Commands:
 
    ls                           List all the registries
    use <registry>               Change registry to registry
    add <registry> <url> [home]  Add one custom registry
    del <registry>               Delete one custom registry
    home <registry> [browser]    Open the homepage of registry with optional browser
    test [registry]              Show the response time for one or all registries
    help                         Print this help
 
  Options:
 
    -h, --help     output usage information
    -V, --version  output the version number