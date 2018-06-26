# SpringBoot整合JDBC数据库操作第七弹-自定义RowMapper

上篇文章我们讲到了怎么对数据的查询操作,每次查询数据都会在返回中构建一个匿名类去封装返回结果,这样的话导致我们有大量的冗余代码,这并不是我们想要的结果,这篇文章主要讲解一下对数据结果的封装,也就是自定义RowMapper返回结果体.

- 在bean目录下创建ArticleRowMapper类文件

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
    package com.edurt.bean;
     
    import org.springframework.jdbc.core.RowMapper;
     
    import java.sql.ResultSet;
    import java.sql.SQLException;
     
    /**
     * ArticleRowMapper <br/>
     * 描述 : ArticleRowMapper <br/>
     * 作者 : qianmoQ <br/>
     * 版本 : 1.0 <br/>
     * 创建时间 : 2018-03-28 下午2:27 <br/>
     * 联系作者 : <a href="mailTo:shichengoooo@163.com">qianmoQ</a>
     */
    public class ArticleRowMapper implements RowMapper<Article> {
     
        @Override
        public Article mapRow(ResultSet resultSet, int i) throws SQLException {
            Article article = new Article();
            article.setId(resultSet.getInt("id"));
            article.setTitle(resultSet.getString("title"));
            article.setDescription(resultSet.getString("description"));
            return article;
        }
     
    }
    ```

- 修改ArticleRepository类文件, 替换rowmapper为自定义的类

    ```java
    /**
     * 查询所有数据
     */
    public List<Article> findAll() {
        String sql = "SELECT id, title, description FROM article";
        return jdbcTemplate.query(sql, new ArticleRowMapper());
    }
     
    /**
     * 查询单条数据
     */
    public Article findById(Integer id) {
        String sql = "SELECT id, title, description FROM article WHERE id = ?";
        return jdbcTemplate.queryForObject(sql, new ArticleRowMapper());
    }
    ```

- 使用RestAPI测试工具测试api接口可用性