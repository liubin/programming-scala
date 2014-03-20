# Actor并发编程

一般来说有两种策略用来在并发线程中进行通信：共享数据和消息传递。

基于共享数据的有信号量（semaphores）等，在C下做过并发程序的可能都会比较熟悉这个概念。Java程序员也可以在`java.util.concurrent`包下知道到同步、锁相关的数据结构。

使用共享数据方式的并发编程面临的最大问题就是数据条件竞争（data race）、思索以及可扩展性问题。

消息传递则是另一种在线程间进行同步协调的方式。消息传递机制相对于共享数据的并发模型来说最大的优点就是不会产生数据竞争状态（data race）。比如在Java里，如果多个线程想要访问通过一个对象的数据的时候，如果不适用同步或者加锁机制，就有可能导致读取了被修改后的数据（也称作数据可见性问题），或者修改了不应该修改的变量，甚至死锁等问题。而如果线程间通信是通过消息传递来完成的话，而且传递的消息都是不可变的（immutable），那么就不会发生上面提到的问题。

消息传递机制也并非完美无缺的。由于消息数量巨大，很可能造成通信负荷过高。进程可能会不停的创建消息并发送，系统会不断的把消息进行缓存（buffered），等待其它进程的读取。如果消息体过大的话，对系统的压力也会增加。而如果需要多个线程使用同一个很大的对象的话，那么也许数据共享也许是个好选择。

实现消息传递也有两种类型：基于channel的消息传递和基于Actors的消息传题系统。

在基于channel的消息传递系统中，消息会被发送到由进程（process）共享的通道（channels）里，其它进程则可以从这个通道里读取消息。基于channel的系统实例有Message-Passing
Interface (MPI)，以及Communicating Sequential Processes。

另一种消息传递的实现方式是基于Actor（也可以叫做Erlang风格进程）的并发模型。在这种系统里，消息会被直接发送到actors，不需要建立中间通道来在不同进程间传递消息。

关于Actor我们会在后面的小节进行说明。

## CSP（Communicating sequential processes）

在计算机科学领域，Communicating Sequential Processes (CSP，*注 3*)是一种用于描述并发系统交互模型的形式语言，最早起源于Tony Hoare（图灵奖获得者、著名的排序算法快排的作者）在1978年发表的论文（*注 4*）。

和上面的Actor模型不同，CSP采用固定数量的sequential processes并连接到固定的拓扑结构上，并采用同步消息传递机制。

CSP用两个基本类型来描述并发系统：事件和进程（Primitive processes）。

- 事件

事件用来表示通信或交互行为。它具有不可分割性和瞬时性。事件可能是原子名称（atom，例如：开、关），也可以是组合名称（compound names，比如valve.open、valve.close），或输入输出事件（mouse?xy、screen!bitmap）

- 进程（Primitive processes）

进程用来表示基本行为，比如它可以是STOP、SKIP等。

CSP定义了很多运算符，比如Prefix，Deterministic Choice、Nondeterministic Choice、Interleaving、Interface Parallel、Hiding，CSP利用这些原语来描述系统中进程和事件的关系。

CSP采用基于channels的消息传递（message passing）机制，很多语言都采用了这种设计，比如occam（注意：不是OCaml）及Limbo，其中最著名的就应该算是Go了。Go语言引入channel来在Go routine之间进行通信，Go routine和channel也是Go并发编程的基石。

## Actor模型的特点

Scala没有像Go那样采用CSP，而是基于Actor来实现其并发编程模型（或理论、框架），也是其很多具体实现的理论基础。

Actor模型（*注 1*）最初于1973由等Carl Hewitt等人提出（*注 2*），是一个并行计算的数学模型。

Actor是计算机科学领域中的一个并行计算模型，它把actors当做通用的并行计算原语：一个actor对接收到的消息做出响应，进行本地决策，可以创建更多的actor，或者发送更多的消息；同时准备接收下一条消息。

在Actor理论中，一切都被认为是actor，这和面向对象语言里一切都被看成对象很类似。但包括面向对象语言在内的软件通常是顺序执行的，而Actor模型本质上则是并发的。

一个actor是一个计算实体，它会对接收到的消息做出响应，并且可以并发的完成下面的工作。

- 向其它actors发送有限数量的消息
- 创建有限多个新的actors
- 指定用于接收下一个消息的行为。

上述行为可以是并行进行的，而且顺序也不是固定的。

在Scala里，Actor也有两种实现：标准库里的`scala.actors`包和Akka（*注 5*）项目。Akka是一个为在JVM平台上开发高并发、分布式、可容错、易扩展、事件驱动的系统而打造的工具集和运行时（runtime）环境。它支持Scala和Java两种编程语言。

不管是哪种实现方式，在大多数的JVM上，Scala里的actor和Java线程想比都是非常轻量的。Actor和线程的对比我们在下一节会详细讲述。

*注 1：<http://en.wikipedia.org/wiki/Actor_model>*  
*注 2：Carl Hewitt; Peter Bishop; Richard Steiger (1973). A Universal Modular Actor Formalism for Artificial Intelligence. IJCAI.*  
*注 3：<http://en.wikipedia.org/wiki/Communicating_sequential_processes>*  
*注 4：Hoare, C. A. R. (1978). "Communicating sequential processes". Communications of the ACM 21 (8): 666–677. doi:10.1145/359576.359585.<http://dx.doi.org/10.1145%2F359576.359585>*  
*注 5：<http://akka.io/>*
