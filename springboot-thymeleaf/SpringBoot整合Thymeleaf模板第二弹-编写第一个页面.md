# SpringBoot整合Thymeleaf模板第二弹-编写第一个页面

上篇文章讲到了使用SpringBoot整合Thymeleaf的时候的基础环境的配置.这篇文章我们主要讲解我们使用整合后的环境去编写第一个页面.

> 创建resources目录文件夹目录为:src/main/resources并将其设置为resource资源目录

> 在resources目录下创建application.yml配置文件

```
spring:
  thymeleaf:
    # 缓冲配置
    cache: false
    # 检查模板配置
    check-template: true
    # 检查模板位置是否正确（默认值:true）
    check-template-location: true
    #Content-Type的值（默认值：text/html）
    content-type: text/html
    # 开启MVC Thymeleaf视图解析（默认值：true）
    enabled: true
    # 模板编码
    encoding: UTF-8
    # 要被排除在解析之外的视图名称列表，用逗号分隔
    # excluded-view-names:
    # 要运用于模板之上的模板模式。另见StandardTemplate-ModeHandlers(默认值：HTML5)
    mode: HTML5
    # 在构建URL时添加到视图名称前的前缀（默认值：classpath:/templates/）
    prefix: classpath:/templates/
    # 在构建URL时添加到视图名称后的后缀（默认值：.html）
    suffix: .html
    # Thymeleaf模板解析器在解析器链中的顺序。默认情况下，它排第一位。顺序从1开始，只有在定义了额外的TemplateResolver Bean时才需要设置这个属性。
#    template-resolver-order:
    # 可解析的视图名称列表，用逗号分隔
#    view-names:
```

> 在resources目录下创建templates文件目录, 并在该目录下创建index.html页面文件

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <title>SpringBoot Thymeleaf Integration</title>
</head>
<body>
 
<h1>SpringBoot Thymeleaf Integration</h1>
 
</body>
</html>
```

> 修改App类文件使其支持springboot

```java
package com.edurt;
 
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
 
/**
 * Hello world!
 */
@SpringBootApplication
public class App {
 
    public static void main(String[] args) {
        SpringApplication.run(App.class, args);
    }
 
}
```

> 创建HomeController进行页面跳转配置

```java
/**
 * Licensed to the Apache Software Foundation (ASF) under one
 * or more contributor license agreements.  See the NOTICE file
 * distributed with this work for additional information
 * regarding copyright ownership.  The ASF licenses this file
 * to you under the Apache License, Version 2.0 (the
 * "License"); you may not use this file except in compliance
 * with the License.  You may obtain a copy of the License at
 * <p>
 * http://www.apache.org/licenses/LICENSE-2.0
 * <p>
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */
package com.edurt.controller;
 
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
 
/**
 * HomeController <br/>
 * 描述 : HomeController <br/>
 * 作者 : qianmoQ <br/>
 * 版本 : 1.0 <br/>
 * 创建时间 : 2018-03-19 下午2:20 <br/>
 * 联系作者 : <a href="mailTo:shichengoooo@163.com">qianmoQ</a>
 */
@Controller
public class HomeController {
 
    @RequestMapping(value = {"/"}, method = RequestMethod.GET)
    String index() {
        return "index";
    }
 
}
```

> 打开控制台运行以下命令,然后打开浏览器访问 ip:端口即可看到页面效果

```bash
mvn spring-boot:run
```


