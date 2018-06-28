# SpringBoot整合Thymeleaf模板第三弹-解除thymeleaf硬编码限制

上篇文章讲到了编写第一个Thymeleaf页面.这篇文章我们主要讲解如何解除thymeleaf页面标签硬编码限制的问题.

> 这个编码限制是由于我们在spring.thymeleaf.mode使用 html5模板导致出现以下错误

```java
2018-03-19 14:41:00.238 ERROR 66806 --- [nio-2000-exec-1] org.thymeleaf.TemplateEngine             : [THYMELEAF][http-nio-2000-exec-1] Exception processing template "index": Exception parsing document: template="index", line 6 - column 3
2018-03-19 14:41:00.244 ERROR 66806 --- [nio-2000-exec-1] o.a.c.c.C.[.[.[/].[dispatcherServlet]    : Servlet.service() for servlet [dispatcherServlet] in context with path [] threw exception [Request processing failed; nested exception is org.thymeleaf.exceptions.TemplateInputException: Exception parsing document: template="index", line 6 - column 3] with root cause
 
org.xml.sax.SAXParseException: 元素类型 "meta" 必须由匹配的结束标记 "</meta>" 终止。
    at com.sun.org.apache.xerces.internal.util.ErrorHandlerWrapper.createSAXParseException(ErrorHandlerWrapper.java:203) ~[na:1.8.0_141]
    at com.sun.org.apache.xerces.internal.util.ErrorHandlerWrapper.fatalError(ErrorHandlerWrapper.java:177) ~[na:1.8.0_141]
    at com.sun.org.apache.xerces.internal.impl.XMLErrorReporter.reportError(XMLErrorReporter.java:400) ~[na:1.8.0_141]
    at com.sun.org.apache.xerces.internal.impl.XMLErrorReporter.reportError(XMLErrorReporter.java:327) ~[na:1.8.0_141]
    at com.sun.org.apache.xerces.internal.impl.XMLScanner.reportFatalError(XMLScanner.java:1472) ~[na:1.8.0_141]
    at com.sun.org.apache.xerces.internal.impl.XMLDocumentFragmentScannerImpl.scanEndElement(XMLDocumentFragmentScannerImpl.java:1749) ~[na:1.8.0_141]
    at com.sun.org.apache.xerces.internal.impl.XMLDocumentFragmentScannerImpl$FragmentContentDriver.next(XMLDocumentFragmentScannerImpl.java:2967) ~[na:1.8.0_141]
    at com.sun.org.apache.xerces.internal.impl.XMLDocumentScannerImpl.next(XMLDocumentScannerImpl.java:602) ~[na:1.8.0_141]
    at com.sun.org.apache.xerces.internal.impl.XMLDocumentFragmentScannerImpl.scanDocument(XMLDocumentFragmentScannerImpl.java:505) ~[na:1.8.0_141]
    at com.sun.org.apache.xerces.internal.parsers.XML11Configuration.parse(XML11Configuration.java:841) ~[na:1.8.0_141]
    at com.sun.org.apache.xerces.internal.parsers.XML11Configuration.parse(XML11Configuration.java:770) ~[na:1.8.0_141]
    at com.sun.org.apache.xerces.internal.parsers.XMLParser.parse(XMLParser.java:141) ~[na:1.8.0_141]
    at com.sun.org.apache.xerces.internal.parsers.AbstractSAXParser.parse(AbstractSAXParser.java:1213) ~[na:1.8.0_141]
    at com.sun.org.apache.xerces.internal.jaxp.SAXParserImpl$JAXPSAXParser.parse(SAXParserImpl.java:643) ~[na:1.8.0_141]
    at com.sun.org.apache.xerces.internal.jaxp.SAXParserImpl.parse(SAXParserImpl.java:327) ~[na:1.8.0_141]
    at org.thymeleaf.templateparser.xmlsax.AbstractNonValidatingSAXTemplateParser.doParse(AbstractNonValidatingSAXTemplateParser.java:209) ~[thymeleaf-2.1.6.RELEASE.jar:2.1.6.RELEASE]
    at org.thymeleaf.templateparser.xmlsax.AbstractNonValidatingSAXTemplateParser.parseTemplateUsingPool(AbstractNonValidatingSAXTemplateParser.java:134) ~[thymeleaf-2.1.6.RELEASE.jar:2.1.6.RELEASE]
    at org.thymeleaf.templateparser.xmlsax.AbstractNonValidatingSAXTemplateParser.parseTemplate(AbstractNonValidatingSAXTemplateParser.java:116) ~[thymeleaf-2.1.6.RELEASE.jar:2.1.6.RELEASE]
    at org.thymeleaf.TemplateRepository.getTemplate(TemplateRepository.java:278) ~[thymeleaf-2.1.6.RELEASE.jar:2.1.6.RELEASE]
    at org.thymeleaf.TemplateEngine.process(TemplateEngine.java:1104) ~[thymeleaf-2.1.6.RELEASE.jar:2.1.6.RELEASE]
    at org.thymeleaf.TemplateEngine.process(TemplateEngine.java:1060) ~[thymeleaf-2.1.6.RELEASE.jar:2.1.6.RELEASE]
    at org.thymeleaf.TemplateEngine.process(TemplateEngine.java:1011) ~[thymeleaf-2.1.6.RELEASE.jar:2.1.6.RELEASE]
    at org.thymeleaf.spring4.view.ThymeleafView.renderFragment(ThymeleafView.java:335) ~[thymeleaf-spring4-2.1.6.RELEASE.jar:2.1.6.RELEASE]
    at org.thymeleaf.spring4.view.ThymeleafView.render(ThymeleafView.java:190) ~[thymeleaf-spring4-2.1.6.RELEASE.jar:2.1.6.RELEASE]
    at org.springframework.web.servlet.DispatcherServlet.render(DispatcherServlet.java:1286) ~[spring-webmvc-4.3.13.RELEASE.jar:4.3.13.RELEASE]
    at org.springframework.web.servlet.DispatcherServlet.processDispatchResult(DispatcherServlet.java:1041) ~[spring-webmvc-4.3.13.RELEASE.jar:4.3.13.RELEASE]
    at org.springframework.web.servlet.DispatcherServlet.doDispatch(DispatcherServlet.java:984) ~[spring-webmvc-4.3.13.RELEASE.jar:4.3.13.RELEASE]
    at org.springframework.web.servlet.DispatcherServlet.doService(DispatcherServlet.java:901) ~[spring-webmvc-4.3.13.RELEASE.jar:4.3.13.RELEASE]
    at org.springframework.web.servlet.FrameworkServlet.processRequest(FrameworkServlet.java:970) ~[spring-webmvc-4.3.13.RELEASE.jar:4.3.13.RELEASE]
    at org.springframework.web.servlet.FrameworkServlet.doGet(FrameworkServlet.java:861) ~[spring-webmvc-4.3.13.RELEASE.jar:4.3.13.RELEASE]
    at javax.servlet.http.HttpServlet.service(HttpServlet.java:635) ~[tomcat-embed-core-8.5.23.jar:8.5.23]
    at org.springframework.web.servlet.FrameworkServlet.service(FrameworkServlet.java:846) ~[spring-webmvc-4.3.13.RELEASE.jar:4.3.13.RELEASE]
    at javax.servlet.http.HttpServlet.service(HttpServlet.java:742) ~[tomcat-embed-core-8.5.23.jar:8.5.23]
    at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:231) ~[tomcat-embed-core-8.5.23.jar:8.5.23]
    at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166) ~[tomcat-embed-core-8.5.23.jar:8.5.23]
    at org.apache.tomcat.websocket.server.WsFilter.doFilter(WsFilter.java:52) ~[tomcat-embed-websocket-8.5.23.jar:8.5.23]
    at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193) ~[tomcat-embed-core-8.5.23.jar:8.5.23]
    at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166) ~[tomcat-embed-core-8.5.23.jar:8.5.23]
    at org.springframework.web.filter.RequestContextFilter.doFilterInternal(RequestContextFilter.java:99) ~[spring-web-4.3.13.RELEASE.jar:4.3.13.RELEASE]
    at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107) ~[spring-web-4.3.13.RELEASE.jar:4.3.13.RELEASE]
    at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193) ~[tomcat-embed-core-8.5.23.jar:8.5.23]
    at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166) ~[tomcat-embed-core-8.5.23.jar:8.5.23]
    at org.springframework.web.filter.HttpPutFormContentFilter.doFilterInternal(HttpPutFormContentFilter.java:108) ~[spring-web-4.3.13.RELEASE.jar:4.3.13.RELEASE]
    at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107) ~[spring-web-4.3.13.RELEASE.jar:4.3.13.RELEASE]
    at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193) ~[tomcat-embed-core-8.5.23.jar:8.5.23]
    at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166) ~[tomcat-embed-core-8.5.23.jar:8.5.23]
    at org.springframework.web.filter.HiddenHttpMethodFilter.doFilterInternal(HiddenHttpMethodFilter.java:81) ~[spring-web-4.3.13.RELEASE.jar:4.3.13.RELEASE]
    at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107) ~[spring-web-4.3.13.RELEASE.jar:4.3.13.RELEASE]
    at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193) ~[tomcat-embed-core-8.5.23.jar:8.5.23]
    at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166) ~[tomcat-embed-core-8.5.23.jar:8.5.23]
    at org.springframework.web.filter.CharacterEncodingFilter.doFilterInternal(CharacterEncodingFilter.java:197) ~[spring-web-4.3.13.RELEASE.jar:4.3.13.RELEASE]
    at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107) ~[spring-web-4.3.13.RELEASE.jar:4.3.13.RELEASE]
    at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193) ~[tomcat-embed-core-8.5.23.jar:8.5.23]
    at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166) ~[tomcat-embed-core-8.5.23.jar:8.5.23]
    at org.apache.catalina.core.StandardWrapperValve.invoke(StandardWrapperValve.java:199) ~[tomcat-embed-core-8.5.23.jar:8.5.23]
    at org.apache.catalina.core.StandardContextValve.invoke(StandardContextValve.java:96) [tomcat-embed-core-8.5.23.jar:8.5.23]
    at org.apache.catalina.authenticator.AuthenticatorBase.invoke(AuthenticatorBase.java:478) [tomcat-embed-core-8.5.23.jar:8.5.23]
    at org.apache.catalina.core.StandardHostValve.invoke(StandardHostValve.java:140) [tomcat-embed-core-8.5.23.jar:8.5.23]
    at org.apache.catalina.valves.ErrorReportValve.invoke(ErrorReportValve.java:81) [tomcat-embed-core-8.5.23.jar:8.5.23]
    at org.apache.catalina.core.StandardEngineValve.invoke(StandardEngineValve.java:87) [tomcat-embed-core-8.5.23.jar:8.5.23]
    at org.apache.catalina.connector.CoyoteAdapter.service(CoyoteAdapter.java:342) [tomcat-embed-core-8.5.23.jar:8.5.23]
    at org.apache.coyote.http11.Http11Processor.service(Http11Processor.java:803) [tomcat-embed-core-8.5.23.jar:8.5.23]
    at org.apache.coyote.AbstractProcessorLight.process(AbstractProcessorLight.java:66) [tomcat-embed-core-8.5.23.jar:8.5.23]
    at org.apache.coyote.AbstractProtocol$ConnectionHandler.process(AbstractProtocol.java:868) [tomcat-embed-core-8.5.23.jar:8.5.23]
    at org.apache.tomcat.util.net.NioEndpoint$SocketProcessor.doRun(NioEndpoint.java:1459) [tomcat-embed-core-8.5.23.jar:8.5.23]
    at org.apache.tomcat.util.net.SocketProcessorBase.run(SocketProcessorBase.java:49) [tomcat-embed-core-8.5.23.jar:8.5.23]
    at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149) [na:1.8.0_141]
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624) [na:1.8.0_141]
    at org.apache.tomcat.util.threads.TaskThread$WrappingRunnable.run(TaskThread.java:61) [tomcat-embed-core-8.5.23.jar:8.5.23]
    at java.lang.Thread.run(Thread.java:748) [na:1.8.0_141]
```

