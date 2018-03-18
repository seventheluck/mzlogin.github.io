---
layout: post
title: Java修饰符对应的访问权限总结
categories: Java
description: Java修饰符对应的访问权限总结
keywords: 访问权限, 修饰符, Java
---
一说到“访问权限”四个字，我们首先想到的就是“层级”，不同层级的成员可以对不同层级的数据有读写的权限。今天，我们来深入探讨下Java中不同修饰符（private，无（包访问权限，可以理解为friendly类型），protected 和 public）对应的访问权限！

对于类中变量而言，能否被其他类访问，取决于变量的修饰词。
对于类中方法而言，能否被其他类访问，取决于方法的修饰词。
对于一个类而言，能否被其他类访问，取决于该类的修饰词。
在Java中，类成员访问权限修饰词有四类：private，无（包访问权限，可以理解为friendly类型），protected 和 public，而其中只有包访问权限和public才能修饰一个类（内部类除外）。
在下文中会提到的个别名词在此先做些解释：
>当前类：指的是同一个类内部；
>同一包：指的是类所在的文件夹是同一个；
>子孙类：指的是父类，子类的继承关系；
>不同包：指的是两个类或多个类所在的文件夹不是同一个；


## 变量
Java中的变量分为三种：
本地变量（局部变量）
实例变量（成员变量）
静态变量（类变量）

##### 重要：java中，friendly这个修饰符并没有显式的声明，在成员变量和方法前不用修饰符修饰时默认为friendly

### 1) public
权限最宽松，该成员变量是公共的，能在任何情况下被访问；

### 2)protected
权限相对宽松，不是同一个包且不是子类的情况下不能被访问；

### 3)friendly
权限相对严格，又名包权限，只能在同一个包中被访问；

### 4)private
权限最严格，只能在本类中访问。
#### 子类不能继承父类的private变量，但是可以通过父类的public方法访问父类的private变量;
#### 子类的对象会继承父类的private变量，可以通过父类的public方法访问父类的private变量;
>[Oracle Java Documentation: A subclass does not inherit the private members of its parent class. However, if the superclass has public or protected methods for accessing its private fields, these can also be used by the subclass. ](https://docs.oracle.com/javase/tutorial/java/IandI/subclasses.html)
>
>[ OBJECTS of subclasses contain private fields of their superclasses. ](https://stackoverflow.com/questions/4716040/do-subclasses-inherit-private-fields)

### 权限总结

|作用域	|当前类	|同一包	|子孙类	|不同包|
|:--------|:-------:|:--------:|:-------:|:------:|
|public	 |√	     |√	      |√	    |√     |
|protected	|√	|√	|√	|×|
|friendly	|√	|√	|×	|×|
|private	|√	|×	|×	|×|

### 5)static
static 与上面说到的public, protected, friendly, private等不一样，但是，我还是准备在这里将它列出来，因为它的访问方式也很特别！
static 变量不应该通过对象去获取，而是应该通过类去获取！如果一定要通过对象获取的话，会得到如下提示：
>The static field XXXClass.xxxmember should be accessed in a static way
因为，子类的对象并不会继承父类的static变量，父类的所有对象共享同一个static变量。无论有多少个对象，都只有一个static变量！
如果static与public, protected, friendly, private搭配使用，那就需要根据上面所说的权限来进行综合判断！

## 方法
### 1) public
权限最宽松，该成员方法是公共的，能在任何情况下被其他类访问；

### 2)protected
权限相对宽松，不是同一个包且不是子类的情况下不能被访问；

### 3)friendly
权限相对严格，又名包权限，只能在同一个包中被访问；

### 4)private
权限最严格，只能在本类中访问。
#### 子类不能继承父类的private变量，但是可以通过父类的public方法访问父类的private变量;
#### 子类的对象会继承父类的private变量，可以通过父类的public方法访问父类的private变量;
>[Oracle Java Documentation: A subclass does not inherit the private members of its parent class. However, if the superclass has public or protected methods for accessing its private fields, these can also be used by the subclass. ](https://docs.oracle.com/javase/tutorial/java/IandI/subclasses.html)
>
>[ OBJECTS of subclasses contain private fields of their superclasses. ](https://stackoverflow.com/questions/4716040/do-subclasses-inherit-private-fields)
我们可以做个小实验，你编写一个类，这个类的构造方法设置为private:
```
class F {
    // private Constructor!
    private F() {}
   
    public static void main() {
        F f = new F();//不报错！！！
    }

 }
 
class S extends F {
    // private Constructor!
    private S() {//报错！！！Implicit super constructor F() is not visible. Must explicitly invoke another constructor
    }
    
    public static void main() {
    		F f = new F();//报错！！！The constructor F() is not visible
    }
 } 
    
```
### 5)static
执行顺序为:
Father的静态代码块>>>Son的静态代码块>>>Father的非静态代码块>>>Father的构造方法>>>Son的非静态代码块>>>Son的构造方法；
如果static在一个类中出现多次,就按照出现的顺序执行.并且一个代码块都只会执行一次.
可以直接通过类名调用静态方法，静态方法中不能用this和super关键字，不能直接访问所属类的实例变量和实例方法(就是不带static的成员变量和成员成员方法)，只能访问所属类的静态成员变量和成员方法。因为实例成员与特定的对象关联！
因为static方法独立于任何实例，因此static方法必须被实现，而不能是抽象的abstract。
不建议用对象获取静态方法，如果一定要通过对象获取类的静态方法的话，会得到如下提示：
>The static field XXXClass.xxxmember should be accessed in a static way
static代码块也叫静态代码块，是在类中独立于类成员的static语句块，可以有多个，位置可以随便放，它不在任何的方法体内，JVM加载类时会执行这些静态的代码块，如果static代码块有多个，JVM将按照它们在类中出现的先后顺序依次执行它们，每个代码块只会被执行一次。

### 6)重写(Override)
这里要注意重写和重载的区别，第六点讲的是重写，不是重载！
>重写是子类对父类的允许访问的方法的实现过程进行重新编写, 返回值和形参都不能改变。
>重写的好处在于子类可以根据需要，定义特定于自己的行为。 也就是说子类能够根据需要实现父类的方法。
>重写方法不能抛出新的检查异常或者比被重写方法申明更加宽泛的异常。例如： 父类的一个方法申明了一个检查异常 IOException，但是在重写这个方法的时候不能抛出 Exception 异常，因为 Exception 是 IOException 的父类，只能抛出 IOException 的子类异常。
>
>重载(Overload)
重载(overloading) 是在一个类里面，方法名字相同，而参数不同。返回类型可以相同也可以不同。
>每个重载的方法（或者构造函数）都必须有一个独一无二的参数类型列表。最常用的地方就是构造器的重载。
声明为static的方法不能被重写，但是能够被再次声明。
子类和父类在同一个包中，那么子类可以重写父类所有方法，除了声明为private和final的方法。
子类和父类不在同一个包中，那么子类只能够重写父类的声明为public和protected的非final方法。
构造方法不能被重写。
如果不能继承一个方法，则不能重写这个方法。

## 类




