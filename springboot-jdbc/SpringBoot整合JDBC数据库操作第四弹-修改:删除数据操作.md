# SpringBoot整合JDBC数据库操作第四弹-修改/删除数据操作

上篇文章我们讲到了如何实现增加数据操作,可以对数据库中增加新的数据信息.这篇文章主要讲解一下我们怎么对已经存在的数据进行修改/删除操作.

- 修改`ArticleRepository`类文件, 增加修改/删除数据方法

    ```java
    /**
     * 修改文章信息
     *
     * @param article 文章信息
     * @return 受影响的行数
     */
    public int modifyArticle(Article article) {
        String sql = "UPDATE article SET title = ?, description = ? WHERE id = ?";
        return jdbcTemplate.update(sql, article.getTitle(), article.getDescription(), article.getId());
    }
     
    /**
     * 删除文章信息
     *
     * @param articleId 文章编号
     * @return 受影响的行数
     */
    public int deleteArticle(Integer articleId) {
        String sql = "DELETE FROM article WHERE id = ?";
        return jdbcTemplate.update(sql, articleId);
    }
    ```

- 修改业务层`ArticleService`类文件, 增加修改/删除数据业务方法

    ```java
    int modifyArticle(Article article);
 
    int deleteArticle(Integer articleId);
    ```

- 修改业务层`ArticleServiceImpl`类文件

    ```java
    @Override
    public int modifyArticle(Article article) {
        return articleRepository.modifyArticle(article);
    }
     
    @Override
    public int deleteArticle(Integer articleId) {
        return articleRepository.deleteArticle(articleId);
    }
    ```

- 修改API接口层`ArticleController`增加修改/删除数据对外接口

    ```java
    @RequestMapping(value = "modify", method = RequestMethod.PUT)
    Integer modify(@RequestBody Article article) {
        return articleService.modifyArticle(article);
    }
     
    @RequestMapping(value = "delete", method = RequestMethod.DELETE)
    Integer delete(@RequestParam(value = "articleId") Integer articleId) {
        return articleService.deleteArticle(articleId);
    }
    ```

- 使用RestAPI测试工具测试api接口可用性