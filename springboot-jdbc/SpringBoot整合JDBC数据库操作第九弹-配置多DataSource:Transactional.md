# SpringBoot整合JDBC数据库操作第九弹-配置多DataSource/Transactional

上篇文章我们讲到了使用代码注入DataSource,这篇文章主要讲解一下在项目中配置多DataSource和启用Transactional事务.

- 将application.yml配置文件加入以下内容

    ```xml
    custom-second:
      source:
        driver: com.mysql.jdbc.Driver
        url: jdbc:mysql://localhost:3306/test1
        username: root
        password: 123456
    ```

- 在源码目录下新建config目录, 在该目录下新建CustomSecondDataSource类文件

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
     
    import org.springframework.beans.factory.annotation.Qualifier;
    import org.springframework.boot.autoconfigure.jdbc.DataSourceBuilder;
    import org.springframework.boot.context.properties.ConfigurationProperties;
    import org.springframework.context.annotation.Bean;
    import org.springframework.context.annotation.Configuration;
    import org.springframework.jdbc.core.JdbcTemplate;
     
    import javax.sql.DataSource;
     
    /**
     * CustomSecondDataSource <br/>
     * 描述 : CustomSecondDataSource <br/>
     * 作者 : qianmoQ <br/>
     * 版本 : 1.0 <br/>
     * 创建时间 : 2018-03-29 下午1:29 <br/>
     * 联系作者 : <a href="mailTo:shichengoooo@163.com">qianmoQ</a>
     */
    @Configuration
    public class CustomSecondDataSource {
     
        @Bean(name = "secondDatasource")
        @ConfigurationProperties(prefix = "custom-second.source")
        public DataSource secondDataSource() {
            return DataSourceBuilder.create().build();
        }
     
        @Bean(name = "secondJdbcTemplate")
        public JdbcTemplate secondJdbcTemplate(@Qualifier("secondDatasource") DataSource dataSource) {
            return new JdbcTemplate(dataSource);
        }
     
    }
    ```

> 注意secondJdbcTemplate在创建时，传入的DataSource必须用@Qualifier("secondDatasource")声明，这样，才能使用第二个DataSource。

- 将CustomDataSource文件中的dataSource和jdbcTemplate标记为主要的, 修改为以下内容

    ```java
    @Bean
    @Primary
    public DataSource dataSource() {
        return DataSourceBuilder.create()
                .driverClassName(driver)
                .url(url)
                .username(username)
                .password(password).build();
    }
     
    @Bean
    @Primary
    public JdbcTemplate jdbcTemplate() {
        return new JdbcTemplate(dataSource());
    }
    ```

- 在repository文件夹下创建SecondRepository用于测试第二个datasource

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
    package com.edurt.repository;
     
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.beans.factory.annotation.Qualifier;
    import org.springframework.jdbc.core.JdbcTemplate;
    import org.springframework.stereotype.Component;
     
    /**
     * SecondRepository <br/>
     * 描述 : SecondRepository <br/>
     * 作者 : qianmoQ <br/>
     * 版本 : 1.0 <br/>
     * 创建时间 : 2018-03-29 下午1:35 <br/>
     * 联系作者 : <a href="mailTo:shichengoooo@163.com">qianmoQ</a>
     */
    @Component
    public class SecondRepository {
     
        @Autowired
        @Qualifier("secondJdbcTemplate")
        // 在需要使用第二个JdbcTemplate的地方，我们注入时需要用@Qualifier("secondJdbcTemplate")标识
        private JdbcTemplate jdbcTemplate;
     
        public int save(int i) {
            return jdbcTemplate.update("INSERT INTO a(id) VALUES (?)", i);
        }
     
    }
    ```

- 修改ArticleController对外接口类

    ```java
    @Autowired
    private SecondRepository secondRepository;
     
    @RequestMapping(value = "test", method = RequestMethod.POST)
    int test(@RequestParam Integer id) {
        return secondRepository.save(id);
    }
    ```

> 多个DataSource，多个JdbcTemplate时，强烈建议总是使用@Primary把其中某一个Bean标识为“主要的”，使用@Autowired注入时会首先使用被标记为@Primary的Bean

- 启用Transactional的话我们只需要将**@EnableTransactionManagement**增加到项目的启动类中和将**@Transactional**注解增加到我们要做事务的方法上即可