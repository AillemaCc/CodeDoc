# 今天是第三天

## 绝对url和相对url

绝对url指向在web上绝对位置定义的位置
包括协议和域名
比如说
如果 index.html 页面上传到了 projects 这一个目录。并且 projects 目录位于 web 服务站点的根目录，web 站点的域名为 `https://www.example.com`，那么这个页面就可以通过 `https://www.example.com/projects/index.html` 访问（或者通过 `https://www.example.com/projects/` 来访问，因为在没有指定特定的 URL 的情况下，大多数 web 服务器会默认访问加载 index.html 这类页面）
不管绝对 URL 在哪里使用，它总是指向确定的相同位置。

而对于相对url
他就会指向一个所谓的相对位置
这个取决于引用的文件的实际位置
例如，如果我们想从示例文件链接 https://www.example.com/projects/index.html 转到相同目录下的一个 PDF 文件，URL 就是文件名（例如 project-brief.pdf），没有其他的信息要求。如果 PDF 文件能够在 projects 的子目录 pdfs 中访问到，相对路径就是 pdfs/project-brief.pdf（对应的绝对 URL 是 https://www.example.com/projects/pdfs/project-brief.pdf）

## 文本格式进阶 描述列表
我们在之前学过有序列表和无序列表了
第三种列表类型是描述列表
用例子来说明比较容易
~~~~html
<dl>
  <dt>内心独白</dt>
  <dd>
    戏剧中，某个角色对自己的内心活动或感受进行念白表演，这些台词只面向观众，而其他角色不会听到。
  </dd>
  <dt>语言独白</dt>
  <dd>
    戏剧中，某个角色把自己的想法直接进行念白表演，观众和其他角色都可以听到。
  </dd>
  <dt>旁白</dt>
  <dd>
    戏剧中，为渲染幽默或戏剧性效果而进行的场景之外的补充注释念白，只面向观众，内容一般都是角色的感受、想法、以及一些背景信息等。
  </dd>
</dl>
~~~~
<dl>
  <dt>内心独白</dt>
  <dd>
    戏剧中，某个角色对自己的内心活动或感受进行念白表演，这些台词只面向观众，而其他角色不会听到。
  </dd>
  <dt>语言独白</dt>
  <dd>
    戏剧中，某个角色把自己的想法直接进行念白表演，观众和其他角色都可以听到。
  </dd>
  <dt>旁白</dt>
  <dd>
    戏剧中，为渲染幽默或戏剧性效果而进行的场景之外的补充注释念白，只面向观众，内容一般都是角色的感受、想法、以及一些背景信息等。
  </dd>
</dl>
描述列表使用与其他列表类型不同的闭合标签——`<dl>`；此外，每一项都用 `<dt>`（description term）元素闭合。每个描述都用 `<dd>`（description definition）元素闭合。
所以可以这么说 项+描述构成了描述列表
一个项可以有多个描述

## 块引用
块级元素：一个段落 多个段落 一个列表
从其他地方被引用了
应该把它用`<blockquote>` 元素包裹起来表示，并且在 cite 属性里用 URL 来指向引用的资源。例如，下面的示例代码就是引用的 MDN 的 `<blockquote>` 元素页面：

算了 我并不知道这个有什么用

## 行内引用
也不写了

## 这网站今天老是进不去 我的学习之路苦难重重

## 文档与网站架构
规划基本的网站架构

## 文档的基本组成部分
* 页眉：一个大标题
* 导航栏：去各个区段
* 主内容：无需多言
* 侧边栏：外围信息
* 页脚：脚
~~~~html
<!doctype html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>二次元俱乐部</title>
    <link
      href="https://fonts.googleapis.com/css?family=Open+Sans+Condensed:300|Sonsie+One"
      rel="stylesheet" />
    <link
      href="https://fonts.googleapis.com/css?family=ZCOOL+KuaiLe"
      rel="stylesheet" />
    <link href="style.css" rel="stylesheet" />
  </head>

  <body>
    <header>
      <!-- 本站所有网页的统一主标题 -->
      <h1>聆听电子天籁之音</h1>
    </header>

    <nav>
      <!-- 本站统一的导航栏 -->
      <ul>
        <li><a href="#">主页</a></li>
        <!-- 共 n 个导航栏项目，省略…… -->
      </ul>

      <form>
        <!-- 搜索栏是站点内导航的一个非线性的方式。 -->
        <input type="search" name="q" placeholder="要搜索的内容" />
        <input type="submit" value="搜索" />
      </form>
    </nav>

    <main>
      <!-- 网页主体内容 -->
      <article>
        <!-- 此处包含一个 article（一篇文章），内容略…… -->
      </article>

      <aside>
        <!-- 侧边栏在主内容右侧 -->
        <h2>相关链接</h2>
        <ul>
          <li><a href="#">这是一个超链接</a></li>
          <!-- 侧边栏有 n 个超链接，略略略…… -->
        </ul>
      </aside>
    </main>

    <footer>
      <!-- 本站所有网页的统一页脚 -->
      <p>© 2050 某某保留所有权利</p>
    </footer>
  </body>
</html>
~~~~

`<header>：页眉。
    <nav>：导航栏。
    <main>：主内容。主内容中还可以有各种子内容区段，可用<article>、<section> <div> 等元素表示。
    <aside>：侧边栏，经常嵌套在 <main> 中。
    <footer>：页脚。`

## 布局元素细节
* main存放每个页面独有的内容 每个页面上只能用一次main，并且直接位于body当中。最好不要把main元素嵌套进其他元素
* header是简介形式的内容，尽管说这也是一个元素
* 没什么可以写的了
* 好吧还有点
* aside是一些间接信息
* section是内容方面的元素 就像一个一个区域。
* 没了

## 无语义元素
有时你会发现，对于一些要组织的项目或要包装的内容，现有的语义元素均不能很好对应。有时候你可能只想将一组元素作为一个单独的实体来修饰来响应单一的用 CSS 或 JavaScript。为了应对这种情况，HTML 提供了 `<div>` 和 `<span>` 元素。应配合使用 class 属性提供一些标签，使这些元素能易于查询。
**这里应该非常重要**
