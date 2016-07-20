---
title: 将本地项目首次提交到远程git上遇到的问题
date: 2016-07-20 17:27:33
tags: 
  - git
  - gitignore配置
categories:
  - 学习笔记
  - git学习
---
当初将一个项目托管到git上时，应首先在git上建立一个仓库，比如名为example，然后在本地项目的文件夹下执行下面的指令：
<!-- more -->

1. git init
2. git add README.md
3. git commit -m "first commit"
4. git remote add origin git@github.com:shly/example.git
5. git push -u origin master
这里面要注意下第5步，平时我们向git上提交代码时只需要执行git push origin master即可，但是第一次一定要加个-u，否则以后执行git pull时必须执行git push -u origin master，加上之后每次pull时只要git pull即可。没加-u时，执行git pull

	warning: push.default is unset; its implicit value has changed in
	Git 2.0 from 'matching' to 'simple'. To squelch this message
	and maintain the traditional behavior, use:

	  git config --global push.default matching

	To squelch this message and adopt the new behavior now, use:

	  git config --global push.default simple

	When push.default is set to 'matching', git will push local branches
	to the remote branches that already exist with the same name.

	Since Git 2.0, Git defaults to the more conservative 'simple'
	behavior, which only pushes the current branch to the corresponding
	remote branch that 'git pull' uses to update the current branch.

	See 'git help config' and search for 'push.default' for further information.
	(the 'simple' mode was introduced in Git 1.7.11. Use the similar mode
	'current' instead of 'simple' if you sometimes use older versions of Git)

	fatal: 'master' does not appear to be a git repository
	fatal: Could not read from remote repository.

	Please make sure you have the correct access rights
	and the repository exists.

详情见：
http://stackoverflow.com/questions/5697750/what-exactly-does-the-u-do-git-push-u-origin-master-vs-git-push-origin-ma