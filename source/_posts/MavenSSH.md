---
title: MavenSSH
date: 2017-04-20 22:42:48
tags: Maven
categories: 教程
---

> 折腾了两天，终于弄懂了在IntelliJ idea 里用maven来配置SSH项目的流程了，记录一下，话说我是不是有一个月没写过博客了==

先说说为什么要使用maven，因为我都快被IDEA自动配置的SSH框架给弄疯了，自动配置的lib往往不全，需要一个个去找齐所有的lib。（不得不说这一点MyEclipse做得比IDEA要好，自动配置的环境往往没有缺这缺那的问题，但Eclipse的代码提示功能太弱了，写起程序来没有快感），然后我就发现了原来还有Maven这种一套pom.xml走天下的神器。

但网上的maven配置SSH框架的教程都缺胳膊少腿的，我参照多个教程才摸索出以下的内容，应该说是比较正确的和容易理解的。

<!-- more -->

## 一、安装Maven

这块不多说，网上的教程很多。如果只使用IDEA的话，因为内部集成了，所以可以跳过这一步。

![1](MavenSSH\1.png)

## 二、创建Maven项目

Maven提供了大量的模版可供使用，这里我们选择web app模版，然后设置GroupId（类似于包名结构）、ArtifactId（即项目名），然后一路next，出现finished提示，选择enable auto-import，这将允许maven即时根据pom.xml文件的修改更新配置。![5](MavenSSH\5.png)

此时的项目文件夹结构如图：

![6](MavenSSH\6.png)

## 三、调整项目结构

Maven 将项目划分为 main 和 test 两部分，main 中存放实际项目资源，test 存放测试项目资源，二者内部同时又划分为 source 和 resource 两部分，source 存放源代码，习惯上我们将该文件夹命名为 java，resource 存放资源配置文件。因此我们需要调整 Maven模版自动配置的项目结构如下，target 为输出文件夹。

![7](MavenSSH\7.png)



## 四、配置 pom.xml

前面说到我之所以选择使用 Maven 的原因在于 IDEA 自动配置 SSH 框架太难用了，Maven 将所有依赖全写在 pom.xml 文件夹中，管理起来非常方便。所以我们需要在 pom.xml 中配置 SSH 的依赖，配置文件如下。

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.yunz.bao</groupId>
  <artifactId>MavenSSH</artifactId>
  <packaging>war</packaging>
  <version>1.0-SNAPSHOT</version>
  <name>MavenSSH Maven Webapp</name>
  <url>http://maven.apache.org</url>
  <build>
    <finalName>${artifactId}</finalName>
    <resources>
      <resource>
        <directory>src/main/resources</directory>
        <filtering>true</filtering>
      </resource>
    </resources>
    <plugins>
      <plugin>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>2.3.2</version>
        <configuration>
          <source>1.7</source>
          <target>1.7</target>
        </configuration>
      </plugin>
    </plugins>
  </build>
  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <spring.version>4.0.3.RELEASE</spring.version>
    <hibernate.version>4.3.5.Final</hibernate.version>
    <struts.version>2.3.16.1</struts.version>
  </properties>

  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.10</version>
      <scope>test</scope>
    </dependency>
    <!-- 添加SSH依赖 -->
    <!-- Struts2 -->
    <dependency>
      <groupId>org.apache.struts</groupId>
      <artifactId>struts2-core</artifactId>
      <version>${struts.version}</version>
      <exclusions>
        <exclusion>
          <groupId>javassist</groupId>
          <artifactId>javassist</artifactId>
        </exclusion>
      </exclusions>
    </dependency>

    <dependency>
      <groupId>org.apache.struts</groupId>
      <artifactId>struts2-spring-plugin</artifactId>
      <version>${struts.version}</version>
    </dependency>
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>jstl</artifactId>
      <version>1.2</version>
    </dependency>

    <dependency>
      <groupId>taglibs</groupId>
      <artifactId>standard</artifactId>
      <version>1.2.5</version>
    </dependency>

    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>servlet-api</artifactId>
      <version>3.0-alpha-1</version>
    </dependency>

    <!-- 添加json支持 -->
    <dependency>
      <groupId>org.apache.struts</groupId>
      <artifactId>struts2-json-plugin</artifactId>
      <version>${struts.version}</version>
    </dependency>
    <dependency>
      <groupId>net.sf.json-lib</groupId>
      <artifactId>json-lib</artifactId>
      <version>2.3</version>
      <classifier>jdk15</classifier>
    </dependency>

    <!-- 添加Hibernate依赖 -->
    <dependency>
      <groupId>org.hibernate</groupId>
      <artifactId>hibernate-core</artifactId>
      <version>${hibernate.version}</version>
    </dependency>
    <dependency>
      <groupId>commons-dbcp</groupId>
      <artifactId>commons-dbcp</artifactId>
      <version>1.4</version>
    </dependency>

    <!-- 添加Log4J依赖  解决maven传递依赖中的版本冲突  -->
    <dependency>
      <groupId>log4j</groupId>
      <artifactId>log4j</artifactId>
      <version>1.2.15</version>
      <exclusions>
        <exclusion>
          <groupId>javax.mail</groupId>
          <artifactId>mail</artifactId>
        </exclusion>
        <exclusion>
          <groupId>javax.jms</groupId>
          <artifactId>jms</artifactId>
        </exclusion>
        <exclusion>
          <groupId>com.sun.jdmk</groupId>
          <artifactId>jmxtools</artifactId>
        </exclusion>
        <exclusion>
          <groupId>com.sun.jmx</groupId>
          <artifactId>jmxri</artifactId>
        </exclusion>
      </exclusions>
      <scope>runtime</scope>
    </dependency>

    <!-- 添加javassist -->
    <!--     <dependency> -->
    <!--         <groupId>javassist</groupId> -->
    <!--         <artifactId>javassist</artifactId> -->
    <!--         <version>3.11.0.GA</version> -->
    <!--     </dependency> -->

    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>5.1.9</version>
    </dependency>

    <!-- 添加Spring依赖 -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-core</artifactId>
      <version>${spring.version}</version>
      <scope>compile</scope>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-web</artifactId>
      <version>${spring.version}</version>
      <scope>compile</scope>
    </dependency>
    <!--     <dependency> -->
    <!--         <groupId>org.springframework</groupId> -->
    <!--         <artifactId>spring-webmvc</artifactId> -->
    <!--         <version>${spring.version}</version> -->
    <!--         <scope>runtime</scope> -->
    <!--     </dependency> -->
    <!--
        Bean Factory and JavaBeans utilities (depends on spring-core)
        Define this if you use Spring Bean APIs (org.springframework.beans.*)
    -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-beans</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <!--
        Aspect Oriented Programming (AOP) Framework (depends on spring-core, spring-beans)
        Define this if you use Spring AOP APIs (org.springframework.aop.*)
    -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-aop</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <!-- 面向切面使用aspectj, cglib的作用是当对没有实现接口的类使用aspect的时候，可以使用CGLIB
        <aop:aspectj-autoproxy proxy-target-class="true"/>
    -->
    <dependency>
      <groupId>org.aspectj</groupId>
      <artifactId>aspectjtools</artifactId>
      <version>1.6.2</version>
    </dependency>
    <dependency>
      <groupId>cglib</groupId>
      <artifactId>cglib</artifactId>
      <version>3.1</version>
    </dependency>
    <!--
        Application Context (depends on spring-core, spring-expression, spring-aop, spring-beans)
        This is the central artifact for Spring's Dependency Injection Container and is generally always defined
    -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <!--
        Object-to-Relation-Mapping (ORM) integration with Hibernate, JPA, and iBatis.
        (depends on spring-core, spring-beans, spring-context, spring-tx)
        Define this if you need ORM (org.springframework.orm.*)
    -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-orm</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <!--
        Transaction Management Abstraction (depends on spring-core, spring-beans, spring-aop, spring-context)
        Define this if you use Spring Transactions or DAO Exception Hierarchy
        (org.springframework.transaction.*/org.springframework.dao.*)
    -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-tx</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <!--
        JDBC Data Access Library (depends on spring-core, spring-beans, spring-context, spring-tx)
        Define this if you use Spring's JdbcTemplate API (org.springframework.jdbc.*)
    -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <version>${spring.version}</version>
    </dependency>

  </dependencies>
