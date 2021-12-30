# Spring Boot Reference Document

## Getting Started

- Overview

````html
介绍Spring Boot,系统要求，小型服务容器，安装Spring Boot,并且开发你的第一个Spring Boot 应用。
````

1、**Introducing Spring Boot**

```html
Spring Boot帮助你创建一个基于Spring的可运行的独立的，生产级别的应用程序。因为我们考虑到了Spring平台以及第三方库的影响，因此，你开始学习的时候不需要考虑这些东西。大部分的Spring Boot 应用程序需要非常少的Spring 配置。
```

```html
你可以用Spring Boot去创建一个Java的应用程序，你可以通过使用java -jar或者更传统的war方式部署应用。我们还提供了一种运行 “spring scripts”的命令行工具的方式。
```

- 我们的主要目标是：

```html
1、为所有Spring开发提供更加快速和广泛可访问的入门体验。
2、开箱即用；
3、提供一些非功能性的特性，例如：安全性，指标，外部化部署等等。
4、不会生成代码，也无需XML配置。
```

2、**System Requirements**

```html
Spring Boot2.6.2：
1、要求Java8并且向上兼容，以及兼用Java17;
2、要求Spring Framework5.3.14及其以上版本；
```

- Build Tool

```html
1、Maven: 3.5+
2、Gradle: 6.8.x,6.9.x,7.x
```

- Servlet Containers

```html
Spring Boot 支持如下嵌入式小型服务器容器
1、Tomcat9.0    4.0
2、Jetty9.4     3.1
3、Jetty10.0    4.0
4、Undertow2.0  4.0
```

- 注：你也可以将Spring Boot应用程序部署在任何兼容servlet 3.1+的容器上

3、**Installing Spring Boot**

```html
Spring Boot可以与“经典的”Java开发工具一起使用，也可以作为命令行工具安装。无论哪种方式，您都需要Java SDK v1.8或更高版本.在开始之前，您应该使用以下命令检查当前的Java安装:

$ java -version
```

- Installation Instructions for the Java Developer

```html
1、你可以像使用任何Java标准库一样的去使用Spring Boot.Spring Boot不需要任何特殊的工具集成，所以您可以使用任何IDE或文本编辑器.
2、同样，Spring Boot应用程序也没有什么特别之处，所以您可以像运行其他Java程序一样运行和调试Spring Boot应用程序。
3、虽然你可以复制Spring Boot jar文件，但我们通常建议你使用支持依赖管理的构建工具(比如Maven或Gradle)。
```

