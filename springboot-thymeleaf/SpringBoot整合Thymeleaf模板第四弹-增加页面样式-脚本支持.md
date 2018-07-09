# SpringBoot整合Thymeleaf模板第四弹-增加页面样式/脚本支持

上篇文章讲到了如何解除thymeleaf页面标签硬编码限制的问题.这篇文章我们主要讲解我们如何去使用thymeleaf模版进行对页面添加样式以及脚本的支持.

> **默认情况下，Spring Boot从classpath下一个叫/static（/public，/resources或/META-INF/resources）的文件夹或从ServletContext根目录提供静态内容。这使用了Spring MVC的ResourceHttpRequestHandler，所以你可以通过添加自己的WebMvcConfigurerAdapter并覆写addResourceHandlers方法来改变这个行为（加载静态文件）**

以上内容一定要注意

> 在resources目录下新建static目录,并创建style.css样式表

```css
.login-title {
    font-size: 30px;
}
```

> 在页面中引入css样式表

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <title>SpringBoot Thymeleaf Integration</title>
    <link rel="stylesheet" href="/style.css" />
</head>
<body>
 
<h1>SpringBoot Thymeleaf Integration</h1>
 
<h2>h2 title</h2>
 
<span class="login-title">我是引用的样式</span>
 
</body>
</html>
```

> 在static目录下创建home.js脚本文件

```javascript
alert(1);
```

> 在页面中引入脚本文件

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <title>SpringBoot Thymeleaf Integration</title>
    <link rel="stylesheet" href="/style.css" />
</head>
<body>
 
<h1>SpringBoot Thymeleaf Integration</h1>
 
<h2>h2 title</h2>
 
<span class="login-title">我是引用的样式</span>
 
</body>
<script src="/home.js"></script>
</html>
```

> 


