# SpringBoot整合JDBC数据库操作第六弹-实现查询数据操作

上篇文章我们讲到了怎么对批量操作(批量增加,批量修改,批量删除),这篇文章主要讲解一下对数据的查询操作.

- 修改ArticleRepository类文件, 增加查询数据方法

    ```java
    /**
     * 查询所有数据
     */
    public List<Article> findAll() {
        String sql = "SELECT id, title, description FROM article";
        return jdbcTemplate.query(sql, new RowMapper<Article>() {
            @Override
            public Article mapRow(ResultSet resultSet, int i) throws SQLException {
                Article article = new Article();
                article.setId(resultSet.getInt("id"));
                article.setTitle(resultSet.getString("title"));
                article.setDescription(resultSet.getString("description"));
                return article;
            }
        });
    }
     
    /**
     * 查询单条数据
     */
    public Article findById(Integer id) {
        String sql = "SELECT id, title, description FROM article WHERE id = ?";
        return jdbcTemplate.queryForObject(sql, new Object[]{id}, new RowMapper<Article>() {
            @Override
            public Article mapRow(ResultSet resultSet, int i) throws SQLException {
                Article article = new Article();
                article.setId(resultSet.getInt("id"));
                article.setTitle(resultSet.getString("title"));
                article.setDescription(resultSet.getString("description"));
                return article;
            }
        });
    }
    ```

- 修改`ArticleService`类文件, 增加查询数据方法

    ```java
    List<Article> findAll();
     
    Article findById(Integer id);
    ```

- 修改`ArticleServiceImpl`类文件, 增加查询数据方法

    ```java
    @Override
    public List<Article> findAll() {
        return articleRepository.findAll();
    }
     
    @Override
    public Article findById(Integer id) {
        return articleRepository.findById(id);
    }
    ```

- 修改API接口层`ArticleController`, 增加查询数据对外接口

    ```java
    @RequestMapping(value = "list", method = RequestMethod.GET)
    List<Article> list() {
        return articleService.findAll();
    }
     
    @RequestMapping(value = "info", method = RequestMethod.GET)
    Article info(@RequestParam Integer id) {
        return articleService.findById(id);
    }
    ```

- 使用RestAPI测试工具测试api接口可用性