- Maven Installation
-  [Maven官网](https://maven.apache.org/)

```html
你需要安装Maven 3.3+的版本。
```

```html
1、Spring Boot 依赖项使用org.springframework.boot groupId；
2、通常，Maven POM文件继承自spring-boot-starter-parent项目，并向一个或多个“启动者”声明依赖关系。
3、Spring Boot还提供了一个可选的Maven插件来创建可执行的jar文件。
```

4、**Developing Your First Spring Boot Application**

```html
本节介绍如何开发一个小型的“Hello World!”这个web应用程序突出了Spring Boot的一些关键特性。我们使用Maven来构建这个项目，因为大多数IDE都支持它。
```

```CQL
在我们开始之前，打开一个终端并运行以下命令，以确保您已经安装了有效版本的Java和Maven:

Microsoft Windows [版本 6.1.7601]
版权所有 (c) 2009 Microsoft Corporation。保留所有权利。

C:\Users\viruser.v-desktop>mvn -version
Apache Maven 3.8.4 (9b656c72d54e5bacbed989b64718c159fe39b537)
Maven home: D:\javaconfig\apache-maven-3.8.4-bin\apache-maven-3.8.4
Java version: 1.8.0_144, vendor: Oracle Corporation, runtime: D:\javaconfig\JDK8
u144x64_ths\jre
Default locale: zh_CN, platform encoding: GBK
OS name: "windows 7", version: "6.1", arch: "amd64", family: "windows"

C:\Users\viruser.v-desktop>java -version
java version "1.8.0_144"
Java(TM) SE Runtime Environment (build 1.8.0_144-b01)
Java HotSpot(TM) 64-Bit Server VM (build 25.144-b01, mixed mode)
```

**4.1 Creating the POM**

```
1、首先，我们需要创建一个Maven pom.xml文件。
2、xml是用于构建项目的配方。
3、打开你最喜欢的文本编辑器，添加以下内容:
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.hexin</groupId>
    <artifactId>myproject</artifactId>
    <version>0.0.1-SNAPSHOT</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.6.2</version>
    </parent>

    <!-- Additional lines to be added here... -->

</project>
```

```
groupId和artifactId：
1、groupId和artifactId被统称为“坐标”，是为了保证项目唯一性而提出的，如果你要把你得项目弄到maven本地仓库去，你想要找到你得项目就必须根据这两个id去查找。
2、groupId一般分为多个阶段，这里我只说两个阶段，第一个阶段为域，第二个阶段为公司名。
3、域又分为org、com、cn等等许多，其中org为非营利组织，com为商业组织。举个例子apache公司的tomcat项目例子：这个项目的groupId是org.apache,它的域是org(因为tomcat是非营利项目)，公司名称是apache,artifactId是tomcat。
4、比如我创建一个项目，如上。它的全路径就是：com.hexin.myproject;
```

- 执行mvn package

```
会在当前路径下生成一个target文件夹：
1、里面包含一个项目的jar包：myproject-0.0.1-SNAPSHOT.jar
2、包含一个maven-archiver文件夹（maven的构建工程），其中包含一个pom.properties文件，该文件为项目的说明文件，内容如下：
artifactId=myproject
groupId=com.hexin
version=0.0.1-SNAPSHOT
```

```
此时，您可以将项目导入到IDE中(大多数现代Java IDE都包含对Maven的内置支持)。
```

**4.2 Adding Classpath Dependencies**

```
1、Spring Boot 提供了一些启动器（Starters）,让你可以把jar包加入到你的类路径中。
2、我们上述的例子是把spring-boot-starter-parent启动器加入到了POM的“父模块”中。
3、spring-boot-starter-parent是一个特殊的启动器，它提供了有用的Maven默认值。
4、它还提供了一个依赖项管理（dependency-management）部分，这样您就可以为“blessed”依赖项省略版本标记。
```

```
1、其他的“Starters”提供的依赖项，在你开发特定类型的应用程序的时候可能会用到。
2、例如我们正在开发一个web应用程序，我们添加了一个spring-boot-starter-web依赖项。
3、我们可以通过运行如下的命令查看我们当前项目中拥有的依赖。

$ mvn dependency:tree

[INFO] com.hexin:myproject:jar:0.0.1-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  01:24 min
[INFO] Finished at: 2021-12-29T17:33:58+08:00
[INFO] ------------------------------------------------------------------------
```

```
1、mvn dependency:tree命令打印一个项目依赖关系的树；
2、您可以看到spring-boot-starter-parent本身没有提供任何依赖项；
3、要添加必要的依赖，编辑你的pom.xml，并将spring-boot-start-web依赖直接添加到父部分下面:
```

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```

```
如果你再次运行mvn dependency:tree，你会看到现在有很多额外的依赖项，包括Tomcat web服务器和Spring Boot本身

[INFO] com.hexin:myproject:jar:0.0.1-SNAPSHOT
[INFO] \- org.springframework.boot:spring-boot-starter-web:jar:2.6.2:compile
[INFO]    +- org.springframework.boot:spring-boot-starter:jar:2.6.2:compile
[INFO]    |  +- org.springframework.boot:spring-boot:jar:2.6.2:compile
[INFO]    |  +- org.springframework.boot:spring-boot-autoconfigure:jar:2.6.2:compile
[INFO]    |  +- org.springframework.boot:spring-boot-starter-logging:jar:2.6.2:compile
[INFO]    |  |  +- ch.qos.logback:logback-classic:jar:1.2.9:compile
[INFO]    |  |  |  +- ch.qos.logback:logback-core:jar:1.2.9:compile
[INFO]    |  |  |  \- org.slf4j:slf4j-api:jar:1.7.32:compile
[INFO]    |  |  +- org.apache.logging.log4j:log4j-to-slf4j:jar:2.17.0:compile
[INFO]    |  |  |  \- org.apache.logging.log4j:log4j-api:jar:2.17.0:compile
[INFO]    |  |  \- org.slf4j:jul-to-slf4j:jar:1.7.32:compile
[INFO]    |  +- jakarta.annotation:jakarta.annotation-api:jar:1.3.5:compile
[INFO]    |  +- org.springframework:spring-core:jar:5.3.14:compile
[INFO]    |  |  \- org.springframework:spring-jcl:jar:5.3.14:compile
[INFO]    |  \- org.yaml:snakeyaml:jar:1.29:compile
[INFO]    +- org.springframework.boot:spring-boot-starter-json:jar:2.6.2:compile
[INFO]    |  +- com.fasterxml.jackson.core:jackson-databind:jar:2.13.1:compile
[INFO]    |  |  +- com.fasterxml.jackson.core:jackson-annotations:jar:2.13.1:compile
[INFO]    |  |  \- com.fasterxml.jackson.core:jackson-core:jar:2.13.1:compile
[INFO]    |  +- com.fasterxml.jackson.datatype:jackson-datatype-jdk8:jar:2.13.1:compile
[INFO]    |  +- com.fasterxml.jackson.datatype:jackson-datatype-jsr310:jar:2.13.1:compile
[INFO]    |  \- com.fasterxml.jackson.module:jackson-module-parameter-names:jar:2.13.1:compile
[INFO]    +- org.springframework.boot:spring-boot-starter-tomcat:jar:2.6.2:compile
[INFO]    |  +- org.apache.tomcat.embed:tomcat-embed-core:jar:9.0.56:compile
[INFO]    |  +- org.apache.tomcat.embed:tomcat-embed-el:jar:9.0.56:compile
[INFO]    |  \- org.apache.tomcat.embed:tomcat-embed-websocket:jar:9.0.56:compile
[INFO]    +- org.springframework:spring-web:jar:5.3.14:compile
[INFO]    |  \- org.springframework:spring-beans:jar:5.3.14:compile
[INFO]    \- org.springframework:spring-webmvc:jar:5.3.14:compile
[INFO]       +- org.springframework:spring-aop:jar:5.3.14:compile
[INFO]       +- org.springframework:spring-context:jar:5.3.14:compile
[INFO]       \- org.springframework:spring-expression:jar:5.3.14:compile
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  33.083 s
[INFO] Finished at: 2021-12-29T17:41:50+08:00
[INFO] ------------------------------------------------------------------------
```

**4.3 Write the Code**

```
1、要完成我们的应用程序，我们需要创建一个Java文件。
2、默认情况下，Maven从src/main/java编译源代码，所以你需要创建这个目录结构，然后添加一个名为src/main/java/MyApplication.java的文件，以包含以下代码:
```

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.EnableAutoConfiguration;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@EnableAutoConfiguration
public class MyApplication {

    @RequestMapping("/")
    String home() {
        return "Hello World!";
    }

    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }

}
```

**4.3.1 The @RestController and @RequestMapping Annotations**

```
1、MyApplication类上的第一个注释是@RestController。这被称为原型注释。
2、它为阅读代码的人提供了提示，并为Spring提供了类扮演特定角色的提示。
3、在本例中，我们的类是一个web @Controller，所以Spring在处理传入的web请求时考虑它。
```

```
1、@RequestMapping注释提供了“路由”信息。
2、它告诉Spring，任何带有/路径的HTTP请求都应该映射到home方法。
3、@RestController注释告诉Spring将结果字符串直接呈现给调用者。
```

**4.3.2 The @EnableAutoConfiguration Annotation**

```
1、第二个类级注释是@EnableAutoConfiguration。
2、这个注释告诉Spring Boot根据添加的jar依赖项“猜测”您想要如何配置Spring。
3、因为Spring -boot-start -web添加了Tomcat和Spring MVC，所以自动配置假设你正在开发一个web应用程序，并相应地设置Spring。
```

**4.3.3 The "main" Method**

```
1、应用程序的最后一部分是“main”方法。
2、这是一个标准方法，它遵循应用程序入口点的Java约定。
3、我们的主方法通过调用run委托给Spring Boot的SpringApplication类。
4、SpringApplication启动我们的应用程序，启动Spring，而Spring又启动自动配置的Tomcat web服务器。
5、我们需要将MyApplication.class作为参数传递给run方法，以告诉SpringApplication哪个组件是Spring的主组件。
6、args数组也被传递来公开任何命令行参数。
```

**4.4 Running the Example**

```
1、此时，您的应用程序应该可以工作了。
2、因为使用了spring-boot-starter-父POM，所以您有了一个有用的运行目标，可以用来启动应用程序。
3、在根项目目录输入mvn spring-boot:run 以启动应用程序。
```

```java
  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::                (v2.6.2)

2021-12-29 18:25:28.401  INFO 5956 --- [           main] MyApplication                            : Starting MyApplication using Java 11.0.4 on trading-10-37-58 with PID 5956 (D:\java_learn\myspringboot\target\classes started by viruser in D:\java_learn\myspringboot)
2021-12-29 18:25:28.407  INFO 5956 --- [           main] MyApplication                            : No active profile set, falling back to default profiles: default
2021-12-29 18:25:32.193  INFO 5956 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8080 (http)
2021-12-29 18:25:32.223  INFO 5956 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2021-12-29 18:25:32.224  INFO 5956 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet engine: [Apache Tomcat/9.0.56]
2021-12-29 18:25:32.534  INFO 5956 --- [           main] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2021-12-29 18:25:32.534  INFO 5956 --- [           main] w.s.c.ServletWebServerApplicationContext : Root WebApplicationContext: initialization completed in 3984 ms
2021-12-29 18:25:35.362  INFO 5956 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http) with context path ''
2021-12-29 18:25:35.386  INFO 5956 --- [           main] MyApplication                            : Started MyApplication in 8.628 seconds (JVM running for 11.604)
2021-12-29 18:26:00.253  INFO 5956 --- [nio-8080-exec-1] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring DispatcherServlet 'dispatcherServlet'
2021-12-29 18:26:00.258  INFO 5956 --- [nio-8080-exec-1] o.s.web.servlet.DispatcherServlet        : Initializing Servlet 'dispatcherServlet'
2021-12-29 18:26:00.263  INFO 5956 --- [nio-8080-exec-1] o.s.web.servlet.DispatcherServlet        : Completed initialization in 5 ms
```

**4.5 Creating an Executable Jar**

```
1、我们通过创建一个可以在生产环境中运行的可执行jar文件来完成我们的示例。
2、可执行jar是包含已编译类以及运行代码所需的所有jar依赖项的归档文件。
3、要创建一个可执行的jar文件，我们需要将spring-boot-maven-plugin添加到pom.xml中。
4、要做到这一点，请在dependencies部分下面插入以下代码行:
```

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```

```
1、执行mvn package打包；
2、生成一个target/myproject-0.0.1-SNAPSHOT.jar文件
3、执行$ java -jar target/myproject-0.0.1-SNAPSHOT.jar即可
```

## Using Spring Boot

- Overview

```
1、构建系统；
2、结构化代码；
3、配置；
4、Spring Beans;
5、依赖注入；
6、开发者工具；
。。。
```

```
本节将详细介绍如何使用Spring Boot。它涵盖了诸如构建系统、自动配置以及如何运行应用程序等主题。我们还将介绍一些Spring Boot的最佳实践。尽管Spring Boot没有什么特别之处(它只是另一个您可以使用的库)，但是有一些建议，当遵循这些建议时，可以使您的开发过程变得更容易一些。
```

**1、Build Systems**

```
1、强烈建议您选择支持“依赖项管理”的构建系统，并且可以使用发布到“Maven Central”存储库的构件。
2、我们建议您选择Maven或Gradle。
3、他们可以让Spring Boot与其他构建系统(例如，Ant)一起工作，但它们并没有得到特别好的支持。
```

**1.1依赖管理**

```
1、Spring Boot的每个版本都提供了一个它所支持的依赖项列表。
2、实际上，您不需要在构建配置中为任何这些依赖项提供版本，因为Spring Boot会为您管理这些依赖项。
3、当您升级Spring Boot本身时，这些依赖项也会以一致的方式升级。
4、如果需要，您仍然可以指定一个版本并重写Spring Boot的建议。
```

```
1、策划的列表包含了所有您可以与Spring Boot一起使用的Spring模块，以及一个精炼的第三方库列表。
2、这个列表是一个标准的材料清单(spring-boot-dependencies)，可以在Maven和Gradle中使用。
3、Spring Boot的每个版本都与Spring框架的一个基本版本相关联。我们强烈建议您不要指定它的版本。（warning）
```

**1.2 Maven**

[maven](https://docs.spring.io/spring-boot/docs/current/reference/html/using.html#using)

**1.3 Gradle**

[Gradle](https://docs.spring.io/spring-boot/docs/current/reference/html/using.html#using)

**1.4 Ant**

```
1、可以使用Apache Ant+Ivy构建Spring Boot项目。
2、spring-boot-antlib“AntLib”模块也可以帮助Ant创建可执行jar文件。
```

- 要声明依赖关系，一个典型的ivy.xml文件看起来像下面的例子:

```xml
<ivy-module version="2.0">
    <info organisation="org.springframework.boot" module="spring-boot-sample-ant" />
    <configurations>
        <conf name="compile" description="everything needed to compile this module" />
        <conf name="runtime" extends="compile" description="everything needed to run this module" />
    </configurations>
    <dependencies>
        <dependency org="org.springframework.boot" name="spring-boot-starter"
            rev="${spring-boot.version}" conf="compile" />
    </dependencies>
</ivy-module>
```

- 典型的build.xml示例如下:

```xml
<project
    xmlns:ivy="antlib:org.apache.ivy.ant"
    xmlns:spring-boot="antlib:org.springframework.boot.ant"
    name="myapp" default="build">

    <property name="spring-boot.version" value="2.6.2" />

    <target name="resolve" description="--> retrieve dependencies with ivy">
        <ivy:retrieve pattern="lib/[conf]/[artifact]-[type]-[revision].[ext]" />
    </target>

    <target name="classpaths" depends="resolve">
        <path id="compile.classpath">
            <fileset dir="lib/compile" includes="*.jar" />
        </path>
    </target>

    <target name="init" depends="classpaths">
        <mkdir dir="build/classes" />
    </target>

    <target name="compile" depends="init" description="compile">
        <javac srcdir="src/main/java" destdir="build/classes" classpathref="compile.classpath" />
    </target>

    <target name="build" depends="compile">
        <spring-boot:exejar destfile="build/myapp.jar" classes="build/classes">
            <spring-boot:lib>
                <fileset dir="lib/runtime" />
            </spring-boot:lib>
        </spring-boot:exejar>
    </target>
</project>
```

**1.5 Starters**

```
1、"Starters"(启动器)是一组 可以在应用程序中包含它们 的 方便的依赖项描述符。
2、您可以获得所需的所有Spring和相关技术的一站式服务，而无需查找示例代码和复制-粘贴大量依赖描述符。
3、例如，如果您想开始使用Spring和JPA进行数据库访问，请在您的项目中包含Spring-boot-starter-data-jpa依赖项。
4、启动器包含大量的依赖项，您需要这些依赖项使项目快速启动和运行，并具有一致的、受托管支持的可传递依赖项集。
```

```
注：
1、在创建自己的Starters（启动器）时，不要以spring-boot开头，这是官方保留字；
2、比如你的项目名是myproject,则  应为：myproject-spring-boot-starter;
```

- The following application starters are provided by Spring Boot under the `org.springframework.boot` group:

```
1、spring-boot-starter ：核心启动器，包括自动配置支持、日志记录和YAML。
2、spring-boot-starter-activemq：使用Apache ActiveMQ的JMS消息传递的启动器。
3、spring-boot-starter-amqp： 使用Spring AMQP和Rabbit MQ的启动器。
4、spring-boot-starter-aop： 使用Spring AOP和AspectJ进行面向方面编程的启动器。
5、spring-boot-starter-artemis： 使用Apache Artemis进行JMS消息传递的启动器。
6、spring-boot-starter-batch： 使用Spring Batch的启动器。
7、spring-boot-starter-cache：使用Spring Framework缓存支持的启动器。
8、spring-boot-starter-data-cassandra：使用Cassandra分布式数据库和Spring Data Cassandra的启动器。
9、spring-boot-starter-data-cassandra-reactive： 使用Cassandra分布式数据库和Spring数据Cassandra Reactive的启动器；
10、等等详细见官网

管网上有社区提供的启动器网址。（github上）
```

**2、Structuring Your Code**

```
Spring Boot不需要特定的代码布局来工作，但是这里有一些建议。
```

**2.1 Using the "default" Package**

```
1、当一个类不包含包声明时，它被认为是在“默认包”中。
2、通常不鼓励使用“默认包”，应该避免使用。
3、对于使用@ComponentScan、@ConfigurationPropertiesScan、@entitscan或@SpringBootApplication注释的SpringBoot应用程序来说，它可能会导致特定的问题，因为每个jar中的每个类都会被读取。
4、我们建议您遵循Java推荐的包命名约定，并使用颠倒的域名(例如com.hexin.project)。
```

**2.2 Locating the Main Application Class**

```
1、我们通常建议您将主应用程序类放在根包中，而不是其他类。
2、@SpringBootApplication注释通常放在主类上，它隐式地为某些项定义一个基“搜索包”。
3、例如，如果您正在编写一个JPA应用程序，那么@SpringBootApplication注释类的包将用于搜索@Entity项。
4、使用根包还允许组件扫描只适用于您的项目。
5、如果你不想使用@SpringBootApplication，它导入的@EnableAutoConfiguration和@ComponentScan注释定义了该行为，所以你也可以使用它们。
```

- 下面的清单显示了一个典型的布局:

```
com
 +- hexin
     +- myapplication
         +- MyApplication.java
         |
         +- customer
         |   +- Customer.java
         |   +- CustomerController.java
         |   +- CustomerService.java
         |   +- CustomerRepository.java
         |
         +- order
             +- Order.java
             +- OrderController.java
             +- OrderService.java
             +- OrderRepository.java
```

- The `MyApplication.java` file would declare the `main` method, along with the basic `@SpringBootApplication`, as follows:

```java
@SpringBootApplication
public class MyApplication {

    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }

}
```

**3. Configuration Classes**

```
1、Spring Boot支持基于java的配置。
2、尽管可以将SpringApplication与XML源一起使用，但我们通常建议您的主源是单个@Configuration类。
3、通常，定义main方法的类可以作为主@Configuration。
```

**3.1 Importing Additional Configuration Classes**

```
1、您不需要将所有的@Configuration放在一个类中。
2、@Import注释可以用于导入其他配置类。
3、或者，您可以使用@ComponentScan自动获取所有Spring组件，包括@Configuration类。
```

**3.2. Importing XML Configuration**

```
1、如果您确定必须使用基于XML的配置，我们建议您仍然从@Configuration类开始。
2、然后可以使用@ImportResource注释来加载XML配置文件。
```

**4. Auto-configuration**

```
1、Spring Boot auto-configuration尝试根据添加的jar依赖项自动配置Spring应用程序。
2、例如，如果HSQLDB在类路径上，并且您没有手动配置任何数据库连接bean，那么Spring Boot将自动配置内存中的数据库。
3、您需要通过在@Configuration类中添加@EnableAutoConfiguration或@SpringBootApplication注释来选择自动配置。
```

**4.1 Gradually Replacing Auto-configuration **

```
1、自动配置是非侵入性的。
2、在任何时候，您都可以开始定义自己的配置来替换自动配置的特定部分。
3、例如，如果您添加自己的DataSource bean，默认的嵌入式数据库支持就会后退。
```

**4.2 Disabling Specific Auto-configuration Classes**

```
如果你发现某个你不想要的自动配置类正在被应用，你可以使用@SpringBootApplication的exclude属性来禁用它们，如下所示:
```

```
@SpringBootApplication(exclude = { DataSourceAutoConfiguration.class })
public class MyApplication {

}
```

```
1、如果类不在类路径上，则可以使用“annotation”的“excludeName”属性，并指定完全限定名。
2、如果你更喜欢使用@EnableAutoConfiguration而不是@SpringBootApplication, exclude和excludeName也是可用的。
3、最后，您还可以使用spring.autoconfiguration.exclude属性来控制要排除的自动配置类列表。
```

**5. Spring Beans and Dependency Injection**

```
1、您可以自由地使用任何标准Spring Framework技术来定义bean及其注入的依赖项。
2、我们通常建议使用构造函数注入来连接依赖和@ComponentScan来查找bean。
3、如果您按照上面建议的方式构造代码(将应用程序类定位在顶级包中)，您可以不带任何参数添加@ComponentScan或使用隐式包含它的@SpringBootApplication注释。（注：@SpringBootApplication中包含有@ComponentScan）
4、您的所有应用程序组件(@Component、@Service、@Repository、@Controller，以及其他)都自动注册为Spring bean。（所谓的组件其实就是一个类）
```

- 下面的例子展示了一个@Service Bean，它使用构造函数注入来获得一个所需的RiskAssessor Bean:

```java
@Service
public class MyAccountService implements AccountService {

