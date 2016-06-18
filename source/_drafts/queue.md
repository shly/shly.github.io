---
title: java中的Queue与Deque
date: 2016-06-18 23:46:10
tags: 
  - java
  - stack
  - add and push
categories:
  - 学习笔记
  - java
---
java中的栈为Stack，Stack是一个类，队列为Queue，但是与栈的实现不同的是，Queue是一个接口，而不是实现类。Queue接口定义的方法有：

	 boolean add(E e);//向队列中添加一个元素，成功返回true
	 boolean offer(E e);
	 E remove();
	 E poll();
	 E element();
	 E peek();

Deque为双端队列，也是一个接口，继承自Queue。