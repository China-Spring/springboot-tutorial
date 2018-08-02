# SpringBoot整合Thymeleaf模板第五弹-自定义资源目录

> springboot的默认资源目录为static/public/resources

我们可以修改其使用自定义的资源目录

> 创建在源码目录下创建一个配置文件夹config, 然后创建一个**StaticConfig**类文件

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
package com.edurt.config;
 
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.ResourceHandlerRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurerAdapter;
 
/**
 * StaticConfig <br/>
 * 描述 : StaticConfig <br/>
 * 作者 : qianmoQ <br/>
 * 版本 : 1.0 <br/>
 * 创建时间 : 2018-03-19 下午3:19 <br/>
 * 联系作者 : <a href="mailTo:shichengoooo@163.com">qianmoQ</a>
 */
@Configuration
public class StaticConfig extends WebMvcConfigurerAdapter {
 
    @Override
    public void addResourceHandlers(ResourceHandlerRegistry registry) {
        // addResourceHandler中的是访问路径，可以修改为其他的字符串
        // addResourceLocations中的是实际路径
        registry.addResourceHandler("/sti/**").addResourceLocations("classpath:/sti/");
        super.addResourceHandlers(registry);
    }
 
}
```

> 在resources目录下新建sti目录, 并在该目录下新建 a.css 样式

```css
h1 {
    font-size: 100px;
}
```

> 在页面文件引入该样式

```html
<link rel="stylesheet" href="/sti/a.css" />
```