    private final RiskAssessor riskAssessor;

    public MyAccountService(RiskAssessor riskAssessor) {
        this.riskAssessor = riskAssessor;
    }

    // ...

}
```

- 如果一个bean有多个构造函数，你需要用@Autowired标记你想让Spring使用的构造函数:

```java
@Service
public class MyAccountService implements AccountService {

    private final RiskAssessor riskAssessor;

    private final PrintStream out;

    @Autowired
    public MyAccountService(RiskAssessor riskAssessor) {
        this.riskAssessor = riskAssessor;
        this.out = System.out;
    }

    public MyAccountService(RiskAssessor riskAssessor, PrintStream out) {
        this.riskAssessor = riskAssessor;
        this.out = out;
    }

    // ...

}
```

**6. Using the @SpringBootApplication Annotation**

```
1、许多Spring Boot开发者喜欢他们的应用使用自动配置、组件扫描，并且能够在他们的“应用类”上定义额外的配置。
2、一个@SpringBootApplication注释可以用来启用这三个特性，即:
   （1）@EnableAutoConfiguration:启用Spring Boot的自动配置机制；
   （2）@ComponentScan:在应用程序所在的包上启用@Component scan；
   （3）@SpringBootConfiguration:允许在上下文中注册额外的bean，或者导入额外的配置类；
