---
layout: post
title: apache zest简介
categories: java
---

apache zest简介
==============

  Zest是一个以领域(domain)为中心的应用开发框架，涉及到面向切面(AOP)，依赖注入(DI)和领域驱动设计(DDD)等概念。它用java平台实现了面向组合编程。Zest前身是Qi4j，其中Qi就是中文的气，意为给java注入新的活力(Energy4Java)。
  
  Zest声称不是框架，是为我们提供一个新思路去写代码，为了摆脱框架的特定只是，Zest使用了很多注解，并没有使用新的语言、复杂的结构、工具，甚至连XML也没有用。
  
# 面向组合编程(Composite Oriented Programming)

  面向组合里面有一些概念是面向对象里面没有的。
  
## 依赖内容的行为(Behavior depends on Context)

  面向对象编程的模型想让我们相信对象是一个简单的模型，但很多对象拥有的生命周期往往没有这么简单。就像蛋->鸡->鸡肉，更进一步的，事物的组成会随着时间流逝而改变。
  
  在编程世界里，我们经常面对各种变化的需求。
  
## 解耦(Decoupling is a virtue)
  
  解耦其实比我们平时的想象更重要。在面向对象中，如果一个类和其他类没什么关系的话，它是很容易被重用的。但当类里面又引用另外的类，类又引用其他类，那这个类的可重用性就大大降低了。
  由于面向对象编程限制了领域类的重用，导致我们需要每次重头开始重写领域模型。
  
## 关注业务规则(Business Rules matters more)

  我们都喜欢做核心的东西，因而我们往往觉得底层代码，框架代码比简单的领域模型更加重要。但实际上领域模式才是反映需求和解决问题的。框架架构仅仅是为了完成任务时用到的东西。如果我们能聚焦于业务规则和领域模型(不要担心一些诸如持久化、事务、安全、框架等架构性的问题)，我们会更有生产力。但这对我们来说是有难度的，因为我们往往被困于一些框架里面和领域模型无关的限制。

## 多使用接口(Classes are dead, long live interfaces)

  在面向组合的新思想下，类变成了实现行为的混入(mixin)的组合，不再具有任何的行为，行为都定义在接口中。
  
  -----
  
# 涉及到的相关词汇

# 应用(Application)
  
  应用是Zest最高级别的，在Zest运行时实例里面有且只有一个。应用包含了层的信息。
  
# 层(Layer)

  层是用于应用里面的分层设计。层只能访问更低级别的层，不能访问高于或相同级别的层。

# 模块(Module)

  模块用于定义组合的范围，不可视的组合不能被其他模块使用。
    
## 组合(Composite)

  组合是组合类型(Composite Type)的一个实例。组合类型就是在OOP里面所说的对象，但我们往往将类当做对象了。

# 架构(Structure)

  Zest应用的架构是在计算机科学中是很常用的，架构如下

* 应用包含层
* 层包含模块
* 模块包含组合

## 组合块(Fragment)
  
  组合块就是组合中某部分行为的实现，包含以下4种类型
  
* 混入(Mixin) - 混入类型(MixinType)用来定义组合中暴露的方法，用接口来表示。而混入则是混入类型的实例，提供状态展示。
* 约束(Constraint) - 约束是一种校验器，用于对调用方法时对参数，返回值等的校验。
* 关系(Concern) - 关系是Mixin的一个拦截器，一般用于事物处理，用户安全等，最好不要在关系中产生副作用。
* 副作用(SideEffect) - 副作用也是Mixin的一个拦截器，但它是在方法执行完后执行的，因而它不能改变方法的入参和返回值。

  上面的约束，关系和副作用都是修饰器(Modifier)，是对方法调用的无状态拦截器。

# 组合的基本类型(Composite Meta Type)

* Entity Composite - 就是实体(Entity)，用于持久化，由于它只的范围在UnitOfWork里面，因而是线程安全的。
* ValueComposite - 当做原始类型的值来使用，是内容特点为不可改变的；能作为 Property的类型使用
* Service composite - 当做服务类来使用
* Configuration Composite (subtype of EntityComposite) - 为服务读配置
* TransientComposite - 主要特点为不能持久化/序列化；不能作为 Property的类型使用
  
  -----
  
# 参考

* [zest](http://zest.apache.org/java/latest/index.html)

