---
title: java中的Queue与Deque
tags:
  - java
  - stack
  - add and push
categories:
  - 学习笔记
  - java
date: 2016-06-18 23:46:10
---

java中的栈为Stack，Stack是一个类，队列为Queue，但是与栈的实现不同的是，Queue是一个接口，而不是实现类。Queue接口定义的方法有：
<!-- more -->

	 boolean add(E e);//向队列中添加一个元素，成功返回true
	 boolean offer(E e);//向队列中添加一个元素，成功返回true
	 E remove();
	 E poll();
	 E element();
	 E peek();

Deque为双端队列，也是一个接口，继承自Queue。以Deque接口的一个实现类ArrayDeque为例，说一下add方法与offer方法的区别。
先看一下add方法的实现

	public boolean add(E e) {
	        addLast(e);
	        return true;
	    }
	 public void addLast(E e) {
	        if (e == null)
	            throw new NullPointerException();
	        elements[tail] = e;
	        if ( (tail = (tail + 1) & (elements.length - 1)) == head)
	            doubleCapacity();
	    }
再看一下offer方法的实现

	public boolean offer(E e) {
	        return offerLast(e);
	    }
	public boolean offerLast(E e) {
	        addLast(e);
	        return true;
	    }
	public void addLast(E e) {
	        if (e == null)
	            throw new NullPointerException();
	        elements[tail] = e;
	        if ( (tail = (tail + 1) & (elements.length - 1)) == head)
	            doubleCapacity();
	    }
	    