# Spring Boot整合Junit单元测试-001-Junit基础环境配置

> 创建一个 maven 项目(可使用 idea 或者其他编辑器)

```bash
mvn archetype:generate -DgroupId=com.edurt -DartifactId=springboot-junit-integration -DarchetypeArtifactId=maven-archetype-quickstart -Dversion=1.0.0 -DinteractiveMode=false
```

等待下载依赖, 完成项目的创建, 完成后将项目导入编辑器中.

> 在项目的pom文件中引入需要的springboot和junit依赖

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
 
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.edurt</groupId>
    <artifactId>springboot-junit-integration</artifactId>
    <packaging>jar</packaging>
    <version>1.0.0</version>
 
    <name>springboot-junit-integration</name>
    <url>http://maven.apache.org</url>
 
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>1.5.9.RELEASE</version>
    </parent>
 
    <properties>
        <system.java.version>1.8</system.java.version>
    </properties>
 
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <!-- 引入单元测试依赖 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
 
</project>
```

**删除src/test下的所有java类**

> 打开控制台运行以下命令

```bash
mvn clean package -X
```

查看编译是否成功, 出现以下内容表示项目编译成功

```java
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 3.568 s
[INFO] Finished at: 2018-03-26T16:11:01+08:00
[INFO] Final Memory: 26M/215M
[INFO] ------------------------------------------------------------------------
```

