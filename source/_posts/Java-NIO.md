---
title: Java NIO
date: 2017-04-05 21:08:13
tags: NIO
categories: Java基础
---

> 一个节过得都完全忘记学习了，这么嗨下去药丸，还是要加油干！@

今天写什么呢？感觉 Java NIO 在面试中的重要性还是挺高的，来学学 Java NIO 吧。

<!-- more -->

## 前言

Java NIO(New IO) 是一个可以替代标准 Java IO API 的 IO API（从 Java 1.4 开始)，Java NIO 提供了与标准 IO 不同的 IO 工作方式。Java7 则改进为 NIO.2，提供了全面的文件 IO 以及基于异步的 Channel 的 IO。

NIO 的主要特性有以下三个：

- **Channels and Buffers（通道和缓冲区）**

  标准的 IO 基于字节流和字符流进行操作的，而 NIO 是基于通道（Channel）和缓冲区（Buffer）进行操作，数据总是从通道读取到缓冲区中，或者从缓冲区写入到通道中。

- **Non-blocking IO（非阻塞 IO）**

  Java NIO 可以让你非阻塞的使用 IO，例如：当线程从通道读取数据到缓冲区时，线程还是可以进行其他事情。当数据被写入到缓冲区时，线程可以继续处理它。从缓冲区写入通道也类似。

- **Selectors（选择器）**

  Java NIO 引入了选择器的概念，选择器用于监听多个通道的事件（比如：连接打开，数据到达）。因此，单个的线程可以监听多个数据通道。



## I/O 模型

首先，需要了解 I/O MO 模型的基本概念。

何为同步？何为异步？何为阻塞？何为非阻塞？

何为同步 IO？何为异步 IO？何为阻塞 IO？何为非阻塞 IO？

这里有一篇写得很好的博文：[Java NIO：浅析 I/O 模型](Java NIO：浅析 I/O 模型)

Java NIO 实际上就是多路复用 IO。如图所示：

![](JAVA-NIO/selectors.png)

在 Java NIO 中，是通过 selector.select() 去查询每个通道是否有到达事件，如果没有事件，则一直阻塞在那里，因此这种方式会导致用户线程的阻塞。

而 Java7 的 NIO.2 则进行了改进：

- 提供了全面的文件 IO 和 文件系统访问支持
- 基于异步 Channel 的 IO



## NIO

Java NIO 由以下几个核心部分组成：

- Channels
- Buffers
- Selectors

Buffer，故名思意，缓冲区，实际上是一个容器，是一个连续数组。Channel 提供从文件、网络读取数据的渠道，但是读取或写入的数据都必须经由 Buffer。

关系可以表示为下图：![](Java-NIO/relation.jpg)



其他细节性的问题我就不写了，写来写去感觉写得没有抓住精髓，推荐一系列博文。源自并发编程网。

Java NIO Pipe
Java NIO 与 IO

[Java NIO 系列教程](http://ifeve.com/java-nio-all/)