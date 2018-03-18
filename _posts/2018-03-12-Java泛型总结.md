---
layout: post
title: Java泛型总结
categories: Java
description: Java泛型总结
keywords: 泛型, Java
---
## 概念
Java是在JDK5.0的时候引入的泛型，泛型是Java中非常重要的一个概念，但是大部分人对泛型的了解都很片面，今天通过这篇文章好好整理一下泛型的知识点，目的就是将泛型的用法、注意点做一个总结！

大家都知道Java中有抽象类，抽象类体现了数据抽象的思想，是实现多态的一种机制。它定义了一组抽象的方法，至于这组抽象方法的具体表现形式有派生类来实现。

那么泛型是什么呢？
>泛型是一个“抽象的类型”--将类型进行抽象！
>
>泛型是一个“类型参数”--将类型作为参数！
我们来看个例子吧：

方法在定义List时没有指定列表元素的具体类型:
```java
List myIntList = new LinkedList(); // 1
myIntList.add(new Integer(0)); // 2
Integer x = (Integer) myIntList.iterator().next(); // 3
```
方法通过List<Integer>指定了List中元素为Integer类型:
```java
List<Integer> 
    myIntList = new LinkedList<Integer>(); // 1'
myIntList.add(new Integer(0)); // 2'
Integer x = myIntList.iterator().next(); // 3'
```
List是一个泛型接口，LinkedList是一个泛型类，在实例化对象时，Integer作为参数被传入泛型类中，从而让编译器知道应该将该类成员实例化成为什么类型：
```java
 * @param <E> the type of elements in this list
 *
 * @author  Josh Bloch
 * @author  Neal Gafter
 * @see Collection
 */

public interface List<E> extends Collection<E> {
    // Query Operations
    }
    
 * @author  Josh Bloch
 * @see     List
 * @see     ArrayList
 * @since 1.2
 * @param <E> the type of elements held in this collection
 */

public class LinkedList<E>
    extends AbstractSequentialList<E>
    implements List<E>, Deque<E>, Cloneable, java.io.Serializable
```
## 重要特点
泛型只在编译阶段有效，在编译之后程序会采取去泛型化的措施。
也就是说Java中的泛型，只在编译阶段有效。
在编译过程中，正确检验泛型结果后，会将泛型的相关信息擦除，并且在对象进入和离开方法的边界处添加类型检查和类型转换的方法。
也就是说，泛型信息不会进入到运行时阶段。

泛型有三大用法：泛型类、泛型接口、泛型方法

## 泛型类

## 泛型接口

## 泛型方法
