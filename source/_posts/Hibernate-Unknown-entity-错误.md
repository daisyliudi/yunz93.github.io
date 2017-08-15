---
title: Hibernate Unknown entity 异常
date: 2017-04-14 00:19:51
tags: Hibernate
categories: Java Web
---

> Hibernate 版本更新有点快啊，还老是改API，版本兼容问题很严重啊！

<!-- more -->

今天使用 Hibernate 时报了一个这样的错误org.hibernate.MappingException: Unknown entity: com.mahe.entity.Users，Users 是项目的一个实体，也就是说映射不成功，然后我就去搜呗。

所有前面的回答都是注解的包导入错误什么的，可我没有使用注解啊，然后第二个可能性就是没有在 hibernate.cfg.xml 文件中加载 Users.hbm.xml。

我查了下我的 hibernate.cfg.xml，发现使用了 mapping resource 加载了，并且文件名也没有问题，然后我估计就是 Hibernate 版本的问题了，因为前面也遇到了Hibernate 版本导致的问题，因为 Intellij Idea 默认下载的是最新的5.1.5 版本的。

然后在知乎查到了解决方法 [https://www.zhihu.com/question/35419808](https://www.zhihu.com/question/35419808) 
好吧就是加上 addClass()，但是很不解，难不成我的 mapping resource 不起作用？于是我就从 hibernate.cfg.xml 中把这句话删了，加上 addClass()，发现能运行成功！我去 mapping resource 真不起作用。。。 
那么5.1版本怎么使用 resource 方式加载呢？
[http://jishu.y5y.com.cn/sinat_32873711/article/details/52979914](http://jishu.y5y.com.cn/sinat_32873711/article/details/52979914) 
于是按照这位博主的方法，重新换了获取 Seeeion Factory 的方法

```
StandardServiceRegistry serviceRegistry = new StandardServiceRegistryBuilder()
.configure().build();
// 创建会话工厂
sessionFactory = new MetadataSources( serviceRegistry ).buildMetadata().buildSessionFactory();
// 会话对象
session = sessionFactory.openSession();123456123456
```

这次删除 addClass 使用 mapping resource 总算成功了。



总结 org.hibernate.MappingException: Unknown entity 异常可能的原因：

1. 如果采用的是注解方式

- 实体上有没有添加 Entity 注解
- 实体所在 package 是否在扫描路径内
- 所使用的 SessionFactoryBean 是否支持注解方式，Spring 3.X 需要注意

2. 如果采用的是 XML 方式

- 实体对应的 hbm 文件是否映射正确
- 是否将 hbm 文件作为 resource 添加到 hibernate 主配



不过最保险的，还是使用低版本的，因为你不知道还会遇见什么坑，所以我决定换成4.1.4了。