# SpringBoot整合Thymeleaf模板第一弹-Thymeleaf整合环境配置

从今天开始我们通过使用详细的代码以及文档详细讲诉SpringBoot整合Thymeleaf模板去做一套Web页面.这篇文章主要讲述在使用SpringBoot整合Thymeleaf的时候的基础环境的配置.

> 创建一个maven项目(可使用idea或者其他编辑器)

```bash
mvn archetype:generate -DgroupId=com.edurt -DartifactId=springboot-thymeleaf-integration -DarchetypeArtifactId=maven-archetype-quickstart -Dversion=1.0.0 -DinteractiveMode=false
```

等待下载依赖, 完成项目的创建, 完成后将项目导入编辑器中.

> 在项目的pom文件中引入需要的springboot和thymeleaf依赖

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
 
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.edurt</groupId>
    <artifactId>springboot-thymeleaf-integration</artifactId>
    <packaging>jar</packaging>
    <version>1.0.0</version>
 
    <name>springboot-thymeleaf-integration</name>
    <url>http://maven.apache.org</url>
 
    <!-- 引入 springboot 全局依赖 -->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>1.5.9.RELEASE</version>
    </parent>
 
    <!-- 配置依赖, 插件, 系统属性版本 -->
    <properties>
        <system.java.version>1.8</system.java.version>
    </properties>
 
    <!-- 引入依赖 -->
    <dependencies>
        <!-- 引入 springboot web 依赖 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <!-- 引入 thymeleaf 依赖 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-thymeleaf</artifactId>
        </dependency>
    </dependencies>
 
    <!-- 引入 springboot 插件 -->
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
 
</project>
```

> 删除src/test下的所有java类

删除该文件是为了方便我们在编译的时候出现编译错误.

> 打开控制台运行以下命令

```bash
mvn clean package -X
```

查看编译是否成功, 出现以下内容表示项目编译成功

```bash
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 6.293 s
[INFO] Finished at: 2018-03-19T14:02:45+08:00
[INFO] Final Memory: 31M/214M
[INFO] ------------------------------------------------------------------------
```

