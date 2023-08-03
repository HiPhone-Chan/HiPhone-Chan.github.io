---
layout: post
title: 关于byte数组和String相互转化
categories: java
---

关于byte数组和String相互转化
=======================

  在Java开发时有时候会遇到将byte[]转化为String，再转化为byte[]的情况，很多时候可能是用到以下的代码。
  
```java
  byte[] bytes = {...};
  String str = new String(bytes);
  str.getBytes();
```
   
  这在传输一般的ASCII字符时是没问题的，但遇到byte的int值为负数的情况就不好用了，这是因为再转化为String的时候存在字符的转换，再String内部是以char存储的，但并不是所有的byte组合都可以映射为char，此时我们通过Base64转码来解决这种问题(jdk,apache-common有提供这种工具类)。
  
  
```java
  byte[] bytes = {...};
  String str = new String(Base64.encodeBase64(bytes));
  Base64.encodeBase64(str.getBytes());
```