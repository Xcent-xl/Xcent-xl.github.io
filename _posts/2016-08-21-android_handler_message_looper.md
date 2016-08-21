---
layout: post
title: android_消息循环
tags:
---
#android _Message _Handler _Looper
android通过Looper，Message，Handler进行消息循环，还有一个在Looepr里面进行维护的消息队列Message Queue，在使用中并不会直接操作。   
##Looper  
通过looper使一个线程变成循环线程，该线程不断循环，有新任务立即执行，没有则等待。   
 
	public class LooperThread extends Thread{
		public void run(){
			Looper.prepare();//使线程初始化为Looper线程
			//进行例如实例化Handler等其他准备操作
			Looper.looper();//开始循环处理MessageQueue队列中的任务
			}
		}
一个线程中只能有一个Looper对象，主线程中也有一个属于自己的Looper，  
##Handler
handler可以往Message Queue中添加消息并通过自身的HandleMessage方法进行处理。  
handler创建的时候默认构造方法会自动关联当前线程的looper  
一个线程可以有多个handler，但是只能有一个Looper   
可以在容易线程中通过对handler的引用向message queue中添加消息并进行处理，那么就能够在非UI线程中进行UI更新了。  
##Message  
Message msg = Message.obtain()在message对象部位空的情况下回从message对象池中返回实例进行复用，当对象为空时则是new Message()进行返回message对象
