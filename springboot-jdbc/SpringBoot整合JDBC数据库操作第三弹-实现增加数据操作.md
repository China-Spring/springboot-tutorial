# SpringBoot整合JDBC数据库操作第三弹-实现增加数据操作

上篇文章我们讲到了如何配置服务的DataSource数据库数据源,方便其对数据库进行操作.这篇文章主要讲解一下我们使用整合的JDBC进行简单的数据增加操作.

- 创建用于做测试数据的模拟数据表

    ```sql
    USE test;
 
    CREATE TABLE article (
      id          INT(10) AUTO_INCREMENT,
      title       VARCHAR(100) NOT NULL,
      description VARCHAR(200),
      PRIMARY KEY (id)
    );
    ```

- 创建数据表对应实体类(在源码目录下新建**bean**文件夹, 并在该文件夹下创建相应的**Article**类文件)

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
     
    /**
     * Article <br/>
     * 描述 : Article <br/>
     * 作者 : qianmoQ <br/>
     * 版本 : 1.0 <br/>
     * 创建时间 : 2018-03-26 下午4:51 <br/>
     * 联系作者 : <a href="mailTo:shichengoooo@163.com">qianmoQ</a>
     */
    public class Article {
     
        private Integer id;
        private String title;
        private String description;
     
        public Integer getId() {
            return id;
        }
     
        public void setId(Integer id) {
            this.id = id;
        }
     
        public String getTitle() {
            return title;
        }
     
        public void setTitle(String title) {
            this.title = title;
        }
     
        public String getDescription() {
            return description;
        }
     
        public void setDescription(String description) {
            this.description = description;
        }
     
        @Override
        public String toString() {
            return "Article{" +
                    "id=" + id +
                    ", title='" + title + '\'' +
                    ", description='" + description + '\'' +
                    '}';
        }
     
    }
    ```

- 创建数据表底层数据库操作Repository(在源码目录下创建**repository**文件夹, 并在该目录下创建**ArticleRepository**类文件)

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
     
    import com.edurt.bean.Article;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.jdbc.core.JdbcTemplate;
    import org.springframework.stereotype.Component;
     
    /**
     * ArticleRepository <br/>
     * 描述 : ArticleRepository <br/>
     * 作者 : qianmoQ <br/>
     * 版本 : 1.0 <br/>
     * 创建时间 : 2018-03-26 下午4:54 <br/>
     * 联系作者 : <a href="mailTo:shichengoooo@163.com">qianmoQ</a>
     */
    @Component
    public class ArticleRepository {
     
        @Autowired
        private JdbcTemplate jdbcTemplate; // 引入数据库操作模型
     
        /**
         * 创建文章信息
         *
         * @param article 文章信息
         */
        public void createArticle(Article article) {
            String sql = "INSERT INTO article(title, description) VALUES(?, ?)";
            jdbcTemplate.update(sql, article.getTitle(), article.getDescription());
        }
     
    }
    ```

- 创建数据库业务层Service (在源码目录下创建**service**文件夹, 并在该目录下创建**ArticleService**)

    ```java
    package com.edurt.service;
 
    import com.edurt.bean.Article;
     
    public interface ArticleService {
     
        void createArticle(Article article);
     
    }
    ```

- 创建接口实现**ArticleServiceImpl**类文件

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
    package com.edurt.service;
     
    import com.edurt.bean.Article;
    import com.edurt.repository.ArticleRepository;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.stereotype.Service;
     
    /**
     * ArticleServiceImpl <br/>
     * 描述 : ArticleServiceImpl <br/>
     * 作者 : qianmoQ <br/>
     * 版本 : 1.0 <br/>
     * 创建时间 : 2018-03-26 下午5:01 <br/>
     * 联系作者 : <a href="mailTo:shichengoooo@163.com">qianmoQ</a>
     */
    @Service(value = "articleService")
    public class ArticleServiceImpl implements ArticleService {
     
        @Autowired
        private ArticleRepository articleRepository;
     
        @Override
        public void createArticle(Article article) {
            articleRepository.createArticle(article);
        }
     
    }
    ```

- 创建API接口层Controller (在源码目录下创建**controller**文件夹, 并在该目录下创建**ArticleController**类文件)

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
     
    import com.edurt.bean.Article;
    import com.edurt.service.ArticleService;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.web.bind.annotation.RequestBody;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RequestMethod;
    import org.springframework.web.bind.annotation.RestController;
     
    /**
     * ArticleController <br/>
     * 描述 : ArticleController <br/>
     * 作者 : qianmoQ <br/>
     * 版本 : 1.0 <br/>
     * 创建时间 : 2018-03-26 下午5:08 <br/>
     * 联系作者 : <a href="mailTo:shichengoooo@163.com">qianmoQ</a>
     */
    @RestController
    @RequestMapping(value = "article")
    public class ArticleController {
     
        @Autowired
        private ArticleService articleService;
     
        @RequestMapping(value = "create", method = RequestMethod.POST)
        String create(@RequestBody Article article) {
            articleService.createArticle(article);
            return "SUCCESS";
        }
     
    }
    ```

- 使用RestAPI测试工具测试添加数据我用的是PostMan软件

    ![](http://image.cdn.ttxit.com/15289610572292.jpg)


- 查看数据表是否已经写入该数据

    ![](http://image.cdn.ttxit.com/15289610707571.jpg)