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

能够保证在同一时刻最多只有一个线程在执行该部分代码。

一、当两个并发线程访问同一个对象中的synchronized部分时，同一时刻内只能有一个线程可以执行该部分代码，另一个线程必须等待当前线程执行完该部分代码后才可以执行该部分代码。

二、当一个线程访问一个对象中的synchronized部分时，另一个线程仍可以并发地访问该对象中的非synchronized部分。

三、当一个线程访问一个对象中的synchronized部分时，其他线程对该对象中的所有其他synchronized部分的访问将会被阻塞，即当一个线程访问一个对象中的synchronized部分时该线程就获得了该对象的对象锁，因此其他线程对该对象的所有synchronized部分的访问都将被阻塞。

