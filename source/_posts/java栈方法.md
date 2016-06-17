---
title: java栈方法中push与add方法的区别
date: 2016-06-17 09:06:46
tags: 
  - java
  - stack
  - add and push
categories:
  - 学习笔记
  - java
---
Java中Stack的压栈操作有两个方法，add和push，
先看下push的api

	 TreeNode java.util.Stack.push(TreeNode item)


	Pushes an item onto the top of this stack. This has exactly the same effect as: 

	 addElement(item)
	Parameters:
	item the item to be pushed onto this stack.
	Returns:
	the item argument.
	See Also:
	java.util.Vector.addElement
再看一下add的api

	 boolean java.util.Vector.add(TreeNode e)


	Appends the specified element to the end of this Vector.

	Specified by: add(...) in List, Overrides: add(...) in AbstractList
	Parameters:
	e element to be appended to this Vector
	Returns:
	true (as specified by Collection.add)
	Since:
	1.2
可以发现两者的返回值不同，push方法返回的是被压入栈的元素，add方法返回的是压栈是否成功。
再来看一下两者的实现。首先是push方法

push是在Stack类中实现的，可以看到返回的就是压栈的元素本身。
	public E push(E item) {
	        addElement(item);

	        return item;
	    }
而addElement方法是在Vector类中实现的，代码如下：

	 public synchronized void addElement(E obj) {
	        modCount++;
	        ensureCapacityHelper(elementCount + 1);
	        elementData[elementCount++] = obj;
	    }

接下来看一下add方法的实现，add方法直接是在Vector类中实现的，代码如下：

	public synchronized boolean add(E e) {
	        modCount++;
	        ensureCapacityHelper(elementCount + 1);
	        elementData[elementCount++] = e;
	        return true;
	    }
通过源代码可以看出两者只有返回值不同。