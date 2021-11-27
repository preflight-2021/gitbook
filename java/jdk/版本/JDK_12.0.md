# JDK_12.0

发布时间：2019-03-19

代号：none

重大改变：Switch表达式、Java微测试套件（JMH）、RedHat领导开发的Shenandoah垃圾收集器。



## 版本新特征

### 1，低暂停延时的垃圾收集器 (实验版)

​	添加一个名为 Shenandoah 的新垃圾收集 (GC)算法，该算法通过与正在运行的 Java 线程并发执行回收工作来减少 GC 暂停时间。

​	Shenandoah 的暂停时间与堆大小无关，这意味着无论堆大小是 200 MB 还是 200 GB，都将拥有相同的暂停时间。



### 2，微基准测试套件

​	在 JDK源代码中添加了一组基本的微基准测试套件，使得开发人员无论运行现有的微基准测试或者创建新的微基准测试都变得十分便利。



### 3，Switch表达式

​	这是一个预览版语言特性。通过对 switch 语法进行了扩展，使其不仅可以作为语句（statement），还可以作为表达式（expression），并且两种形式都可以	使用“传统的”或“简化的”语法用于作用于不同的范围或者控制执行流。

​	老的写法

```java
switch (day) {
    case MONDAY:
    case FRIDAY:
    case SUNDAY:
        System.out.println(6);
        break;
    case TUESDAY:
        System.out.println(7);
        break;
    case THURSDAY:
    case SATURDAY:
        System.out.println(8);
        break;
    case WEDNESDAY:
        System.out.println(9);
        break;
}
```

​	新的写法

```java
switch (day) {
    case MONDAY, FRIDAY, SUNDAY -> System.out.println(6);
    case TUESDAY                -> System.out.println(7);
    case THURSDAY, SATURDAY     -> System.out.println(8);
    case WEDNESDAY              -> System.out.println(9);
}
```

​	带返回值：

```java
int numLetters = switch (day) {
    case MONDAY, FRIDAY, SUNDAY -> 6;
    case TUESDAY                -> 7;
    case THURSDAY, SATURDAY     -> 8;
    case WEDNESDAY              -> 9;
};
```

### 4，JVM 常量 API

​	引入一个 API 来建模关键类文件（key class-file）和运行时构件（run-time artifacts）的标称描述，特别是对那些可从常量池加载的常量。



### 5，默认类数据共享归档文件

​	增强 JDK 构建过程，在 64 位平台上使用默认的类列表生成类数据共享(class data-sharing，CDS)存档。



### 6，可中断的 G1 Mixed GC

​	如果 Mixed GC 的 G1 存在超出暂停目标的可能性，则使其可被中止。



### 7， G1 未使用分配内存即时返回

​	增强 G1 垃圾收集器，以便在空闲时自动将 Java 堆内存返回给操作系统。

​	

### 8，仅保留 AArch64 实现

​	删除与 arm64 实现相关的所有源代码，仅保留 32-bit ARM 和 64-bit aarch64 实现。

