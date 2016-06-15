---
title: 二叉树遍历java版（递归与非递归）
date: 2016-06-14 10:50:34
tags: 
  - 数据结构
  - 二叉树遍历
categories:
  - 学习笔记
  - 数据结构
---
今天复习了一下二叉树的遍历，包括递归与非递归形式，记录一下
首先定义一个简单的二叉树结构，包括节点的值与左子节点和右子节点
<!-- more -->

	public class TreeNode {
		int value;
		TreeNode left,right;
		public TreeNode(int value, TreeNode left, TreeNode right) {
			this.value = value;
			this.left = left;
			this.right = right;
		}
	}
下面是递归方式实现的，首先是先序遍历

	public void preOrder(TreeNode root) {
			if (root != null) {
				System.out.print(root.value);
				preOrder(root.left);
				preOrder(root.right);
			}
		}

中序遍历

	public void inOrder(TreeNode root) {
			if (root != null) {
				inOrder(root.left);
				System.out.print(root.value);
				inOrder(root.right);
			}
		}

后序遍历

	public void postOrder(TreeNode root) {
			if (root != null) {
				postOrder(root.left);
				postOrder(root.right);
				System.out.print(root.value);
			}
		}

递归的形式比较简单，就是调整三行代码的顺序，下面来看非递归的实现。首先是先序遍历

	public void preOrder1(TreeNode root) {
			Stack<TreeNode> stack = new Stack<TreeNode>();
			if (root != null) {
				stack.add(root);
				while (!stack.isEmpty()) {
					TreeNode p = stack.pop();
					System.out.print(p.value);
					if (p.right != null) {
						stack.add(p.right);
					}
					if (p.left != null) {
						stack.add(p.left);
					}
				}
			}
		}
先序遍历是先遍历根节点，首先将根节点压入栈底，然后弹出，弹出时要记得输出。看当前根节点是否有右子节点，有则压入右子节点，为什么要先压入右子节点呢，原因是栈是先进后出，我们要先弹出左子节点，故要先压入右子节点。然后在看有没有左子节点，有则压入，现在栈里面有两个个节点，依次是左子节点和右子节点，这个时候弹出左子节点，将左子节点视为根节点，继续重复上面过程，左子节点都弹出之后在弹出右子节点，将右子节点视为根节点，继续重复以上步骤。

下面看中序遍历的非递归形式

	public void inOrder1(TreeNode root) {
			Stack<TreeNode> stack = new Stack<TreeNode>();
			while (root != null || !stack.isEmpty()) {
				if (root != null) {
					stack.push(root);
					root = root.left;
				}else {
					root = stack.pop();
					System.out.print(root.value);
					root = root.right;
				}
			}
		}
最后是后序遍历的非递归形式

	public void postOrder1(TreeNode root) {
			Stack<TreeNode> stack = new Stack<TreeNode>();
		    Stack<TreeNode> output = new Stack<TreeNode>();
		    TreeNode node = root;
		    while (node != null || !stack.empty()) {
		      if (node != null) {
		        output.push(node);
		        stack.push(node);				
		        node = node.right;
		      } else {
		        node = stack.pop();				
		        node = node.left;
		      }
		    }
		    while (output.size() > 0) {
		    	System.out.print(output.pop().value);
		    }
		}

