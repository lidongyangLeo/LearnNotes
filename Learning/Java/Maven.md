## Maven

Maven 是一个Java项目管理和构建工具，它可以定义项目结构、项目依赖，并使用统一的方式进行自动化构建，是Java项目不可缺少的工具。

Maven 就是专门为Java项目打造的管理和构建工具，它的主要功能有：

1. 提供了一套标准化的项目结构
2. 提供了一套标准化的构建流程（编译，测试，打包，发布）
3. 提供了一套依赖管理机制

#### Maven项目结构 

一个使用Maven管理的普通的Java项目，它的目录结构默认如下：

```ascii
a-maven-project
├── pom.xml
├── src
│   ├── main
│   │   ├── java
│   │   └── resources
│   └── test
│       ├── java
│       └── resources
└── target
```

项目的根目录是a-maven-project是项目名，

它有一个项目描述文件pom.xml,存放Java源码的目录是`src/main/java`

存放资源文件的目录是`src/main/resources`

存放测试源码的目录是`src/test/resources`

所有的目录结构都是约定好的标准结构，我们千万不要随意修改目录结构，使用标准结构不需要做任何配置。Maven就可以正常使用。

`pom.xml`

```maven
<project ...>
	<modelVersion>4.0.0</modelVersion>
	<groupId>com.itranswarp.learnjava</groupId>
	<artifactId>hello</artifactId>
	<version>1.0</version>
	<packaging>jar</packaging>
	<properties>
        ...
	</properties>
	<dependencies>
        <dependency>
            <groupId>commons-logging</groupId>
            <artifactId>commons-logging</artifactId>
            <version>1.2</version>
        </dependency>
	</dependencies>
</project>
```

其中groupId 类似于java的包名，通常是公司或组织名称，

`artifactId`类似于Java的类名，通常是项目名称，再加上version,一个Maven工程就是由groupId，artifactId,和version作为唯一标识。我们在引用其他第三方库的时候，也是通过这三个变量确定。例如，依赖`commons-logging`

```maven
<dependency>
    <groupId>commons-logging</groupId>
    <artifactId>commons-logging</artifactId>
    <version>1.2</version>
</dependency>
```

使用dependency 声明一个依赖后， Maven就会自动下载这个依赖包并把它放到classpath 中。



### 安装Maven 

要安装Maven ，可以从Maven 官网下载最新Maven3.6.x. 然后在本地解压，设置几个环境变量

```
M2_HOME=/path/to/maven-3.6.x
PATH=$PATH:$M2_HOME/bin
```

Windows 可以把`%M2_HOME%\bin` 添加到系统Path 变量中。

然后打开命令行窗口， 输入 mvn -version ,应该看到maven的版本信息



Maven 解决了依赖管理。

#### 依赖关系

Maven 定义了几种依赖关系，分别是compile, test, runtime 和provided

| scope    | 说明                                          | 示例            |
| -------- | --------------------------------------------- | --------------- |
| compile  | 编译时需要用到该jar包（默认）                 | Commons-logging |
| test     | 编译Test 时需要用到该jar 包                   | junit           |
| runtime  | 编译时不需要，但运行时需要用到                | mysql           |
| provided | 编译时需要用到，但运行时由JDK或某个服务器提供 | Servlet-api     |

其中，默认的compile是最常用的，Maven会把这种类型的依赖直接放入classpath。

`test`依赖表示仅在测试时使用，正常运行时并不需要。最常用的`test`依赖就是`Junit`

```
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-api</artifactId>
    <version>5.3.2</version>
    <scope>test</scope>
</dependency>
```

Runtime 依赖表示编译时不需要，但运行时需要，最典型的runtime 依赖就是JDBC驱动，例如MySQL驱动

```
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.48</version>
    <scope>runtime</scope>
</dependency>
```

Provided 依赖表示编译时需要，但运行时不需要，最典型的provided依赖时`Servlet`API，编译的时候需要，但是运行时，Servlet服务器内置了相关的jar,所以运行期不需要，

```
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>4.0.0</version>
    <scope>provided</scope>
</dependency>
```

