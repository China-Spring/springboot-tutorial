# SpringBoot整合JDBC数据库操作第二弹-配置基本数据库连接源

上篇文章我们讲到了如何配置整合JDBC的基础环境,这篇文章我们讲解一下如何去配置服务的DataSource数据库数据源,方便其对数据库进行操作.

- 在**src/main/**目录下创建**resources**目录文件夹目录,并将**src/main/resources**设置为**resource**资源目录
- 在resources目录下创建**application.yml**配置文件

    ```yml
    spring:
      datasource:
        # 使用数据库驱动
        driver-class-name: com.mysql.jdbc.Driver
        # 数据库连接地址
        url: jdbc:mysql://localhost:3306/test
        # 数据库用户名
        username: root
        # 数据库用户密码
        password: 123456
    ```

- 修改App类文件使其支持springboot

    ```java
    package com.edurt;
 
    import org.springframework.boot.SpringApplication;
    import org.springframework.boot.autoconfigure.SpringBootApplication;
    import org.springframework.context.annotation.ComponentScan;
     
    /**
     * Hello world!
     */
    @SpringBootApplication
    @ComponentScan(value = "com.edurt")
    public class App {
     
        public static void main(String[] args) {
            SpringApplication.run(App.class, args);
        }
     
    }
    ```
    
    此时我们运行App类中的main方法就可以启动SpringBoot服务了,如果咩有出现任何错误就说明服务配置成功!!!