# SpringBoot整合Thymeleaf模板第七弹-实现项目热部署

> 修改 pom 文件增加maven的devtools依赖

```
<!-- 引入热部署依赖 -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <optional>true</optional>
</dependency>
```
**注意：optional只有设置为true时才会热启动，即当修改了html、css、js等这些静态资源后不用重启项目直接刷新即可。**

> 修改 springboot 插件配置

```
<plugin>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-maven-plugin</artifactId>
    <configuration>
        <fork>true</fork>
    </configuration>
</plugin>
```

**配置了fork后在修改java文件后也就支持了热启动，不过这种方式是属于项目重启（速度比较快的项目重启），会清空session中的值，也就是如果有用户登陆的话，项目重启后需要重新登陆。**
**IDEA 中File-Settings-Compiler-Build Project automatically**

