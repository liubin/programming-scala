# Scala基础

## 安装Scala

首先，需要去官网<http://www.scala-lang.org/download/>下载最新的安装包，目前最新版本为2.11.0-RC1。

在下载Scala之后，我们需要简单的"安装"一下。这里之所以在"安装"上加上双引号，是因为所谓的安装，也只是简单地拷贝和设置环境变量。

比如我在Mac下用Chrome下载Scala之后，会将最新版本的Scala文件保存到`~/Downloads/scala-2.11.0-RC1.tgz`，我们需要将它解压后保存到某处。

这里我们将Scala保存到`/usr/local/share/scala`：

```shell
$ tar zxf scala-2.11.0-RC1.tgz
$ sudo cp -r scala-2.11.0-RC1 /usr/local/share/scala
```

仅仅这样还是不够的，我们还需要设置一下环境变量。我们可以通过编辑自己的`profile`文件来实现，比如我的话可以编辑`~/.profile`，（在这个文件的最后）加入下面两行

```
export SCALA_HOME=/usr/local/share/scala
export PATH=$PATH:$SCALA_HOME/bin
```

在编辑完`profile`文件之后，再执行`source`命令新设置的环境变量生效：

```shell
$ source ~/.profile
```

不出意外，这时候我们就应该可以使用`scala`命令了：

```shell
$ echo $SCALA_HOME
/usr/local/share/scala
$ scala -version
Scala code runner version 2.11.0-RC1 -- Copyright 2002-2013, LAMP/EPFL
```

## Scala开发IDE

工欲善其事，必先利其器。同样，编程的话需要需要一个MacBook，需要一个大显示器，需要一个HHKB，需要一个15平米的房子就我一个人可以大声的放凤凰传奇。。。

上面所说的都需要money，但是是装个好用的IDE或者编辑器却很便宜，而且大部分还是免费的。

Scala可以使用的IDE很多，比如基于Eclipse的Scala IDE(<http://scala-ide.org/>)，或者IntelliJ IDEA + Scala插件(<http://www.jetbrains.com/idea/>)，以及NetBeans IDE + Scala插件(<https://netbeans.org/>)。

这里我们使用Scala IDE。

首先，从官网下载这个软件，下载网址为：<http://scala-ide.org/download/sdk.html>。

目前Scala IDE的最新版本为3.0.2 Release，面向的是2.10 版本的Scala，并且基于Eclipse 4.3(Kepler)。目前Scala IDE提供了供Windows、Mac或者Linux上使用版本，并且每个版本都能支持32位或者64位的操作系统。

如果你想运行Scala IDE，那么还需要安装JDK 6或者JDK 7。

在Scala IDE的下载页面，这里我们选择64位的Mac OS X。这个文件较大，有178M，如果网速很慢的话，估计会花费很长时间，需要耐心的等待。或者你可以在它下载的时候，顺便将本书翻到后面章节浏览一下。

## 启动Scala解释器

在正式编写大规模的Scala之前，我们先尝试使用Scala解释器进行交互式的操作，这样你不仅不需要编译就可以执行Scala代码，还能实时进行执行结果的确认，比如看看每次执行一条语句后的返回值以及返回值的类型等。

下面我们先来启动Scala解释器

```
$ scala
Welcome to Scala version 2.11.0-RC1 (Java HotSpot(TM) 64-Bit Server VM, Java 1.7.0_45).
Type in expressions to have them evaluated.
Type :help for more information.

scala>
```
怎么样，如果你熟悉Ruby或者Python这类脚本(当然，也可以叫做动态语言，面向对象语言等)语言的话，一定很熟悉这种交互式操作借口吧。每一行开头的`scala>`就是解释器等待输入的修饰符。

在继续之前我想先说一下的是要退出Scala解释器，可以使用命令`:q`，它是`:quit`的缩略版。不过`CTRL + C`和`CTRL + D`也可以达到同样的效果。

在了解了如何启动和退出Scala解释器之后，我们还是先来个最经典的打印`Hello World`操作吧：

```scala
scala> println("Hello, world!")
Hello, world!

```

再来个`1 + 1`：

```
scala> 1 + 1
res1: Int = 2

```

我想大家都能从上面的输出能猜出一些端倪吧。比如上面的输入`res1: Int = 2`，意思就是结果为`Int`型，其值为`2`。

等等，那`res1`是什么呢？是变量名？试试就知道了。

```
scala> println(res1)
2

scala> res1
res3: Int = 2
```

不错，确实在Scala解释器里，我们得到了一个变量`res1`，而且它的值就是`2`。

那上面第二个语句呢？怎么又多了一个变量`res3`，那肯定还有一个变量`res2`喽？我们可以继续试验一下：

```
scala> println(res2)
()

scala> println(res4)
()
```

从上面的结果我们不难推断出，在调用`println(res1)`的时候，除了打印出`res1`的值`2`之外，同时将`println`的调用结果赋值给了`res2`，它的值为`()`。

在我们执行`1 + 1`的时候，生成的变量（严格说事常量，val类型，你不能修改它的值。）是`res1`，那么之前的打印`Hello World`返回值是`res0`么？

```
scala> println(res0)
()

```

不错，正是如此。

尽管我们之前将`res1`等称为变量，实际上是有点不合适的，因为这些变量都是只读的，在Scala里，它们属于`val`类型的"变量"。

```
scala> res1 = 2
<console>:8: error: reassignment to val
       res1 = 2
            ^
```

关于`val`，你现在只需记住的就是它是只读的。和它相对的是`var`保留字（或者叫关键字），这个保留字用来声明一个可变的变量。


## 编译Scala文件并运行

除了在解释器里执行Scala代码，我们当然也可以将代码保存为文件编译并执行，这个过程很像Java。


比如我们准备如下的源文件：

*代码清单1：HelloWorld.scala*

```
object HelloWorld {
  def main(args: Array[String]) {
    println("Hello, world!")
  }
}

```

非常类型Java，Scala用来编译源文件的命令是`scalac`，而用来运行编译后class文件的命令就是`scala`。

```shell
$ scalac HelloWorld.scala

$ scala HelloWorld
Hello, world!
```

默认的class文件会被保存到当前目录，你可以通过`scalac -d`来将class文件保存到其它文件夹。

同时如果你在通过`scala`运行Scala程序的时候，也可以像Java那样通过`-cp`选项来指定class文件的加载路径。


## 将Scala当做脚本来用

我们也可以将Scala程序当做脚本来运行。比如同样是打印"Hello World"，我们可以写出下面这样的脚本：

```shell
#!/bin/sh
exec scala "$0" "$@"
!#
object HelloWorld extends App {
  println("Hello, world!")
}
HelloWorld.main(args)
```

下面就是我们运行这个脚本文件的例子：

```shell
$ chmod +x helloworld.sh

$ ./helloworld.sh
Hello, world!
```
