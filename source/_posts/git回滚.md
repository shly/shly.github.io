---
title: git回滚
date: 2016-07-28 16:05:57
tags: 
  - git
categories:
  - 学习笔记
  - git学习
---
Git版本恢复命令,首先通过git log指令找出要恢复的版本，之后可以执行下面的两种操作

1. git reset

git reset 版本号 
git checkout .
这两个指令可以将本地的代码恢复成历史版本，但是无法提交到远程，除非使用git push -f但是这样会直接将远程代码库恢复成历史版本，中间做的任何修改都会消失，不推荐使用

2. git reverse



