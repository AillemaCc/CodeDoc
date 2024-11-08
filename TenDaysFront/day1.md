# 快速入门html css js

## html
HyperText Markup Language 超文本标记语言
告知浏览器如何组织页面的标记语言

构成要素为：元素
元素是最基本组成部分

构成要素为：标签
标签可以实现样式

eg：
````html
<p>My cat is very grumpy</p>
````
上面例子包括：
* 开始标签：标志元素开始或者生效的地方
* 内容：元素的内容
* 结束标签：结束了

上面的例子是一个段落元素

## 嵌套元素
元素可以实现嵌套
````html
<p>My cat is <strong>very</strong> grumpy.</p>
````

## 块级元素 内联元素
这是元素的分类
* 块级元素：在页面里面就是一块一块的。作为页面上的结构元素。基本会换行 <p>
* 内联元素：出现在块级元素当中，环绕文档内容。不换行。


## 空元素
有些元素只有一个标签
````html
<img
  src="https://roy-tian.github.io/learning-area/extras/getting-started-web/beginner-html-site/images/firefox-icon.png"
  alt="Firefox 图标" />
````
没有开始标签没有结束标签

## 属性
元素可以有自己的属性 这很正常
属性包含元素的额外信息

属性必须包含：

    一个空格，它在属性和元素名称之间。如果一个元素具有多个属性，则每个属性之间必须由空格分隔。
    属性名称，后面跟着一个等于号。
    一个属性值，由一对引号（""）引起来。

两个属性之间需要有一个空格

## 为元素添加属性

关于<a> 这是一个锚元素。他有herf属性。可以出示连接
当然他可以添加不止一个属性 其余的还包括
title
target
更多的属性可以参考
https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/a

以下为一个例子
````html
<p>A link to my <a href="https://www.mozilla.org/" title="The Mozilla homepage" target="_blank">favorite website</a>.</p>
````
在段落当中添加了一个锚元素
猫元素有三个属性 链接 title target

## 布尔属性
布尔属性只能有一个值
这个值一般和属性名称相同
例如，考虑 disabled 属性，你可以将其分配给表单输入元素。用它来禁用表单输入元素，这样用户就不能输入了。被禁用的元素通常有一个灰色的外观。

## 省略包围属性值的引号
我们在之前说到：

		一个属性值，由一对引号（""）引起来。
那么什么时候会出现：

		<a href=https://www.mozilla.org/>favorite website</a>

这样的情况呢？
属性只有这一个属性值的时候就可以
但我们**不推荐**
结束

## 单引号还是双引号
风格问题
但应该注意单引号和双引号不能在一个属性值里面混用

## html文档
这段应该很重要
因为单独的html元素组成了这一部分
例子如下
````html
<!doctype html>
<html lang="zh-CN">
  <head>
    <meta charset="utf-8" />
    <title>我的测试站点</title>
  </head>
  <body>
    <p>这是我的页面</p>
  </body>
</html>
````
在上面的例子当中，我们有这样一些部分：

```


<html></html>: <html> 元素。这个元素包裹了页面中所有的内容，有时被称为根元素。

<head></head>: <head> 元素。这个元素是一个容器，它包含了所有你想包含在 HTML 页面中但不在 HTML 页面中显示的内容。这些内容包括你想在搜索结果中出现的关键字和页面描述、CSS 样式、字符集声明等等。以后的章节中会学到更多相关的内容。

<meta charset="utf-8">: <meta> 元素。这个元素代表了不能由其他 HTML 元相关元素表示的元数据，比如 <base>、<link>、<script>、<style> 或 <title>。charset 属性将你的文档的字符集设置为 UTF-8，其中包括绝大多数人类书面语言的大多数字符。有了这个设置，页面现在可以处理它可能包含的任何文本内容。没有理由不对它进行设置，它可以帮助避免以后的一些问题。

<title></title>: <title> 元素。这设置了页面的标题，也就是出现在该页面加载的浏览器标签中的内容。当页面被加入书签时，页面标题也被用来描述该页面。

<body></body>: <body> 元素。包含了你访问页面时所有显示在页面上的内容，包含文本、图片、视频、游戏、可播放音频轨道等等。

```

现在让我们来一个例子：

~~~html
<h1>经典回忆</h1>
<p>
 相思无用，惟别而已。别期若有定，千般煎熬又何如？莫道黯然销魂，何处<strong>柳暗花明</strong>？<br>
 ——《<a href="https://zh.wikipedia.org/zh-hans/神鵰俠侶">神雕侠侣</a>》
</p>
<img src="https://roy-tian.github.io/learning-area/extras/tools/playable-code/images/sdxl.jfif" alt="《神雕侠侣》作品图片">
~~~

## 空白
就是空白

## 实体引用：在html当中包含一个特殊字符
在 HTML 中，字符 <、>、"、' 和 & 是特殊字符。它们是 HTML 语法自身的一部分，那么你如何将这些字符包含进你的文本中呢，比如说如果你真的想要在文本中使用符号 & 或者小于号，而不想让它们被浏览器视为代码并被解释？

我们必须使用字符引用——表示字符的特殊编码，它们可以在那些情况下使用。每个字符引用以符号 & 开始，以分号（;）结束。

具体怎么引用：
https://zh.wikipedia.org/wiki/XML%E4%B8%8EHTML%E5%AD%97%E7%AC%A6%E5%AE%9E%E4%BD%93%E5%BC%95%E7%94%A8%E5%88%97%E8%A1%A8


## 注释
<!-- 和 -->

## 没了
没了
2024年10月25日