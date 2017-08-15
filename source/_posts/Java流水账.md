---
title: Java流水账
date: 2017-03-30 16:57:47
tags: Java
categories: Java基础
---

> 学习Java的过程中，经常会有一些细枝末节的概念性问题，很杂但经常很重要，以流水账的形式记录下来，本文长期更新。



## == 、equals以及hashcode

`==` 比较的是两个对象在 JVM 中的地址 。

`equals` 用于比较两个对象的值是否相同【不是比地址】，可以通过重写 `equals` 方法，来设定相等的标准。

`Object` 类中的 `equals` 方法和 `==` 是一样的，没有区别，而 String 类，Integer 类等等一些类，是重写了 equals 方法，才使得 `equals` 和 `==` 不同，所以，当自己创建类时，自动继承了 Object 的 equals 方法，要想实现不同的等于比较，必须重写 equals 方法。

当 `equals` 方法被重写时，通常有必要重写 `hashCode` 方法，以维护 `hashCode` 方法的常规协定，该协定声明相等对象必须具有相等的哈希码。

[参考：hashCode 与 equals 的区别与联系](http://blog.csdn.net/afgasdg/article/details/6889383)

Hashtable 实现一个哈希表，为了成功地在哈希表中存储和检索对象，用作键的对象必须实现 hashCode 方法和 equals 方法。必须保证 equals 相等的对象，hashCode 也相等。因为哈希表通过 hashCode 检索对象。