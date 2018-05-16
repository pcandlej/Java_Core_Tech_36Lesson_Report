## 2 Exception 和 Error 的区别

1. 典型回答

* `Exception` 和 `Error` 继承 **Throwable** 类
    * 只有继承 **Throwable** 才能被**抛出**（throws）或**捕获**（catch）
* `Exception` 和 `Error` 体现了 Java 对不同异常情况的分类
    * `Exception` 只正常运行中可预料的意外情况，可能并应该被捕获和处理
    * `Error` 指正常情况下，不大可能出现的情况，可能导致程序（JVM 自身）处于异常的、不可恢复的状态，例如 OutOfMemoryError 之类
* `Exception` 分为**可检查**（checked）异常和**不检查**(unchecked)异常
    * 可检查异常在源代码里必须显示地捕捉处理
    * 不检查异常指运行时异常，例如 NullPointerException、ArrayIndexOutOfBoundsException 之类

1. 分析

* 理解Throwable、Exception、Error的设计和分类

```yaml
Object.Throwable:
  Error:
    LinkageError:
    - NoClassDefError
    - UnsatisfiedLinkError
    - ExceptionInInitializerError
    - ...
    VirtualMachineError:
    - OutOfMemoryError
    - StackOverflowError
  Exception:
    IOException: []
    RuntimeException:
    - NullPointerException
    - ClassCastException
    - SecurityException
    - ...
```

* 理解 Java 语言中操作 Throwable 的元素和实践

1. 补充

```java
try {
    // 业务代码
    // ...
    Thread.sleep(1000L);
} catch (Exception e) { // 尽量不要捕获 Exception 异常
    // Ignore it // 不要生吞异常
}
```

```java
public void readPreferences(String fileName) { // 如果 fileName 是 null ，程序会抛出 NullPointerError
    // ... perform operations ...
    InputStream in = new FileInputStream(fileName);
    // ... read the preferences file ...
}
```

```java
public void readPreferences(String fileName) {
    Objects.requireNonNull(fileName);
    // ... perform operations ...
    InputStream in = new FileInputStream(fileName);
    // ... read the preferences file ...
}
```
