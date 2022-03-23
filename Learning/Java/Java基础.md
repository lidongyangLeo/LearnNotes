## Java简介

- Java SE: Standard Edition (标准版)
- Java EE: Enterprise Edition （企业版 它只是在Java SE 的基础上加上了大量的API和库，以便方便开发web应用、数据库、消息服务等。JavaEE 的应用使用的虚拟机和JavaSE完全相同）
- Java ME: Micro Edition （和JavaSE 不同，它是一个针对嵌入式设备的瘦身版，JavaSE的标准库无法在JavaME上使用，JavaME的虚拟机也是瘦身版）



```code
┌───────────────────────────┐
│Java EE                    │
│    ┌────────────────────┐ │
│    │Java SE             │ │
│    │    ┌─────────────┐ │ │
│    │    │   Java ME   │ │ │
│    │    └─────────────┘ │ │
│    └────────────────────┘ │
└───────────────────────────┘
```



毫无疑问，JavaSE是整个Java平台的核心。而JavaEE 是进一步学习web应用所必须的。我们熟悉的Spring等框架都是Java EE开源生态系统的一部分。



推荐学习路线：

1. 首先学习JavaSE, 掌握Java语言本身、Java核心开发技术以及Java标准库的使用；
2. 如果继续学习Java EE,那么Spring 框架、数据库开发、分布式架构就是需要学习的
3. 如果学习大数据开发，那么Hadoop，Spark, Flink 这些大数据平台就是需要学习的。他们都是基于Java或Scala开发
4. 如果想要学习移动开发，那么就深入Android平台。掌握Android App开发。

名词解释：

初学者学Java 

- JDK ： Java Development Kit
- JRE： Java Runtime Environment 
- 





#### Java 重要特点

1. Java语言是面向对象的（oop）

2. Java语言是健壮的，Java的强类型机制、异常处理、垃圾的自动收集等是Java程序健壮性的重要保证

3. Java语言是跨平台性的 (一个编译好的.class文件可以在多个系统下运行，这种特性称为跨平台)

4. Java语言是解释型的

   解释性语言： javascript， PHP， java

   编译性语言： c/c++ 

   区别是：解释性语言，编译后的代码，不能直接被机器执行，需要解释器来执行，编译性语言，编译后的代码，可以直接被机器执行，c/c++

#### Java 开发工具

1. editplus
2. Nodepad++
3. Sublime Text
4. IDEA
5. eclipse



#### Java 运行机制及运行过程

- Java 核心机制 -Java虚拟机【JVM  java virtual machine】

基本介绍

1. JVM 是一个虚拟的计算机，具有指令集并使用不同的存储区域。负责执行指令，管理数据，内存、寄存器，包含在JDK中。
2. 对于不同的平台，有不同的虚拟机
3. Java 虚拟机机制屏蔽了底层运行平台的差别，实现了”一次编译，导出运行“

编译（javac）	

运行 （java）



#### 什么是JDK，JRE

##### JDK 基本介绍

1. JDK的全称（Java Development kit java开发工具包）

   JDK = JRE + java的开发工具【java, javac, javadoc, javap等】

2. JDK是提供给java开发人员使用的，其中包含了java的开发工具，也包括了JRE，所以安装了JDK，就不用在单独安装JRE了。

##### JRE基本介绍

1. JRE（Java Runtime Environment Java运行环境）

   JRE = JVM + Java的核心类库

2. 包括Java虚拟机（JVM Java Virtual Machine）和Java程序所需的核心类库等。

   如果想要运行一个开发好的Java程序，计算机中只需要安装JRE即可。



#### JDK  安装

官网

https://www.oracle.com/java/technologies/downloads/

安装路径不要有中文或者特殊符号如空格等。



#### 配置环境变量path 

- 为什么要配置path

  看到一个现象

  在dos命令中敲入javac,出现错误提示

- 原因分析

  错误原因：当前执行的程序在当前目录下如果不存在，win10系统会在系统中已有的一个名为path的环境变量指定的目录中查找。如果仍未找到，会出现以上的错误提示。

  所以进入到 jdk安装路径\bin 目录下，执行javac,会看到javac参数提示信息。

#### Mac OS 安装JDk







#### Java 开发注意事项和细节说明

1. Java源文件以.java为扩展名。源文件的基本组成部分是类（class）,如本类中的Hello类。

2. Java应用程序的执行入口是main()方法。它有固定的书写格式：

   Public static void main (String[] args) {}

3. Java语言严格区分大小写。

4. Java方法由一条条语句构成，每个语句以“；”结束。

5. 大括号都是成对出现的，缺一不可，【习惯先写{}再写代码】

6. 一个源文件中最多只能有一个public类，其他类的个数不限

7. 如果源文件包含一个public类，则文件名必须按该类名命名

8. 一个源文件中最多只能有一个public类。其它类的个数不限，也可以将main方法写在非public类中，然后指定运行非public类，这样入口方法就是非public的main方法

- 一个源文件中最多只能有一个public类。其他类的个数不限
- 每一个类编译后 都对应一个.class文件。









