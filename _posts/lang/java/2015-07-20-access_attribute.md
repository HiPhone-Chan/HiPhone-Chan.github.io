---
layout: post
title: Java 访问属性总结
categories: java
---

Java 访问属性总结
==============
      
 |修饰词                                   | 本类 | 同一个包的类 | 继承类 | 其他类 |
 |:-----:       | :-----: | :-----: |:-----:|:-----: |
 |private       | √  |   ×     |  ×  |  ×  |
 |无(不能用default)| √  |   √     |  ×  |  ×  |
 |protected     | √  |   √     |  √  |  ×  |
 |public        | √  |   √     |  √  |  √  |
   
  可访问的范围由大到小为 public > protected > default > private
   
  继承下来的方法，访问属性范围只能扩大不能缩小
   
  P.S. 内部类的访问也是相同的，外部使用来创建实例(A里面有一个类A1)是这样的A1 a1 = new A().new A1();

