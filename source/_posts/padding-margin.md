---
title: padding and margin学习笔记
date: 2016-09-28 21:46:01
tags: 
  - padding
  - margin
categories:
  - 学习笔记
  - 前端学习
---
# padding学习笔记

1. 对于block水平元素：

当padding-left+padding-right>width时，容器的宽度变为padding-left+padding-right，
容器中的内容按最小尺寸显示（width为200px的盒子，padding为200px时，盒子的宽度变为400px）

2. 对于inline水平元素（width和height不能设置）

水平padding影响尺寸，垂直padding不影响尺寸,但是会影响背景色（占据空间）

## padding应用
1. 高度可控的分割线
1.1 直接使用字符
1.2 inline-block控制
1.3 使用inline padding

    	注册&lt;span>&lt;span>登录

    	span{
    	padding：16px 6px 1px;
    	margin-left:12px;
    	border-left:2px solid;
    	font-size:0;
    	}
