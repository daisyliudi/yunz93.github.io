---
title: Java 实习面试总结
date: 2017-03-26 12:49:46
tags: Java
categories: 面试
---

这是知乎专栏[【编程之路】](https://zhuanlan.zhihu.com/p/25725929)的一篇文章，感觉不错，收录一下。

看完之后，深觉自己还有很多不足，最近的学习也很乱，感觉没有章法。后面会按这个列表逐一地解决。

<!-- more -->

## Java 基础

- java 内存模型


- 多态（重载重写）
- object 方法
- 类访问权限
- sleep、notify、wait 联系、区别
- String、stringbuffer、stringbuilder 联系、区别、源码
- Volatile 原理、源码、与 syn 区别
- 线程间通信方式
- 线程的各种状态
- 等等等等



## 集合框架

### List

- ArrayList
- LinkedList
- Vector

三者区别，联系，源码

### Set

- HashSet
- LinkedHashSet
- TreeSet

基于什么实现，内部数据结构，适用场景，源码

### Map

- HashMap
- weakHashMao
- LinkedHashMap
- TreeMap

HashMap 与 hashtable 的区别

内部实现原理、源码、适用场景



## 并发包

### ConcurrentHashMap

- 原理、源码、与 hashmap 的区别

### CopyOnWriteArrayList (set)

- 什么情况加锁、什么情况不加锁、适用场景

### ArrayblockingQueue (Linked)

- 两者区别，take、put、offer、poll 方法原理、源码

### AtomicInteger (long boolean)

- 功能

### CountDownLatch

- 功能、场景

### CyclicBarrier

- 功能、场景

### FutureTask (Callable)

- 源码、场景

### ReentantLock

- 与 syn 的区别、好处、场景

### Condition

- 与 wait、notify 的区别、好处

### Semaphore

- 好处、场景

### ReentrantReadWriteLock

- 读写分离的好处、适用场景、源码

### Executors

- 线程池种类、各个作用、适用场景

### ThreadPoolExecutor

- 重载方法的参数、各参数作用、源码



## 虚拟机

### JVM 五大区

- 每个区的存储、作用

### JVM 内存模型

- 类加载机制
- 双亲委派模型

### 垃圾收集器

- 常用 gc 算法
- 收集器种类、适用场景
- fullGC、MinorGC 触发条件

### JVM 优化

- 可视化工具使用

- 日志查询

- 各项参数设置

- 四种引用

  ​

## IO 流

### BIO

- 字节流：类型、适用场景
- 字符流：类型、适用场景

### NIO

- 类型、适用场景
- 三大组件的联系、使用
- 内存情况



## 大数据

- zookeeper
- kafka
- redis 集群
- storm
- hadoop
- spark
- solr cloud

挑一两个组件深入理解下就好



## 数据库

### 三范式

### 主从复制

- 原理、实现

### 读写分离

- 原理、实现

### 事务

- 类型
- 使用
- 可能引起的问题

### 存储引擎

- InnoDB
- MyISAM

区别、联系、锁机制、适用场景

### 索引

- 类型
- 使用
- 什么样的字段适合做索引

### SQL 优化



## web

### Tomcat

- 结构、流程、源码

### Servlet

- 生命周期
- 三种实现方式

### springMVC

- 使用
- 请求流程

### spring

- IOC/AOP 原理、源码、联系
- 两种动态代理实现

### mybatis

- 使用
- 、$ 区别
- 一级、二级缓存



## 设计模式

- 单例模式
- 工厂模式
- 观察者模式
- 适配器模式
- 模仿方法模式
- 策略模式
- 责任链模式
- 装饰者模式

常用的八种掌握就行，原理，使用
单例、工厂、观察者重点



## 数据结构

### 二叉树

- 平衡二叉树
- 二叉查找树
- 红黑树
- 完全二叉树
- 满二叉树

概念、适用场景、时间复杂度、好处坏处

### B 树

- B-Tree
- B+Tree

两者的联系、区别、适用场景



## 算法

- 直接插入排序
- 二分插入排序
- 希尔插入排序
- 冒泡排序
- 快排
- 选择排序
- 堆排序
- 归并排序

1. 各种排序的思想
2. 实现复杂度
3. 稳定性如何
4. 可以手写



## 网络

### TCP

- 三次握手、四次挥手、各种状态、状态改变
- 和 UDP 的区别

### IO 模型

- 同步、异步、阻塞、非阻塞概念
- 模型种类、各自特点、适用场景
- 如何使用



## Linux 基础

- 常用命令
- 管道符
- 查看日志相关命令
- CPU 使用命令