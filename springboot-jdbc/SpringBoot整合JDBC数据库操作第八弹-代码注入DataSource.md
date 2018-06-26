# SpringBoot整合JDBC数据库操作第八弹-代码注入DataSource

上篇文章我们讲到了自定义RowMapper返回结果体,这篇文章主要讲解一下在项目中去使用代码注入DataSource(也是为了将项目的属性定制为自己喜欢的名称等).

- 将application.yml配置文件修改为以下内容

    ```xml
    custom:
      source:
        driver: com.mysql.jdbc.Driver
        url: jdbc:mysql://localhost:3306/test
        username: root
        password: 123456
    ```

- 在源码目录下新建config目录, 在该目录下新建CustomDataSource类文件

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
     
    import org.springframework.beans.factory.annotation.Value;
    import org.springframework.boot.autoconfigure.jdbc.DataSourceBuilder;
    import org.springframework.context.annotation.Bean;
    import org.springframework.context.annotation.Configuration;
    import org.springframework.jdbc.core.JdbcTemplate;
     
    import javax.sql.DataSource;
     
    /**
     * CustomDataSource <br/>
     * 描述 : CustomDataSource <br/>
     * 作者 : qianmoQ <br/>
     * 版本 : 1.0 <br/>
     * 创建时间 : 2018-03-28 下午2:51 <br/>
     * 联系作者 : <a href="mailTo:shichengoooo@163.com">qianmoQ</a>
     */
    @Configuration
    public class CustomDataSource {
     
        @Value(value = "${custom.source.driver}")
        private String driver;
     
        @Value(value = "${custom.source.url}")
        private String url;
     
        @Value(value = "${custom.source.username}")
        private String username;
     
        @Value(value = "${custom.source.password}")
        private String password;
     
        @Bean
        public DataSource dataSource() {
            return DataSourceBuilder.create()
                    .driverClassName(driver)
                    .url(url)
                    .username(username)
                    .password(password).build();
        }
     
        @Bean
        @ConfigurationProperties(prefix = "custom.source")
        public DataSource dataSource() {
            return DataSourceBuilder.create().build();
        }
     
        @Bean
        public JdbcTemplate jdbcTemplate() {
            return new JdbcTemplate(dataSource());
        }
     
    }
    ```

- 启动服务测试数据即可