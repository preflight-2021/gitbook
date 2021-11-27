# JDK_5.0

发布时间：2004-09-30

代号：Tiger（老虎）

2004年9月，命名方式JDK x。

重大改变： 增加：自动装箱、泛型、动态注解、枚举、可变长参数、遍历循环（foreach循环）。改进了Java的内存模型（Java Memory Model，JMM）、提供了java.util.concurrent并发包。Windows 9x操作系统的最后一个JDK版本。

## 版本新特征



### 1，自动装箱与拆箱

​	自动装箱的过程，每当需要一种类型的对象时，这种基本类型就自动地封装到与它相同类型的包装中。

​	自动拆箱的过程，每当需要一个对象中的值时，被装箱对象中的值就被自动地提取出来，没必要再去调用intValue()和doubleValue()方法。

​	自动装箱，只需将该值赋给一个类型包装器（Double,Float,Long,Integer,Short,Character和Boolean）引用，java会自动创建一个对象。

​	自动拆箱，只需将该对象值赋给一个基本类型即可。



###  2，枚举（Enum）

​	将集合里面的对象元素分别列举出来，属于强类型，保证了系统安全性。枚举类型更具可读性， 易于理解， 易于维护。

​	简单用法：一般用于一组常量，可代替同类型的常量值。

​	复杂用法：内置有提供一些方法，而且枚举常量还可以有自己的方法。便于遍历枚举对象做更多业务操作。



### 3，静态导入（Import Static）

​	可以不用指定 Constants 类名而直接使用静态成员，包括静态方法。

​	import X和 import static X 的区别: 前者一般导入的是类文件如import java.util.Scanner; 后者一般是导入静态的方法，import static java.lang.System.out。



### 4，可变参数（Varargs）

​	可变参数的简单语法格式为：methodName([argumentList], dataType...argumentName);



### 5，内省（Introspector）

​	是 Java语言对Bean类属性、事件的一种缺省处理方法。

​	一 般的做法是通过类Introspector来获取某个对象的BeanInfo信息，然后通过BeanInfo来获取属性的描述器 （PropertyDescriptor），通过这个属性描述器就	可以获取某个属性对应的getter/setter方法，然后我们就可以通过反射机制来 调用这些方法。



### 6，泛型（Generic）

​	一个集合可以放任何类型的对象，相应地从集合里面拿对象的时候我们也 不得不对他们进行强制得类型转换。类似C++ 通过模板技术指定集合的元素类型。



### 7，循环（ForEach）

​	For-Each循环得加入简化了集合的遍历。假设我们要遍历一个集合对其中的元素进行一些处理。



### 8，元数据（注解）



### 9，内存模型（JMM）



### 10，并发包（concurrent）















