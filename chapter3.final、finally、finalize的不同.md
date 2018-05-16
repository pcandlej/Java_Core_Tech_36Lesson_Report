## chapter3.final、finally、finalize的不同

1. 典型回答
    1. final 可修饰 类、方法、变量
        * 修饰类 class不能被继承
        * 修饰方法 方法不能被重写(override)
        * 修饰变量 变量不能被修改
    1. finally 是 Java 保证重点代码一定被执行的机制
        * 可以用 try-finally 和 try-catch-finally 来执行类似关闭 JDBC 连接、保证释放锁等动作
    1. finalize java.lang.Object 的一个方法，设计目的保证对象在被垃圾手机前完成特定资源回收，已经不建议使用

