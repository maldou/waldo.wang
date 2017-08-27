---
title: Java中的作用域和编程规范
date: 2016-12-27 16:16:29
tags:
- java作用域
- 编程规范
categories:
- JAVA
---
### java作用域
java语言提供了四种作用域，用于控制类、成员和方法的可见性
+ public：对所有类可见
+ protected：对本包和所有子类可见
+ private：只对本类可见
+ default：只对本包可见，默认（没有标明任何修饰符）

#### 继承
子类在继承父类并覆盖父类方法的时候，子类方法的可见性不能低于父类方法的可见性
#### 反射
java作用域在编译阶段可以很好的保护类的成员和方法，但是由于java提供了反射机制，可以在运行时动态处理类，比如调用Class#getDeclaredFields()获取该类所有的属性，即使该属性默认是private的，依然可以通过Field#setAccessilbe(true)拿到field的访问权限：
```
Field.get(Object clazzObject) //返回field对象表示的值
Filed.set(Object clazzObject, Object newVAlue) //设置filed对象表示的属性值
Method.invoke(Object clazzObject, Object... tags) //执行Method表示的方法
```

### 编程规范   
在阿里巴巴Java开发手册中有如下规约
> 【推荐】接口类中的方法和属性不要加任何修饰符号（public 也不要加），保持代码的简洁性，并加上有效的Javadoc 注释。尽量不要在接口里定义变量，如果一定要定义变量，肯定是与接口方法相关，并且是整个应用的基础常量。

之所以规约中如此推荐，是因为对于接口中的方法默认都是public的，所以接口中定义的方法为了保持代码的简洁，无需在加上public;同样地，在接口中可以定义常量，并自动设置为public static final。
```java
public interface MyInterface {
  void foo();
  String foo = "FOO"; //a public static final constant
}
```