```

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication // same as @SpringBootConfiguration @EnableAutoConfiguration
                        // @ComponentScan
public class MyApplication {

    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```

```
1、这些特性都不是强制性的，您可以选择用它启用的任何特性来替换这个单一的注释。
2、例如，你可能不想在你的应用程序中使用组件扫描或配置属性扫描：
```

```java
@SpringBootConfiguration(proxyBeanMethods = false)
@EnableAutoConfiguration
@Import({ SomeConfiguration.class, AnotherConfiguration.class })
public class MyApplication {

    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }

}

在这个例子中，MyApplication和其他任何Spring Boot应用程序一样，除了带@ component注释的类和带@ configurationproperties注释的类不会自动检测到，用户定义的bean会显式导入(参见@Import)。
```



**7. Running Your Application**

```
1、将应用程序打包为jar并使用嵌入式HTTP服务器的最大优点之一是，您可以像运行其他任何应用程序一样，在任何地方运行您的应用程序。
```

**7.1. Running from an IDE**

```
1、您可以从IDE中作为Java应用程序运行Spring Boot应用程序。
2、但是，首先需要导入项目。
3、导入步骤因IDE和构建系统的不同而不同。
4、大多数ide都可以直接导入Maven项目。
5、如果你不能直接将你的项目导入到你的IDE中，你可以使用一个构建插件来生成IDE元数据。Maven为Eclipse和IDEA提供了插件。Gradle为各种ide提供了插件。
```

