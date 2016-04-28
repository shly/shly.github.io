---
title: 部署到git上面时报错 FATAL spawn git ENOENT
date: 2016-04-27 23:58:01
tags: hexo部署报错,hexo
---
报错信息
		FATAL spawn git ENOENT
		Error: spawn git ENOENT
		    at notFoundError (C:\Users\Administrator\Desktop\Hexo\node_modules\hexo-depl
		oyer-git\node_modules\hexo-util\node_modules\cross-spawn\node_modules\cross-spaw
		n-async\lib\enoent.js:8:11)
		    at verifyENOENT (C:\Users\Administrator\Desktop\Hexo\node_modules\hexo-deplo
		yer-git\node_modules\hexo-util\node_modules\cross-spawn\node_modules\cross-spawn
		-async\lib\enoent.js:43:16)
		    at ChildProcess.cp.emit (C:\Users\Administrator\Desktop\Hexo\node_modules\he
		xo-deployer-git\node_modules\hexo-util\node_modules\cross-spawn\node_modules\cro
		ss-spawn-async\lib\enoent.js:30:19)
		    at Process.ChildProcess._handle.onexit (child_process.js:1074:12)

解决方案：

之前使用cmd执行的hexo d ,改成使用git bash执行就成功了。