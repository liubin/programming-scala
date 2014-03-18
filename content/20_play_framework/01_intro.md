# Play Framework简介

在正式开始使用Play之前，我们先来看看什么是Play，以及它的特点。

## 什么是Play Framework

Play是一个开源的Java和Scala的Web开发框架，它采用MVC（Model-View-Controller）架构，并遵循约定优于配置（convention over configuration）原则。

Play基于Akka开发，这也使得我们更容易开发可预测的和最小资源消耗（CPU，内存，线程）的高并发且可扩展的应用程序。

Play在2007年之前就开始开发，第一次正式发布代码是在2008年5月。Play从1.1版本就开始支持Scala语言，将使用的Apache MINA库替换为JBoss Netty库。2.0版本的Play在2012年3月发布，其核心也用Scala进行了重写，构建和部署组件也迁移到了SBT，模板则用Scala替换了Groovy（*注 1*）。现在Play的最新版本为2.3.0。

Play深受Ruby on Rails和Django等的影响，用它编写的Java应用可以认为是弱Java EE性的，它并没有那么多Java EE的约束，想必用Java编写的Web应用，Play会更简单更灵活。用Play编写的应用除了可以运行在Netty服务器上，还可以打包为WAR文件，放到任何Java EE应用服务器上运行。

## Play Framwwork的特点

Play的主要特点有下面这些：

- 丰富的模块
  - 基于Scala的模板引擎
  - RESTful 路由
  - CRUD支持，方便操作model对象
  - 基于注解（annotations）的验证框架（validation framework）
  - job scheduler
  - 简单的SMTP邮件服务
  - JSON/XML解析及marshaller
  - 基于JPA的持久层
  - 嵌入式数据库，方便开发和测试
  - 测试框架支持
  - 支持不同环境的配置


- 高可用性和扩展性
 - 无状态Web
 - 非阻塞I/O操作
  由于底层采用了JBoss Netty作为Web服务器，它不像传统的Java EE框架/Servlet那样，为每一个HTTP请求都创建一个线程。在Play里，你可以采用异步的方式来进行耗时较长的处理。
 - 基于Akka
 - 支持实时应用
  Websockets, Comet, EventSource等。
 - 编译后执行
 - 类型安全（得益于Scala）


- 对开发者友好
 - 功能强大的控制台工具
 - 采用sbt进行依赖管理、构建（build）和部署
 - 集成到Eclipse和IntelliJ IDEA
 - 内建测试工具


- 现代Web框架
 - 资源编译（采用CoffeeScript，LESS等）
 - RESTful


- 良好的生态系统
 - 复用Java的生态系统
 - 使用Maven中心仓库（Maven Central libraries）
 - 大量的Play插件
 - 活跃的Play社区

*注 1：Groovy是基于JVM的面向对象动态语言，也可以称为脚本语言，其主页为<http://groovy.codehaus.org/>*  
