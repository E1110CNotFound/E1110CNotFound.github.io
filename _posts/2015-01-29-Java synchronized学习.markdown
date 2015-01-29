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

三、当一个线程访问一个对象中的某个synchronized部分时，其他线程对该对象中的所有synchronized部分的访问将会被阻塞，即当一个线程访问一个对象中的某个synchronized部分时该线程就获得了该对象的对象锁，因此其他线程对该对象的所有synchronized部分的访问都将被阻塞。

synchronized示例如下

synchronized方法以及非synchronized方法定义
	public class Synchronized {

		/**
		 * 定义同步方法A
		 */
		public synchronized void synchronizedMethodA() {
			for(int i = 0; i < 3; i++) {
				System.out.println(Thread.currentThread().getName() + "\t访问同步方法A\t第" + (i + 1) + "次");
				try {
					Thread.sleep(1000);
				} catch (InterruptedException e) {
					e.printStackTrace();
				}
			}
		}

		/**
		 * 定义同步方法B
		 */
		public synchronized void synchronizedMethodB() {
			for(int i = 0; i < 3; i++) {
				System.out.println(Thread.currentThread().getName() + "\t访问同步方法B\t第" + (i + 1) + "次");
				try {
					Thread.sleep(1000);
				} catch (InterruptedException e) {
					e.printStackTrace();
				}
			}
		}

		/**
		 * 定义非同步方法
		 */
		public void unsynchronizedMethod() {
			for(int i = 0; i < 3; i++) {
				System.out.println(Thread.currentThread().getName() + "\t访问非同步方法\t第" + (i + 1) + "次");
				try {
					Thread.sleep(1000);
				} catch (InterruptedException e) {
					e.printStackTrace();
				}
			}
		}

	}

多线程访问synchronized部分以及非synchronized部分
	public class Main {

		public static void main(String[] args) {
			Synchronized syn = new Synchronized();

			//访问同步方法A的线程1
			Thread thread1 = new Thread(new Runnable() {
				
				@Override
				public void run() {
					syn.synchronizedMethodA();
				}
				
			}, "线程1");
			//访问非同步方法的线程2
			Thread thread2 = new Thread(new Runnable() {
				
				@Override
				public void run() {
					syn.unsynchronizedMethod();
				}
				
			}, "线程2");
			//访问同步方法A的线程3
			Thread thread3 = new Thread(new Runnable() {
				
				@Override
				public void run() {
					syn.synchronizedMethodA();
				}
				
			}, "线程3");
			//访问同步方法B的线程4
			Thread thread4 = new Thread(new Runnable() {
				
				@Override
				public void run() {
					syn.synchronizedMethodB();
				}
				
			}, "线程4");
			
			thread1.start();
			thread2.start();
			thread3.start();
			thread4.start();
		}
		
	}
