## 问题
### 程序代码
请阅读如下代码，并给出输出！
```java
package package_1;

class A {
	public String show(D obj) {
		return ("A and D");
	}

	public String show(A obj) {
		return ("A and A");
	}
}

class B extends A {

	public String show(B obj) {

		return ("B and B");
	}

	public String show(A obj) {

		return ("B and A");
	}
}

class C extends B {
}

class D extends C {
}

public class ExtendClass {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		A a1 = new A();
		A a2 = new B();
		B b = new B();
		C c = new C();
		D d = new D();
		System.out.println(a1.show(b)); // ① A and A
		System.out.println(a1.show(c)); // ② A and A
		System.out.println(a1.show(d)); // ③ A and D
		System.out.println(a2.show(b)); // ④ 编译：A and A；运行：B and A；
		System.out.println(a2.show(c)); // ⑤ 编译：A and A；运行：B and A；
		System.out.println(a2.show(d)); // ⑥ 编译：A and D；运行：B-->A-->show(D)
		System.out.println(b.show(b)); // ⑦ B and B
		System.out.println(b.show(c)); // ⑧ B and B
		System.out.println(b.show(d));// ⑨A and D

		
		}

}

```


## 解决步骤：
### 1、编译阶段：
程序首先保证的是编译不能出错，所以，方法调用以引用类型为准，引用调用方法的优先级：this.show(object) > super.show(object) > this.show(super(object)) > 
		 * a1.show(b) --> A.show(A)
		 * a1.show(c) --> A.show(A)
		 * a1.show(d) --> A.show(D)
		 * a2.show(b) --> A.show(A)
		 * a2.show(c) --> A.show(A)
		 * a2.show(d) --> A.show(D)
		 * b.show(b) --> B.show(B)
		 * b.show(c) --> B.show(B)
		 * b.show(d) --> B.show(D)
     
### 2、运行阶段：
运行阶段的调用规则是，变量和静态方法优先按引用类型来调用，其余方法优先按实例类型来调用！
		 * a1.show(b) --> A.show(A) --> 引用类型：A，实例类型：A --方法优先按实例类型A--> A and A
		 * a1.show(c) --> A.show(A) --> 引用类型：A，实例类型：A --方法优先按实例类型A--> A and A
		 * a1.show(d) --> A.show(D) --> 引用类型：A，实例类型：A --方法优先按实例类型A--> A and D
		 * a2.show(b) --> A.show(A) --> 引用类型：A，实例类型：B --方法优先按实例类型B--> B and A
		 * a2.show(c) --> A.show(A) --> 引用类型：A，实例类型：B --方法优先按实例类型B--> B and A
		 * a2.show(d) --> A.show(D) --> 引用类型：A，实例类型：B --方法优先按实例类型B，B调用继承的父类A的方法--> A and D
		 * b.show(b) --> B.show(B) --> 引用类型：B，实例类型：B --方法优先按实例类型B--> B and B
		 * b.show(c) --> B.show(B) --> 引用类型：B，实例类型：B --方法优先按实例类型B--> B and B
		 * b.show(d) --> B.show(D) --> 引用类型：B，实例类型：B --方法优先按实例类型B，B调用继承的父类A的方法--> A and D
