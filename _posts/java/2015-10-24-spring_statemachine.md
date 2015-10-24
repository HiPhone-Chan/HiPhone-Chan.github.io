---
layout: post
title: Spring Statemachine简介
categories: java
---

Spring Statemachine简介
=======================
   
  Spring Statemachine(SSM)就是在Spring框架上帮我们实现了状态机的框架。对于有限状态机，可分为以下2种类型
  
* Moore状态机 - 输出只和状态有关而与输入无关
* Mealy状态机 - 输出不仅和状态有关而且和输入有关系
  
# 使用场景
 
  在以下的场景下可以考虑使用状态机
 
* 应用或者某个部分可以用状态来展示
* 希望将复杂的逻辑分解成一个个小的可管理的子任务
* 需要解决如异步回调等同步的问题

  其实我们可能在无意中已经使用了状态机的，如以下的情况
  
* 使用了一些boolean或enum的flag
* 应用中的一些变量就只用来表示状态
* 使用了很多if/else
  
# SSM使用到的相关词汇和概念 
  
## 状态机(State Machine)
   
  状态机为驱动状态(一起的还有区域、转移和事件)的主实体。
  层级状态机(Hierarchical State Machines)就是为了简化只能在一起存在的状态的设计的的概念。层级状态机允许对场景进行抽象，就像继承抽象类一样。例如一个嵌套的状态机，每一层都定义了转移条件。状态机会一层一层的往上检查守卫条件直到当前层的计算值为真。
  
## 状态（States）
   
  状态就是状态机处于哪一状态下的模型，其中伪状态(Pseudo States)是一种具有特殊含义的状态，可以表达更高的抽象逻辑。而扩展状态(Extended State)为状态机保留的一组变量，用于减少需要的状态数。
   
* 初始 - 初始状态(Initial pseudostate)表明状态机开始的状态，就是状态机运行的入口。
* 结束 - 结束状态(Terminate pseudostate)表明状态机结束的状态。
* 选择 - 选择状态(Choice pseudostate)是状态转移时的一个选择分支状态。类似于 if/elseif/else 
* 历史 - 历史状态(History pseudostate)用来获取上一个活动状态的配置。有2种类型的历史状态，shallow只能记住最顶层的状态，deep能记住子状态机的状态。
* 分支 - 分支状态(Fork pseudostate)给出了区域的入口。

![fork](http://docs.spring.io/spring-statemachine/docs/1.0.0.RELEASE/reference/htmlsingle/images/statechart7.png)

* 合并 - 合并状态(Join pseudostate)给出了区域的出口，用来将多个区域的转移合并成一个，一般情况下是用来阻塞等待某个区域来合并成目标状态。

![join](http://docs.spring.io/spring-statemachine/docs/1.0.0.RELEASE/reference/htmlsingle/images/statechart8.png)
  
## 守卫(Guard)
   
  守卫是一个动态计算的布尔表达式。守卫条件(Guard Conditions)通过对状态的变量和事件的参数来计算是否为真，来选择某个行为或者转移要不要被执行。
  
## 事件(Events)
   
  事件是用来驱动状态机的触发行为。我们可以通过如计时器等方法来触发状态机的行为，但我们可以通过事件来和状态机进行交互，也就是所谓的改变状态机状态的信号(signals)。
  
## 转移(Transitions)
   
  转移是由源状态到目标状态的一种关系。状态转移是通过触发器引起的由一种状态变成另外一种状态。
  
* 内部转移(Internal Transition)用于执行一些行为但不发生状态的转移。
* 自我转移(self-transition)是不执行进/出状态行为的内部转移。
* 本地转移(Local Transition)如果目标状态是源状态的子状态，本地转移不会引起源状态的进出；反过来，如果源状态是目标状态的子状态，本地转移不会引起目标状态的进出。
* 外部转移(External Transition)和本地转移不同，会引起进出。

![join](http://docs.spring.io/spring-statemachine/docs/1.0.0.RELEASE/reference/htmlsingle/images/statechart4.png)

## 行为(Actions)
   
  行为就是在转移时触发的动作。行为是用户实际粘合各状态的代码。当进/出状态，或进行转移时，状态机都可以执行行为。
  
## 区域(Regions)
   
  区域是状态的组合或者是一个状态机，包括状态和转移。区域(也叫原始区域orthogonal regions )给人一种在状态上进行了或(or)的感觉。每个区域其实就是一个状态机，但是同时处理2个不同的状态机比较不方便，而且实际上这些状态机是一起工作。区域这个概念就是将多种类似的状态合成一种单一状态。
   

-----
  
# 参考

* [状态机](http://baike.baidu.com/link?url=pEU1aOz0PuB_ekXbA0bBl_ovs5QxAfV7lbSJDJm2Y7q5G7st0jrP8ECtIw2nzdiwuBBob0zIboeaoZX44FEHzK)
* [Statemachine](http://docs.spring.io/spring-statemachine/docs/1.0.0.RELEASE/reference/htmlsingle/)