> **thymeleaf对.html的内容要求很严格，比如<meta charset=”UTF-8″ />， 如果少最后的标签封闭符号/，就会报错而转到错误页。也比如你在使用第三方 js 的库，然后有div v-cloak这样的html代码，也会被thymeleaf认为不符合要求而抛出错误。**

也就是说我们只要解决页面标签的封闭就可以解决了硬编码错误.

> 修改pom文件增加nekohtml依赖

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
        <!-- 依赖包 -->
        <dependency.nekohtml.version>1.9.22</dependency.nekohtml.version>
    </properties>
 
    <!-- 引入依赖 -->
    <dependencies>
        <!-- 引入 nekohtml 依赖 -->
        <dependency>
            <groupId>net.sourceforge.nekohtml</groupId>
            <artifactId>nekohtml</artifactId>
            <version>${dependency.nekohtml.version}</version>
        </dependency>
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

> 修改application.yml配置模板类型

```yml
mode: LEGACYHTML5
```

> 在html页面中增加一个未关闭的标签

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <title>SpringBoot Thymeleaf Integration</title>
</head>
<body>
 
<h1>SpringBoot Thymeleaf Integration</h1>
 
<h2>h2 title
 
</body>
</html>
```

> 启动服务访问我们所需要访问的页面就不会在出现硬编码的错误了