**7.2. Running as a Packaged Application**

- 如果你使用Spring Boot Maven或Gradle插件来创建一个可执行jar文件，你可以使用**java -jar**运行你的应用程序，如下所示:

```java
$ java -jar target/myapplication-0.0.1-SNAPSHOT.jar
```

- 也可以在启用远程调试支持的情况下运行打包的应用程序。这样做可以将调试器附加到打包的应用程序中，如下所示:

```java
$ java -Xdebug -Xrunjdwp:server=y,transport=dt_socket,address=8000,suspend=n -jar target/myapplication-0.0.1-SNAPSHOT.jar
```



**7.3. Using the Maven Plugin**

```
1、Spring Boot Maven插件包含一个 run 目标，可以用来快速编译和运行你的应用程序。
2、应用程序以exploded 的形式运行，就像它们在IDE中所做的那样。
3、下面的例子展示了一个典型的Maven命令来运行Spring Boot应用程序:

	$ mvn spring-boot:run
```

**7.4. Using the Gradle Plugin**

```
1、Spring Boot Gradle插件也包括一个bootRun任务，它也可以被用来以exploded的形式运行你的应用程序。
2、当你应用org.springframework.boot和java插件时，就会添加bootRun任务，如下所示:

	$ gradle bootRun
```

**8. Developer Tools**

