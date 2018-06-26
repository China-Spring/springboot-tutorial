# SpringBoot整合JDBC数据库操作第五弹-批量添加/删除/修改数据

上篇文章我们讲到了怎么对已经存在的数据进行修改/删除操作,也讲到了如何添加数据,但以前的操作只是对单条数据的操作.当我们要批量的进行数据的操作(比如批量增加,批量修改,批量删除)该怎么做呢?这篇文章主要讲解一下对数据的批量操作(批量增加,批量修改,批量删除).

- 修改`ArticleRepository`类文件, 增加批量添加/删除/修改方法

    ```java
    /**
     * 批量添加数据
     */
    public int batchCreateArticle(final List<Article> articles) {
        String sql = "INSERT INTO article(title, description) VALUES(?, ?)";
        // spring jdbc 帮我们生成了批量插入的 sql 语句, 我们也可以直接使用批量的插入 sql 语句进行批量数据插入
        // return jdbcTemplate.batchUpdate(new String[]{sql});
        return jdbcTemplate.batchUpdate(sql, new BatchPreparedStatementSetter() {
            @Override
            public void setValues(PreparedStatement preparedStatement, int i) throws SQLException {
                Article article = articles.get(i);
                preparedStatement.setString(1, article.getTitle());
                preparedStatement.setString(2, article.getDescription());
            }
     
            @Override
            public int getBatchSize() {
                return articles.size();
            }
        }).length;
    }
     
    /**
     * 批量修改数据
     */
    public int batchModfiyArticle(final List<Article> articles) {
        String sql = "UPDATE article SET title = ?, description = ? WHERE id = ?";
        // spring jdbc 帮我们生成了批量插入的 sql 语句, 我们也可以直接使用批量的插入 sql 语句进行批量数据插入
        return jdbcTemplate.batchUpdate(sql, new BatchPreparedStatementSetter() {
            @Override
            public void setValues(PreparedStatement preparedStatement, int i) throws SQLException {
                Article article = articles.get(i);
                preparedStatement.setString(1, article.getTitle());
                preparedStatement.setString(2, article.getDescription());
                preparedStatement.setInt(3, article.getId());
            }
     
            @Override
            public int getBatchSize() {
                return articles.size();
            }
        }).length;
    }
     
    /**
     * 批量删除数据
     */
    public int batchDeleteArticle(final List<Integer> ids) {
        String sql = "DELETE FROM article WHERE id = ?";
        // spring jdbc 帮我们生成了批量插入的 sql 语句, 我们也可以直接使用批量的插入 sql 语句进行批量数据插入
        return jdbcTemplate.batchUpdate(sql, new BatchPreparedStatementSetter() {
            @Override
            public void setValues(PreparedStatement preparedStatement, int i) throws SQLException {
                preparedStatement.setInt(1, ids.get(i));
            }
     
            @Override
            public int getBatchSize() {
                return ids.size();
            }
        }).length;
    }
    ```

- 修改`ArticleService`类文件, 增加批量添加/删除/修改方法

    ```java
    int batchCreateArticle(final List<Article> articles);
     
    int batchModfiyArticle(final List<Article> articles);
     
    int batchDeleteArticle(final List<Integer> ids);
    ```

- 修改`ArticleServiceImpl`类文件, 增加批量添加/删除/修改方法

    ```java
    @Override
    public int batchCreateArticle(List<Article> articles) {
        return articleRepository.batchCreateArticle(articles);
    }
     
    @Override
    public int batchModfiyArticle(List<Article> articles) {
        return articleRepository.batchModfiyArticle(articles);
    }
     
    @Override
    public int batchDeleteArticle(List<Integer> ids) {
        return articleRepository.batchDeleteArticle(ids);
    }
    ```

- 修改API接口层`ArticleController`, 增加批量添加/删除/修改对外接口

    ```java
    @RequestMapping(value = "batch/create", method = RequestMethod.POST)
    Integer batchCreate(@RequestBody List<Article> articles) {
        return articleService.batchCreateArticle(articles);
    }
     
    @RequestMapping(value = "batch/modify", method = RequestMethod.PUT)
    Integer batchModfiy(@RequestBody List<Article> articles) {
        return articleService.batchModfiyArticle(articles);
    }
     
    @RequestMapping(value = "batch/delete", method = RequestMethod.DELETE)
    Integer batchDelete(@RequestBody List<Integer> ids) {
        return articleService.batchDeleteArticle(ids);
    }
    ```

- 使用RestAPI测试工具测试api接口可用性