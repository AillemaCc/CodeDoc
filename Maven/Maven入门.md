# maven第一天

## maven简介

首先，我们需要知道传统项目管理状态分析是什么情况。我们用自己本地的jar包很方便，假如有一天（在没有maven的情况下）一个依赖包升级了，mybatis从4.0升级到5.0，但是我们的junit没有升级。这样就会出现冲突。调试起来也比较麻烦。

**上面的就是JAR包不统一或者不兼容导致的问题**

当然了，后面还有很多问题



这些就用maven来解决

### maven是什么

maven的本质是一个项目管理工具，将项目开发和管理过程，抽象成一个项目对象模型POM(Project Object Model)

这些都以面向对象的形式来进行设计

具体是怎么一回事呢？

把一个项目看成一个对象。pom.xml就是这个项目抽象成的对象。同时，项目对象里面用什么东西，需要**依赖管理**。同时，做出的项目也能变成资源，被maven管理。这是一个双向的调用。

还有一个概念是仓库，仓库有本地仓库 私服仓库 中央仓库，很多仓库。很多仓库不是仓库。

到这里，maven做我们依赖管理的一套结构就差不多了

接下来，有一个概念叫做**构建生命周期（阶段）**这个周期自身没有任何功能，但是maven针对这个项目构建的生命周期中的不同时期，做了相应的插件，使得在这个项目构建的周期内，maven能推动整个项目构建下来。

构建和插件是多对多的关系

