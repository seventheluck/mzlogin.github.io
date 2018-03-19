---
layout: post
title: 堆和栈（Heap and Stack）的区别
categories: DataStructure
description: 堆和栈（Heap and Stack）的区别
keywords: Data Structure, 堆, 栈, Heap, Stack
---
## 堆和栈最明显的区别是：

堆（Heap）：队列优先,先进先出（FIFO—first in first out）；

栈（Stack）：先进后出(FILO—First-In/Last-Out)；

如果有人把堆栈合起来说，那他很可能说的是栈！
<!--more-->
## 其次，他们还有如下区别：

栈（Stack）：

栈（Stack）是暂存空间(scratch space),主要用于内部计算。当函数被调用时，栈（Stack）队列上有一块区域会被分配出来用作存储局部变量和数据。当函数返回时，这块区域会被释放！由于栈（Stack）是FILO队列，所以，最近被使用的区域会最先被释放，最后被使用的区域被后释放！栈（Stack）的使用不需要我们操心！

堆（Heap）：

堆（Heap）是动态分配的，你可以在任意时间自由分配！使用起来肯定比栈（Stack）复杂，但是也给了我们灵活性！

操作系统在线程建立时会自动为系统级线程分配Stack，而Heap的分配是由程序运行时调用系统完成的！Stack的速度比Heap要快的多！

![image](http://upload-images.jianshu.io/upload_images/2946710-d392ce975fbeb450?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Image source: [vikashazrati.wordpress.com](http://vikashazrati.wordpress.com/2007/10/01/quicktip-java-basics-stack-and-heap/)
