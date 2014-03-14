# Scala简介

## 什么是Scala

"Object-Oriented Meets Functional"

可以说，Scala是一门面向对象的函数式编程语言。

Scala是一种现代多范式编程语言，它试图通过简洁，优雅，类型安全的方式来表现常用编程模式的。它非常顺滑的结合了面向对象和函数式编程语言的特性。

### 它是基于JVM的

由于Scala是在JVM上运行的，所以说它天然就具有跨平台的特性。

此外，它不仅能使用Java里的内置类型，还能使用Java的各种库。如果你觉得Scala无能为力的话，借助Java也应该能实现你的需求吧。



### 它是面向对象的

在Scala里，任何东西都是对象，即使是最简单的数字`1`，这和Java等不一样。Scala通过类和特质(traits)来表示一个对象的类型和行为。

和其它很多面向对象语言一样，Scala不直接支持多重继承，它采用了类似Ruby的方式，通过混入(mixin/mix-in)来间接地实现了多重继承。

*特质（Traits）是一些字段（field）和行为（behavior）的组合，可以扩展或混入（mixin）到你的类中。*

### 它也是函数式编程语言

Scala同样也可以算是函数式编程语言，在Scala里，所有的函数（function）也是一个对象，也是类的实例。Scala也提供了很轻量的创建匿名函数的方式，并且支持高阶函数。

此外，它的函数还可以是嵌套的，并且支持currying。

像其它函数式编程语言一样，Scala也支持模式匹配。


### 它是静态类型的

Scala术语静态类型编程语言，此外，它还有很多不同于其它语言的特点：

- 泛型编程
- generic classes
- variance annotations
- upper and lower type bounds,
- inner classes and abstract types as object members
- compound types
- explicitly typed self references
- views
- polymorphic methods

Scala会让你尽量少的敲打键盘，它提供的Local Type Inference机制，使得你在编码的时候，不必为每个变量都指定类型。

总之，Scala的这些特性为安全重用抽象编程和类型安全的软件扩展提供了强大的基础。

### 它是容易扩展的

在Scala里，任何只接收一个参数的方法，都可以作为中缀操作符来使用。这句话其实也就是说，你在调用方法的时候，可以不用写`.`和`()`，比如：

```scala
scala> 1 + 1
res0: Int = 2

scala> 1.+(1)
res1: Int = 2
```

这里用到了Int类型的+方法，`1.+(1)`是比较传统的方法调用方式，`1 + 1`则可以认为是精简的中缀操作符方式。


关于Scala的更多的信息，可以参考它的主页：<http://www.scala-lang.org/>

## Scala的历史


## Scala的特点


## 我能用Scala做什么
