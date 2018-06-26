# SpringBoot整合JDBC数据库操作第十弹-第三方DataSource配置示例

上篇文章我们讲到了在项目中配置多DataSource和启用Transactional事务, 这篇文章主要讲解一下使用第三方DataSource配置示例.

> 使用druid数据源

在pom文件中加入druid数据源的依赖

```xml
<!-- druid -->
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid</artifactId>
    <version>1.0.18</version>
</dependency>
```

配置Druid数据源

```java
@Bean
public DataSource dataSource() {
    DruidDataSource dataSource = new DruidDataSource();
    dataSource.setDriverClassName(driver);
    dataSource.setUrl(url);
    dataSource.setUsername(username);
    dataSource.setPassword(password);
    return dataSource;
}
```

> 使用dbcp数据源

在pom文件中加入dbcp数据源的依赖

```xml
<!-- dbcp -->
<dependency>
    <groupId>commons-dbcp</groupId>
    <artifactId>commons-dbcp</artifactId>
    <version>1.4</version>
</dependency>
```

配置dbcp数据源

```java
@Bean
public DataSource dataSource() {
    BasicDataSource dataSource = new BasicDataSource();
    dataSource.setDriverClassName(driver);
    dataSource.setUrl(url);
    dataSource.setUsername(username);
    dataSource.setPassword(password);
    return dataSource;
}
```

以上是两种常用的数据源配置(当然配置项会很多,大家去到响应的官网上即可进行详细配置查询),使用其他的数据源的话就需要大家自行研究了.