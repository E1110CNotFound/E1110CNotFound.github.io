---
layout: post
title:  Java synchronized学习
author:	Guo Yonghui
date:   2015-01-29 21:33:00
categories: Java
---
synchronized是Java语言中的关键字，当用synchronized来修饰一个方法或是一个代码块时，例如

	/**
	 * 修饰一个方法
	 */
	public synchronized void method() {
		//code
	}
	
	/**
	 * 修饰一个代码块
	 */
	public void method() {
		synchronized (this) {
			//code block
		}
	}