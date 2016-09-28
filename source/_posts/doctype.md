---
title: doctype
date: 2016-09-07 22:48:56
tags:
  -html
categories:
  - 学习笔记
  - 前端学习
---
## 关于doctype的一些知识

1. <!DOCTYPE>声明必须位于文档的第一行，位于<html>之前
2. <!DOCTYPE>不是html的标签，是指示web浏览器关于页面使用哪个HTML版本进行编写的指令
3. 在 HTML 4.01 中，<!DOCTYPE> 声明引用 DTD，因为 HTML 4.01 基于 SGML。DTD 规定了标记语言的规则，这样浏览器才能正确地呈现内容。
4. HTML5 不基于 SGML，所以不需要引用 DTD。
5. <!DOCTYPE> 声明没有结束标签。
6. <!DOCTYPE> 声明对大小写不敏感。
<!-- more -->

## 常见的DOCTYPE类型
html 5
&lt;!DOCTYPE html>
html 4.01
strict 
frameset
traditional
xhtml 1.0
strict 
frameset
traditional