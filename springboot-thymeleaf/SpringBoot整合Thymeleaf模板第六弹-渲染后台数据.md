# SpringBoot整合Thymeleaf模板第六弹-渲染后台数据

> 修改 HomeController 增加后台模拟数据

```
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
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.servlet.ModelAndView;
 
import java.util.concurrent.ConcurrentHashMap;
 
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
    public ModelAndView index() {
        ConcurrentHashMap<String, Integer> dataMap = new ConcurrentHashMap<String, Integer>();
        dataMap.put("1", 1);
        dataMap.put("2", 2);
        dataMap.put("3", 3);
        dataMap.put("4", 4);
        dataMap.put("5", 5);
        dataMap.put("6", 6);
        ModelAndView modelAndView = new ModelAndView("/index");
        modelAndView.addObject("data", dataMap);
        return modelAndView;
    }
 
    public String index(Model model) {
        ConcurrentHashMap<String, Integer> dataMap = new ConcurrentHashMap<String, Integer>();
        dataMap.put("1", 1);
        dataMap.put("2", 2);
        dataMap.put("3", 3);
        dataMap.put("4", 4);
        dataMap.put("5", 5);
        dataMap.put("6", 6);
        model.addAttribute(dataMap);
        return "index";
    }
 
}
```

> 修改页面渲染返回数据

```
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8" />
    <title>SpringBoot Thymeleaf Integration</title>
    <link rel="stylesheet" href="/style.css" />
    <link rel="stylesheet" href="/sti/a.css" />
</head>
<body>
 
<h1>SpringBoot Thymeleaf Integration</h1>
 
<h2>h2 title</h2>
 
<span class="login-title">我是引用的样式</span>
 
<div>
    后台数据是
    <p th:text=" ${data} " ></p>
</div>
 
</body>
<script src="/home.js"></script>
</html>
```

