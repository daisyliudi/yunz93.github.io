---
title: Java Web 错误记录
date: 2017-03-02 20:27:12
tags: Java Web
categories: Java Web
---

本文用来记录 Java Web 学习过程中遇到的错误以及相应的解决方法。

## Address already in use: JVM_Bind

### 问题描述

这个错误是在我换新电脑，把原来的项目搬移到新电脑上运行的时候遇到的。

### 问题分析

tomcat 默认端口为8080端口，很明显这个端口被占用了。

### 解决方法

cmd 中查看 8080 端口的占用情况 : `netstat -aon|findstr "8080"`

然后根据查询到的进程 PID ，找对应的进程：`tasklist|findstr "PID"`

发现  utorrent 占用了该端口，我们结束该进程就可以了。



## 