```
1、Spring Boot包括一组额外的工具，可以使应用程序开发体验更愉快一些。
2、spring-boot-devtools模块可以包含在任何项目中，以提供额外的development-time特性。
3、要包含对devtools的支持，需要将模块依赖关系添加到构建中，如下Maven和Gradle的清单所示:
```

```java
Maven:

<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
        <optional>true</optional>
    </dependency>
</dependencies>
    
Gradle:

dependencies {
    developmentOnly("org.springframework.boot:spring-boot-devtools")
}
```

- 注意

```java
当运行完全打包的应用程序时，开发人员工具会自动禁用。如果你的应用程序是从java -jar启动的，或者是从一个特殊的类加载器启动的，那么它就被认为是一个“生产应用程序”。你可以通过使用spring.devtools.restart.enabled系统属性来控制这种行为。要启用devtools，不管用于启动应用程序的类加载器是什么，设置-Dspring.devtools.restart.enabled=true系统属性。在运行devtools会带来安全风险的生产环境中，不能这样做。要禁用devtools，请排除该依赖或设置
-Dspring.devtools.restart.enabled=false系统属性。
```

- 提示

```
1、在Maven中将依赖标记为可选的，或者在Gradle中使用developmentOnly配置(如上所示)，可以防止devtools被传递地应用到使用你项目的其他模块上。
2、默认情况下，重新打包的归档文件不包含devtools。如果您想使用某个远程devtools特性，则需要包含它。
3、当使用Maven插件时，将excludeDevtools属性设置为false。
4、当使用Gradle插件时，将任务的类路径配置为包含developmentOnly配置。
```

