#### 访问控制修饰符

Java 支持 4 种访问权限：

+ default (即缺省，什么也不写)：在同一包内可见，不使用任何修饰符。使用对象：类、接口、变量、方法。
+ private：在同一类可见。使用对象：变量、方法。**注意：不能修饰类（外部类）**
+ public：对所有类可见。使用对象：类、接口、变量、方法。
+ protected：对同一包内的类和所有子类可见。使用对象：变量、方法。**注意：不能修饰类（外部类）**。



| 修饰符    | 当前类 | 同一包内 | 子孙类（同一包） | 子孙类（不同包） | 其他包 |
| --------- | ------ | -------- | ---------------- | ---------------- | ------ |
| public    | Y      | Y        | Y                | Y                | Y      |
| protected | Y      | Y        | Y                | Y/N              | N      |
| default   | Y      | Y        | Y                | N                | N      |
| private   | Y      | N        | N                | N                | N      |



**默认访问修饰方法，不适用任何关键字**

使用默认访问修饰符声明的变量和方法，对同一包内的类是可见的。

接口里的变量都隐式地声明为 public static final，接口里的方法默认情况下访问权限为 public。



#### 访问控制和继承

+ 父类种声明为 public 的方法在子类中也必须为 public。
+ 父类中声明为 protected 的方法在子类中要么声明为 protected，要么声明为 public，不能声明为 private。
+ 父类中声明为 private 的方法，不能够被继承。



#### 非访问修饰符

为了实现一些其他的功能，Java 也提供了许多非访问修饰符：、

+ static 用来修饰类方法和类变量。
+ final 用来修饰类、方法和变量。final 修饰的类不能够被继承，修饰的方法不能被继承类重新定义，修饰的变量为常量，是不可修改的。（在第一次赋值后不可修改）
+ abstract 用来创建抽象类和抽象方法。
+ synchronized 和 volatile 主要用于线程的编程。

