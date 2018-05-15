## 1 如何理解Java平台

1. 宣传中的样子

```
Write once, run anywhere
```

1. 吐槽时的样子

```
形式主义的语法
```

1. 典型回答
    1. 书写一次，到处运行(Write once, run anywhere) -- 跨平台
    1. 垃圾收集(GC, Garbage Collection) -- 省心

1. 基本概念
    1. **JRE** Java运行环境，包含 JVM 和 Java 类库 以及一些模块
    1. **JDK** 是 JRE 的超集，提供了更多工具，例如 编译器、各种诊断工具
    1. **解释执行** 
        * Java 源码通过 javac 编译成为`字节码`(bytecode)，在运行时通过 JVM 的解释器将字节码转为机器码
        * 常见的 JVM 例如 Oracle JDK 提供的 Hotspot JVM ，都提供了 JIT(Just-In-Time) 编译器，也就是通常所说的『动态编译器』
        * JIT 能在运行时将热点代码编译成机器码，此时这部分热点代码就属于**编译执行**，而不是解释执行

1. 理解思路
    1. Java 语言特性，包括 泛型、Lambda、面向对象、反射 等语言特性
    1. 基础类库，包括 集合、IO/NIO、网络、并发、安全 等基础类库
    1. 常用类库
    1. JVM 的基础概念和机制
        1. Java 类加载机制，常用版本 JDK 内嵌的 Class-Loader，例如 Bootstrap、Application 和 Extension Class-Loader
        1. 类加载的大致过程：加载、验证、链接、初始化
        1. 自定义 Class-Loader 等
    1. 垃圾收集的基本原理
    1. 常见的垃圾收集器，例如 SerialGC、Parallel GC、CMS、G1 等，已经各自使用的场景
    1. JDK 工具和 Java 领域其他工具，例如 编译器、运行时环境、安全工具、诊断和监控工具等
        * 辅助工具，例如 jlink、jar、jdeps 等
        * 编译器，例如 javac、sjavac
        * 诊断工具，例如 jmap、jstack、jconsole、jhsdb、jcmd 等
        * Java/JVM 生态，例如 Java EE、Spring、Hadoop、Spark、Cassandra、Elastic Search、Maven 等

1. 补充
    1. 通常把 Java 分为『编译期』和『运行时』
        1. 编译期
            * 这里的编译是将『源代码』转为『字节码』
            * 通过『字节码』和 JVM 这种跨平台的抽象，屏蔽了操作系统和硬件的细节，是实现『Write onec, run anywhere』的关键
        1. 运行时
            * JVM 通过 Class-Loader 加载字节码，解释或者编译执行，例如 JDK 8 实际是解释+编译的『混合模式』(-Xmixed)
            * 通常运行在 server 模式的 JVM ，会进行上万次调用(收集足够的信息)以进行高效编译
            * client 模式的门限是 1500 次
            * Oracle Hotspot JVM 内置了两个 JIT compiler
                * C1 对应 client 模式，适用于普通 Java 桌面应用
                * C2 对应 server 模式，适用于长时间运行的服务器端应用
                * 默认采用的是『分层编译』(TieredCompilation)
            * 新的编译方式 AOT(Ahead-of-Time Compilation) 直接将字节码编译成机器代码，避免 JIT 预热等各方面的开销
                * Oracle JDK 9 就引入了实验性的 AOT 特性
    1. JVM 启动时可以指定不同的参数对运行模式进行选择
        1. `-Xint` 指定 JVM 只进行解释执行，不对代码进行编译，抛弃 JIT 带来的性能优势
        1. `-Xcomp` 指定 JVM 关闭解释器(interpreter)
            * `-Xcomp` 未必是最高效的选择，该参数会导致 JVM 启动变慢，有些 JIT 编译器优化方式，如分支预测，在不进行 profiling 的情况下往往不能进行有效优化
    1. JVM 作为一个强大的平台，本质上合规的字节码都可以运行，由此产生了如 Clojure、Scala、Groovy、JRuby、Jython 等大量 JVM 语言

