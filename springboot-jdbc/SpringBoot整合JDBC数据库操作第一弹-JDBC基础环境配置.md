# SpringBoot整合JDBC数据库操作第一弹-JDBC基础环境配置

从今天开始我们通过使用详细的代码以及文档详细讲诉SpringBoot整合JDBC去做数据库的操作.这篇文章主要讲述在使用SpringBoot整合JDBC的时候的基础环境的配置.

> 创建一个maven项目(可使用idea或者其他编辑器)

```bash
mvn archetype:generate -DgroupId=com.edurt -DartifactId=springboot-jdbc-integration -DarchetypeArtifactId=maven-archetype-quickstart -Dversion=1.0.0 -DinteractiveMode=false
```

等待下载依赖(此时下载可能会慢,建议使用自主的maven私服或者是国内的maven镜像), 完成项目的创建, 完成后将项目导入编辑器中.

> 在项目的pom文件中引入需要的springboot和jdbc依赖

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.edurt</groupId>
    <artifactId>springboot-jdbc-integration</artifactId>
    <packaging>jar</packaging>
    <version>1.0.0</version>
    
    <name>springboot-jdbc-integration</name>
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
    
    <dependencies>
        <!-- 引入 springboot web 依赖 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <!-- 引入 jdbc 依赖 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-jdbc</artifactId>
        </dependency>
        <!-- 引入 mysql 依赖 -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
        </dependency>
    </dependencies>
    
</project>
```

> **删除`src/test`下的所有java类**

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
[INFO] Total time: 3.568 s
[INFO] Finished at: 2018-03-26T16:11:01+08:00
[INFO] Final Memory: 26M/215M
[INFO] ------------------------------------------------------------------------
```

编译成功后说明我们的整合环境已经准备完善!!!