[热部署](https://www.jianshu.com/p/de544b13b9d5)

**8.1. Property Defaults**

```java
1、Spring Boot支持的几个库都使用缓存来提高性能。
2、例如，模板引擎缓存已编译的模板，以避免重复解析模板文件。
3、此外，当提供静态资源时，Spring MVC可以向响应添加HTTP缓存头信息。
4、虽然缓存在生产环境中非常有益，但在开发过程中可能会适得其反，使您无法看到刚才在应用程序中所做的更改。
5、因此，spring-boot-devtools默认禁用缓存选项。
6、缓存选项通常由application.properties文件设置。
7、例如，Thymeleaf 提供了spring.thyymleaf.cache属性。
8、spring-boot-devtools模块不需要手动设置这些属性，而是自动应用合理的 development-time 配置。
9、因为您在开发Spring MVC和Spring WebFlux应用程序时需要更多关于web请求的信息，developer tools建议您为web日志组启用DEBUG日志记录。
10、这将为您提供关于传入请求、哪个处理程序正在处理它、响应结果和其他细节的信息。
11、如果希望记录所有请求细节(包括潜在的敏感信息)，可以打开spring.mvc.log-request-details或spring.codec.log-request-details配置属性。
12、如果你不想应用默认属性，你可以在你的application.properties中将spring.devtools.add-properties设置为false。
13、关于devtools应用的属性的完整列表，请参见DevToolsPropertyDefaultsPostProcessor。
```

[DevToolsPropertyDefaultsPostProcessor](https://github.com/spring-projects/spring-boot/blob/v2.6.2/spring-boot-project/spring-boot-devtools/src/main/java/org/springframework/boot/devtools/env/DevToolsPropertyDefaultsPostProcessor.java)

**8.2. Automatic Restart**

```
1、只要类路径上的文件发生变化，使用spring-boot-devtools的应用程序就会自动重启。
2、当在IDE中工作时，这可能是一个有用的特性，因为它为代码更改提供了一个非常快速的反馈循环。
3、默认情况下，类路径中指向目录的任何条目都将被监视以查看是否有更改。
4、注意，某些资源，如静态资产和视图模板，不需要重新启动应用程序。
5、当DevTools监视类路径资源时，触发重新启动的唯一方法是更新类路径。
6、你更新类路径的方式取决于你使用的IDE:
7、在IntelliJ IDEA中，构建项目(Build +→+ Build project)也有同样的效果。
```

- 提示

```
1、如果你正在使用构建插件使用Maven或Gradle重新启动，你必须让fork设置为enabled。
2、Spring Boot提供的重启技术通过使用两个类加载器来工作。不会更改的类(例如，来自第三方jar文件的类)被装入一个基类装入器。您正在积极开发的类被装入一个重新启动的类装入器中。当应用程序重新启动时，将丢弃重新启动类加载器，并创建一个新的类加载器。这种方法意味着应用程序重启通常比“冷启动”快得多，因为基类加载器已经可用并被填充。
3、如果您发现重新启动应用程序的速度不够快，或者遇到了类加载问题，您可以考虑重新加载ZeroTurnaround的JRebel等技术。这些方法是在类加载时重写它们，使它们更易于重新加载。
```



**8.2.1. Logging changes in condition evaluation**

```
1、默认情况下，每次应用程序重新启动时，都会记录一个显示条件评估增量的报告。
2、当您进行诸如添加或删除bean以及设置配置属性等更改时，该报告将显示对应用程序的自动配置的更改。
3、要禁用报告的日志记录，请设置以下属性:

	spring.devtools.restart.log-condition-evaluation-delta=false
```

**8.2.2. Excluding Resources**

```
1、某些资源在被更改时并不一定需要触发重新启动。
2、例如，可以就地编辑Thymeleaf模板。
3、默认情况下，在/META-INF/maven、/META-INF/resources、/resources、/static、/public或/templates中更改资源不会触发重启，但会触发live reload。
4、如果你想定制这些排除项，你可以使用spring.devtools.restart.exclude属性。
5、例如，要只排除/static和/public，你需要设置以下属性:

	spring.devtools.restart.exclude=static/**,public/**
6、如果你想保留这些默认值并添加额外的排除项，请改用spring.devtools.restart.additional-exclude属性。
```

**8.2.3. Watching Additional Paths**

```
1、当对不在类路径中的文件进行更改时，您可能希望重新启动或重新加载应用程序。
2、要做到这一点，请使用spring.devtools.restart.additional-paths属性来配置额外的路径来监视其更改。
3、您可以使用前面描述的spring.devtools.restart.exclude属性来控制附加路径下的更改是触发完全重启还是动态重新加载（ live reload）。
```

**8.2.4. Disabling Restart**

```
1、如果不想使用重启特性，可以使用spring.devtools.restart.enabled属性来禁用它。
2、在大多数情况下，您可以在application.properties中设置此属性(这样做仍然会初始化重新启动的类加载器，但它不会监视文件更改)
3、如果你需要完全禁用重启支持(例如，因为它不能与特定的库一起工作)，你需要在调用SpringApplication.run(…)之前将spring.devtools.restart.enabled System属性设置为false，如下所示:
```

```java
@SpringBootApplication
public class MyApplication {

    public static void main(String[] args) {
        System.setProperty("spring.devtools.restart.enabled", "false");
        SpringApplication.run(MyApplication.class, args);
    }

}
```

**8.2.5. Using a Trigger File**

```
1、如果您使用的IDE不断编译已更改的文件，那么您可能希望仅在特定时间触发重启。
2、要做到这一点，你可以使用一个“trigger file”，这是一个特殊的文件，当你想真正触发重启检查时，必须修改它。
3、任何对文件的更新都会触发检查，但是只有当Devtools检测到它有一些事情要做时才会重启。
4、要使用触发器文件，请将spring.devtools.restart.trigger-file属性设置为触发器文件的名称(不包括任何路径)。
5、触发器文件必须出现在类路径的某个地方。
```

- 例如，如果你有一个结构如下的项目:

```
src
+- main
   +- resources
      +- .reloadtrigger
```

- 那么你的trigger-file属性将是:

```
spring.devtools.restart.trigger-file=.reloadtrigger
```

- 现在只会在src/main/resources/.reloadtrigger更新是重启。
- 您可能希望将spring.devtools.restart.trigger-file设置为全局设置，以便所有项目都以相同的方式运行。

```
1、有些ide有一些特性，可以让您不必手动更新触发器文件。
2、Eclipse和IntelliJ IDEA(旗舰版)都有这样的支持。
3、使用Spring Tools，你可以在控制台视图中使用“reload”按钮(只要你的触发器文件名为.reloadtrigger)
4、。
```

**8.2.6. Customizing the Restart Classloader**



## Core Features

- Overview

```
配置文件、日志记录、安全、缓存、Spring集成、测试等等。
```

## Web

- Overview

```
Servlet Web，响应式Web，嵌入式容器支持，优雅关闭，等等。
```

## Data

- Overview

```
SQL和NOSQL数据访问。
```

## IO

- Overview

```
缓存、Quartz调度器、REST客户端、发送电子邮件、Spring Web服务等等。
```

## Messaging

- Overview

```
MS, AMQP, RSocket, WebSocket和Spring集成。
```

## Container Images

- Overview

```
高效的容器映像和使用Dockerfiles和Cloud Native Buildpacks构建容器映像。
```

## Production-ready Features

- Overview

```
监控、度量、审计等等。
```

## Deploying Spring Boot Applications

- Overview

```
部署到云，并作为Unix应用程序安装。
```

## Spring Boot CLI

- Overview

```
安装CLI、使用CLI、配置CLI等。
```

## Build Tool Plugins

- Overview

```
Maven Plugin, Gradle Plugin, Antlib等等。
```

## "How-to Guides"

- Overview

```
应用程序开发、配置、嵌入式服务器、数据访问等等。
```



