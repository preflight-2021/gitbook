# JDK(Java Development Kit)



## 阐述

JDK 是整个Java的核心，包括了Java运行环境，Java工具和Java基础的类库。

JDK是开发工具包， JRE是Java运行环境；JDK中包含JRE， JRE可以选择性安装， 他的主要功能是用来便宜Java程序代码。

一图说明JDK和JRE内置关系：

![1538359-20181116230026406-1027438630](F:\gitbook\java\jdk\resources\1538359-20181116230026406-1027438630.png)<



## Java的运行机制

Java语言编写的程序需要经过编译生成.class 文件，与平台无关的字节码。这种字节码必须使用JVM解释器来解释执行。

JVM是可运行Java字节码文件（.class ）的**虚拟计算机**，将字节码转换成特定系统的**机器码执行**。

![image-20211127114438739](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20211127114438739.png)<



## JDK 目录说明

![image-20211127114900787](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20211127114900787.png)<

1.  bin      ： 该路径下存放JDK各种命令工具的可执行文件， 包括java， javac 等命令都在该目录下命令实现， 都是在lib目录下的tools.jar 包中

   ​				（如：javac就在tools.jar包中的路径： sun/tools/javac路径下的main类， 有兴趣的同学可以反编译查看）。

2.  include:  该路径下存放系统平台特定的文件。

3.  jre        :  该路径下安装的就是运行Java程序所必须的JRE环境。

4.  lib        :  该路径下存放的是JDK工具命令的实际执行程序 ，包括执行环境编译打包后的jar包， 配置等。

5. javafx-src.zip ：是Java FX所有核心类库的源代码。

6. src.zip： 是Java所有核心类库的源代码。

7. README和LICENSE和COPYRIGHT等为说明性文件。

   

## JAVA环境配置

1. 安装Java jdk环境， 下载安装步骤则不作说明。

2. 配置环境变量（基于windows系统）：

   1. 新增系统变量JAVA_HOME

      <![image-20211127120302692](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20211127120302692.png)

   2. 系统变量Path路径下新增%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;

      ![image-20211127120526250](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20211127120526250.png)<





## JAVA 版本说明（v1 - 17）



图文说明JDK版本的更新历程：

![image-20211127133155338](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20211127133155338.png)<



## 官网

## https://www.oracle.com/java/



















