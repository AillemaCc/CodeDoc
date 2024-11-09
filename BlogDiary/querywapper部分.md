# 前言
今天在写博客里面的一个新功能的时候，发现自己对于**QueryWrapper** 和 **LambdaQueryWrapper **已经很生涩了。在这里就总结一下这个关键字的功能。

在mp的官方文档当中·，对于条件构造器，是这样描述的：

>  MyBatis-Plus 提供了一套强大的条件构造器（Wrapper），用于构建复杂的数据库查询条件。Wrapper 类允许开发者以链式调用的方式构造查询条件，无需编写繁琐的 SQL 语句，从而提高开发效率并减少 SQL 注入的风险。  
>
> 
>

常用的基本就是**QueryWrapper** 和 **LambdaQueryWrapper。**这两个都继承自**AbstractWrapper。**

> + **QueryWrapper****：专门用于构造查询条件，支持基本的等于、不等于、大于、小于等各种常见操作。它允许你以链式调用的方式添加多个查询条件，并且可以组合使用 **`**and**`** 和 **`**or**`** 逻辑。**
> + **LambdaQueryWrapper：这是一个基于 Lambda 表达式的查询条件构造器，它通过 Lambda 表达式来引用实体类的属性，从而避免了硬编码字段名。这种方式提高了代码的可读性和可维护性，尤其是在字段名可能发生变化的情况下。  **
>

对我来说，这样可以封装（我不知道封装这个词用的是不是恰当）许多sql语句。实现非常方便的对数据的crud。

# 1.常用的基本方法：
## 1.1 eq
`eq` 方法是 MyBatis-Plus 中用于构建查询条件的基本方法之一，它用于设置单个字段的相等条件。  

事实上官方文档的实例写的非常易读。在这里不如放上一点我自己的代码片段。反正这个博客也只有我自己看

```java
    @Override
    public ResponseResult searchArticle(Integer pageNum, Integer pageSize, String keywords) {
        LambdaQueryWrapper<Article> queryWrapper = new LambdaQueryWrapper<>();
        queryWrapper.like(Article::getContent,keywords);
        queryWrapper.eq(Article::getStatus,SystemConstants.ARTICLE_STATUS_NORMAL);
        queryWrapper.orderByDesc(Article::getCreateTime);

        //分页查询
        Page<Article> page = new Page<>(pageNum,pageSize);
        page(page,queryWrapper);
        //封装查询结果
        List<ArticleListVo> articleListVos = BeanCopyUtils.copyBeanList(page.getRecords(), ArticleListVo.class);

        PageVo pageVo = new PageVo(articleListVos,page.getTotal());
        return ResponseResult.okResult(pageVo);
    }
```

这里面的命名也是垃圾。。

对于：

```java
queryWrapper。eq(Article::getStatus,SystemConstants.ARTICLE_STATUS_NORMAL);
```

就用到了eq方法。用来判断文章的状态是否正常

也可以用QueryWarapper这样写：

```java
queryWrapper。eq("status",SystemConstants.ARTICLE_STATUS_NORMAL)
```

官方文档当中这样写道：

```java
-- 普通 Wrapper 和 Lambda Wrapper 生成的 SQL 相同
SELECT * FROM user WHERE name = '老王'
```

## 1.2 like
`like` 方法是 MyBatis-Plus 中用于构建模糊查询条件的基本方法之一，它用于设置单个字段的 LIKE 条件。  

```java
LambdaQueryWrapper<User> lambdaQueryWrapper = new LambdaQueryWrapper<>();
lambdaQueryWrapper。like(User::getName, "王");
```

名字里面带王的都算

```java
-- 普通 Wrapper 和 Lambda Wrapper 生成的 SQL 相同
SELECT * FROM user WHERE name LIKE '%王%'
```

这时候有人就要问了：

做一个左模糊或者右模糊匹配要怎么来呢：

>  默认情况下，`notLike` 方法会在搜索值前后添加 `%`，实现全模糊排除。如果需要排除左模糊或排除右模糊匹配，可以使用 `notLikeRight` 或 `notLikeLeft` 方法。  
>

如上。

## 1.3 isnull
`isNull` 方法是 MyBatis-Plus 中用于构建查询条件的基本方法之一，它用于设置单个字段的 IS NULL 条件。  

```java
LambdaQueryWrapper<User> lambdaQueryWrapper = new LambdaQueryWrapper<>();
lambdaQueryWrapper。isNull(User::getName);
```

用来告诉你这玩意是不是空的。

# 后记
2024年10月16日19:59:56

先写这么多，估计还有很多要写的。先放着。今天主要是like这个忘掉了。