![](http://photos.swindle.icu/picture/typora%E5%9B%BE%E7%89%87%E5%AD%98%E5%82%A8/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202024-11-17%20102656.png)

### maven的作用

项目构建

依赖管理

统一了开发结构

## maven下载安装

idea里面集成了，这些可以不用管

## 基本概念--仓库

中央服务器有一个中央仓库，里面放着全世界99%的jar包。但是人家这库里有，不代表你本地就有。所以你要去下载中央仓库里面的jar包，到你的本地仓库里。

但是这里面有一个问题，这个世界上不是我一个人搞开发，很多人都需要到中央仓库里面去下载jar包的内容。简而言之，kale

而且这个中央服务器不在中国境内，也会kale。怎么解决呢？

干脆在中间放一台服务器，在这个中间的服务器里面放一个私服仓库，私服仓库再从中央仓库拿。相当于一个缓存。而且个人仓库访问私服仓库是非常快速的。

## 基本概念--坐标

仓库当中有超级多的资源，资源变多了，查找的时候怎么查？

给一个设计良好的位置--坐标

来对仓库中资源进行定位

以下是maven坐标基础组成

* groupid：定义当前maven隶属组织名称，通常是域名的反写。例如org.mybaits
* artifactid：定义当前Maven项目名称，通常是模块名称，例如CRM，SMS
* verision：定义当前项目版本号

这就是资源的唯一标识

## 仓库配置

idea集成了孩子们，赞美idea吧

## idea创造maven项目

额，这个有什么可以写的吗

正常创建就可以了

~~~~xml
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
~~~~

上面的就是正常的引用

也没啥说的

构建用的命令随便点点就行了

## 如何把自己的项目变成javaweb项目

创建一个项目

点击这个项目

双击shift

输入add framework support

配置tomcat的部分

[链接](https://blog.csdn.net/qq_68754937/article/details/140342004)

但现在都是用springboot了，不用这么麻烦了

## 依赖管理

~~~~xml
   整个项目的依赖
<dependencies>
        单独的一个jar包依赖
        <dependency>
            组id
            <groupId>junit</groupId>
            项目id
            <artifactId>junit</artifactId>
            版本
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
~~~~

直接依赖是指在当前项目当中通过上面的那种依赖配置建立的依赖联系

间接依赖是指被依赖的资源还依赖着其他资源，大家都会一起出现

A->B->C

D->A

=>D->A->B->C

![](http://photos.swindle.icu/picture/typora%E5%9B%BE%E7%89%87%E5%AD%98%E5%82%A8/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202024-11-17%20120919.png)

除此之外，可选依赖可以让依赖的资源不透明

使用optional标签就可以

## 依赖范围

scope：范围

五种选项值

对于每一个jar来说，他在被添加成jar的时候，默认可以在任何情况之下使用。可以通过scope标签设定它的作用范围

* 主程序范围内依赖有效--main文件夹范围内
* 测试程序范围有效--test范围内
* 是否参与打包--package范围内

| scope                     | main | test | package |
| ------------------------- | ---- | ---- | ------- |
| compile--默认             | Y    | Y    | Y       |
| test--测试                |      | Y    |         |
| provided--不参与打包      | Y    | Y    |         |
| runtime--比如jdbc这种驱动 |      |      | Y       |

变成间接依赖的话，scpoe属性还有用吗？

项目一去依赖项目二

那么只有项目二打包的依赖才出现在项目一里面

依赖范围的传递性了解即可

## 生命周期与插件

### 构建生命周期

对于项目来说，整个的操作称为构建

compile--》test--》package--》install

在测试之前就会发生编译，这个流程或者说生命周期是线性的

maven构建生命周期描述的是一次构建过程经历了多少个事件

他对项目构建的生命周期分为三套：

* clean 清理工作
* default 核心工作：编译 测试 打包 部署
* site：产生报告 发布站点

每一个阶段当中，都包含具体的事件

### clean

pre-clean

clean

post-clean

### default

该生命周期也称为 Build 生命周期，是 Maven 使用的最频繁的生命周期，它覆盖了编译、测试、打包、部署等几乎所有的构建任务。它包括以下七个主要阶段：

    validate：验证项目是否正确，并且所有必要的信息都是可用的。
    compile：编译项目的源代码。
    test：使用适当的单元测试框架（如JUnit）运行测试。
    package：将编译后的代码打包成可分发的格式，如JAR、WAR或EAR文件。
    verify：运行任何检查以验证包是否有效且满足质量标准。
    install：将包安装到本地仓库，以便在本地的其他项目中作为依赖使用。
    deploy：将最终的包复制到远程仓库，以便与其他开发人员和项目共享。

上述七个阶段是顺序执行的，例如如果执行指令mvn package，那么则会自动执行前面的validate、compile和test三个生命周期。

里面还有非常多的生命周期函数



### site

presite

....

### 插件

插件与生命周期内的阶段进行绑定，在执行到对应生命周期的时候，执行对应的插件功能

默认maven在各个生命周期当中，绑定有预设的功能

通过插件可以自定义其他功能

##  模块开发设计思路

### 工程模块与模块划分

之前在接触项目的时候，都会接触到控制层数据层业务层这些概念。在以往的工程当中，只需要在一个项目当中分包开发就可以。但我们也可以把每一个层都变成独立的项目

独立的项目之间，靠接口通信。通过多个独立模块当中的合作，来完成整合项目。

## 模块聚合

多模块当中，

cntroller-->service-->dao-->pojo

这四个模块都会发布到我们的本地仓库当中。假如dao更新了，我们的其他模块知道他更新了吗？不一定知道。这就造成了冲突

最好是四个模块同时进行，不要分别执行。设计一个统领四个模块的模块，让他们能同时编译或者进行其他操作

这种思想就叫做模块聚合

这个工程当中，可以只留一个pom文件

~~~~xml
<packaging>pom</packaging>
~~~~

这句说明，这个项目当中只有pom

下面接着一句

~~~~xml
    <packaging>pom</packaging>
    <modules><!--管理的工程列表-->
        <module></module><!--具体的工程名称-->
    </modules>
~~~~

这就能管理其他的工程了

参与聚合操作的模块最终执行顺序和模块之间的依赖关系有关，和配置顺序无关

## 继承

通过聚合，我们解决了构建的问题。但是我们还有这样一个问题

比如不同的模块，都对同样的资源进行引用，但是同样的资源还存在版本问题。比如我开发模块A，使用资源α的1.0版本。你开发模块B，但是使用资源α的1.1版本。这两个版本之间不兼容。这就出现问题。

我们可以再造一个新的模块，负责管理这些引用的资源

儿子一样的工程继承爹一样的工程，用什么版本，爹说了算

Maven继承通过父子关系实现。子项目通过指定父项目的`groupId`、`artifactId`和`version`来建立继承关系。

~~~~xml
    <parent>
        <groupId>org.swindle</groupId>
        <artifactId>BLOG</artifactId>
        <version>1.0-SNAPSHOT</version>
    </parent>
~~~~

`dependencyManagement`

- **作用**：用于在父项目中定义依赖的版本管理。
- **特点**：子项目继承时，不会自动引入依赖，而是只继承版本信息。

~~~~xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>${spring.version}</version>
        </dependency>
    </dependencies>
</dependencyManagement>

~~~~

子项目使用时只需引用依赖，而不需要显式指定版本：

~~~~xml
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <!-- 版本号已由父项目管理 -->
    </dependency>
</dependencies>

~~~~

`pluginManagement`

- **作用**：用于在父项目中定义插件的版本管理。
- **特点**：子项目继承时，不会自动引入插件，而是只继承版本信息。

~~~~xml
<build>
    <pluginManagement>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.11.0</version>
                <configuration>
                    <source>${java.version}</source>
                    <target>${java.version}</target>
                </configuration>
            </plugin>
        </plugins>
    </pluginManagement>
</build>

~~~~

子项目需要手动引入插件

~~~~xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
        </plugin>
    </plugins>
</build>

~~~~

`build`与`profiles`

- **作用**：定义构建过程中的配置和多环境配置。

~~~~xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-surefire-plugin</artifactId>
            <version>3.0.0-M5</version>
        </plugin>
    </plugins>
</build>

<profiles>
    <profile>
        <id>development</id>
        <properties>
            <env>dev</env>
        </properties>
    </profile>
    <profile>
        <id>production</id>
        <properties>
            <env>prod</env>
        </properties>
    </profile>
</profiles>

~~~~

## 属性

最好有一种机制保证a改了，和a相关的b c都能改了

通过配置一些属性，就能实现上面的想法

`properties`

- **作用**：用于在父项目中定义全局属性，子项目可以继承并使用这些属性。

~~~~xml
<properties>
    <java.version>17</java.version>
    <spring.version>5.3.12</spring.version>
</properties>

~~~~

~~~~xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.11.0</version>
            <configuration>
                <source>${java.version}</source>
                <target>${java.version}</target>


            </configuration>
        </plugin>
    </plugins>
</build>

~~~~

## 版本管理

1.0-SNAPSHOT

1.1-SNAPSHOT

1.2-SNAPSHOT

通过版本号描述工程的版本

这个版本号都有啥含义呢？

* SNAPSHOT版本--快照版本

  项目开发过程中，输出的临时性版本叫做快照版本，或者说是一种阶段测试版本、快照版本会随着开发的进展不断更新

* RELEASE版本--发布版本

  项目开发进入到阶段里程碑之后，向外部发布的较为稳定的版本。这种版本对应的构件文件是稳定的。即使进行功能的后续开发，也不会改变当前版本已经发布的内容

## 资源配置

对于现在的maven工程，可以说已经管理的不错了。我是说管好自己这方面

那怎么管管其他部分呢

在工程当中，还有这种配置文件

~~~~xml
jdbc.driver=com.mysql.jdbc.Driver
~~~~

这种玩意也是需要管理的

于是，maven设定了一种机制，把所有配置文件都加入到pom文件当中。

但是没几个这么做的。。

既然是了解即可，我就不写了哈哈

## 结束了