</project>
```



## 五、添加SSH支持

在前面配置pom.xml 之后，maven 自动为我们添加了相关的SSH依赖包，但我们还需要在 resource 文件中添加相关配置文件。

1. Spring配置

   新建 Spring配置文件 applicationContext.xml，因为后面需要将 Hibernate的配置置于其中，我们将文件命名为 spring-hibernate.xml。

   ![8](MavenSSH\8.png)

   然后将该文件添加到 Project structure-Modules-Spring-Fileset 中

   ![9](MavenSSH\9.png)

2. Hibernate 配置

   Project structure-Modules 点 + 号，添加 Hibernate support

   ![10](MavenSSH\10.png)

   然后点Description 右上角加号，将 spring-hibernate.xml 添加到其 Configuration 中。

   ![11](MavenSSH\11.png)

3. Struts2 配置

   新建 Struts2 配置文件 struts.xml，然后类似与前面，将配置文件添加到Project structure-Modules-Struts2-Fileset 中，同时选中struts-default.xml和struct-plugin.xml。

   ![12](MavenSSH\12.png)

   至此，SSH 的环境配置基本完成，上述配置文件的内容我省略了，就是一般SSH整合项目的配置内容。

此时项目结构如图：

![13](MavenSSH\13.png)

## 六、测试及一些问题

测试上面的框架，我们写一个简单的登录 Demo，如图。

![14](MavenSSH\14.png)

注意：在使用 Hibernate  向导自动生成 实体类时，spring-hibernate.xml 自动生成配置。

```xml
<property name="annotatedClasses">
            <list>
                <value>com.com.mahe.entity.Users</value>
            </list>
        </property>
        <property name="mappingLocations">
            <list>
                <value>classpath:com.mahe.entity/Users.hbm.xml</value>
            </list>
        </property>
```

Maven 项目中默认的资源路径根目录为 resource 文件夹，而自动生成的实体类 entity.xml 在 java entity文件夹中，所以这里 mappingLocation 的属性值是有问题的。解决方法有两种，一种是改属性值，一种是在 resource 文件夹中建立和 java entity文件夹一样的结构，将 entity.xml 文件拷贝过来。

过程中还遇到两个问题，折腾了好久，但莫名其妙又消失了，真是玄学。

运行成功。

![15](MavenSSH\15.png)

![16](MavenSSH\16.png)