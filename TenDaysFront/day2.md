# 今天是第二天

现在看来这篇文档应该是十天html
## html元信息

在一个html文档当中
有<head></head>这样一个标签规定了头部的部分
头里面有什么？
今天说这个

## 什么是html头部
对于：
~~~
<!doctype html>
<html lang="zh-CN">
  <head>
    <meta charset="utf-8" />
    <title>我的测试页面</title>
  </head>
  <body>
    <p>这是我的页面</p>
  </body>
</html>
~~~
<head></head>里面带的就是了
页面在浏览器加载之后
这里面的内容不会在浏览器当中显示
它的作用是
**保存页面的一些元数据**
大型页面的头部会很大，让我们尝试去看一个网站的头部
~~~
<head>
    <meta charset="UTF-8">
    <title>哔哩哔哩 (゜-゜)つロ 干杯~-bilibili</title>
    <meta name="description" content="哔哩哔哩（bilibili.com)是国内知名的视频弹幕网站，这里有及时的动漫新番，活跃的ACG氛围，有创意的Up主。大家可以在这里找到许多欢乐。">
    <meta name="keywords" content="bilibili,哔哩哔哩,哔哩哔哩动画,哔哩哔哩弹幕网,弹幕视频,B站,弹幕,字幕,AMV,MAD,MTV,ANIME,动漫,动漫音乐,游戏,游戏解说,二次元,游戏视频,ACG,galgame,动画,番组,新番,初音,洛天依,vocaloid,日本动漫,国产动漫,手机游戏,网络游戏,电子竞技,ACG燃曲,ACG神曲,追新番,新番动漫,新番吐槽,巡音,镜音双子,千本樱,初音MIKU,舞蹈MMD,MIKUMIKUDANCE,洛天依原创曲,洛天依翻唱曲,洛天依投食歌,洛天依MMD,vocaloid家族,OST,BGM,动漫歌曲,日本动漫音乐,宫崎骏动漫音乐,动漫音乐推荐,燃系mad,治愈系mad,MAD MOVIE,MAD高燃">
    <meta name="renderer" content="webkit">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="spm_prefix" content="333.1007">
    <meta name="referrer" content="no-referrer-when-downgrade">
    <meta name="applicable-device" content="pc">
    <meta http-equiv="Cache-Control" content="no-transform">
    <meta http-equiv="Cache-Control" content="no-siteapp">
    <meta name="server_render" content="is_server_render">

    <link rel="dns-prefetch" href="//s1.hdslb.com">
    <link rel="apple-touch-icon" href="https://i0.hdslb.com/bfs/static/jinkela/long/images/512.png">
    <link rel="shortcut icon" href="https://i0.hdslb.com/bfs/static/jinkela/long/images/favicon.ico">
    <link rel="canonical" href="https://www.bilibili.com/">
    <link rel="alternate" media="only screen and (max-width: 640px)" href="https://m.bilibili.com">
    <link rel="stylesheet" href="//s1.hdslb.com/bfs/static/jinkela/long/font/medium.css" media="all" onload="this.media='all'">
    <link rel="stylesheet" href="//s1.hdslb.com/bfs/static/jinkela/long/font/regular.css" media="all" onload="this.media='all'">
    <script>window._BiliGreyResult={"method":"gray","grayVersion":"55002"}</script><script src="//s1.hdslb.com/bfs/static/laputa-home/client/assets/svgfont.2cee4853.js" async=""></script><script src="https://www.bilibili.com/gentleman/polyfill.js?features=es2015%2Ces2016%2Ces2017%2Ces2018%2Ces2019%2Ces2020%2Ces2021%2Ces2022%2CglobalThis&amp;flags=gated"></script>   
    <script type="text/javascript" src="//s1.hdslb.com/bfs/seed/jinkela/short/bmg/register/fallback.js"></script><script src="//s1.hdslb.com/bfs/seed/jinkela/kv-sdk/index.js"></script>
    
    <link rel="stylesheet" href="//s1.hdslb.com/bfs/seed/jinkela/short/bili-theme/map.css">
    <link rel="stylesheet" href="//s1.hdslb.com/bfs/seed/jinkela/short/bili-theme/light_u.css">
    <link id="__css-map__" rel="stylesheet" href="//s1.hdslb.com/bfs/seed/jinkela/short/bili-theme/light.css">
  
    <script>window.__SERVER_CONFIG__={"serverBuvid":"B253B0A8-29B3-DF33-152F-248BA7619B5469945infoc","homeFeedColumn":"4","browserResolution":"1022-990","isModern":true,"aiexp":"1","remove_channel_lift":0,"ab_test":{"for_ai_home_version":"V8","tianma_banner_inline":"CONTROL","tianma_banner_live":"RENDER","in_theme_version":"CLOSE","enable_web_push":"DISABLE","enable_player_bar":"DISABLE","enable_ad_feedback":"DISABLE"},"constants":{"previewTipCountingSecond":1,"previewCountingSecond":4,"nanoVersionHash":"cfa2c429","nanoVersionPcdnHash":"cfa2c429","tianma_banner_inline_V0":-1,"tianma_banner_inline_V1":10},"uniq_page_id":688836771571};</script>
    <script type="text/javascript">
    window.__NANO_VERSION_HASH__ = "cfa2c429"
  </script>
    <script type="text/javascript">
      // 当没有值时，给一个合适页面使用的
      if (!window.__NANO_VERSION_HASH__) {
        window.__NANO_VERSION_HASH__ = '17866fdb'
      }
    </script>
    <script type="text/javascript">
      ;(function () {
        if (document.querySelector('meta[name=server_render]')) {
          return
        }
        var ua = window.navigator.userAgent,
          agents = ['Android', 'Phone', 'SymbianOS', 'iPod'],
          isPC = true
        if (/\sVR\s/g.test(ua)) return
        for (var i = 0, len = agents.length; i < len; i++) {
          if (ua.indexOf(agents[i]) > 0) {
            isPC = false
            break
          }
        }
        if (!isPC) {
          window.location.href = window.location.href.replace('www', 'm')
        }
      })()
    </script>
    <script type="text/javascript">
      window.spmReportData = {}
      window.reportConfig = {
        sample: 1,
        msgObjects: 'spmReportData',
        errorTracker: true
      }
      function getCookie(name) {
        var reg = new RegExp('(^| )' + name + '=([^;]*)(;|$)')
        var r = document.cookie.match(reg)
        return r ? unescape(r[2]) : null
      }
      function fsrCb() {
        if (window.performance && window.performance.timing) {
          window.performance.timing.firstscreenfinish = new Date().getTime()
        }
      }
      // 图片降级使用
      function imgOnError(img) {
        typeof window.imgAutoFallbackOnError === 'function' && window.imgAutoFallbackOnError(img)
      }
      // 图片降级使用
      function imgOnLoad(img) {
        typeof window.imgAutoFallbackOnLoad === 'function' && window.imgAutoFallbackOnLoad(img)
      }
      function lqipCb(img) {
        var lqip =
          img && img.parentNode && img.parentNode.querySelector('.lqip')
        if (lqip) {
          lqip.classList.add('is-active')
        }
      }
      if (history.scrollRestoration) {
        history.scrollRestoration = 'manual'
      }
      window.page_load_time = Date.now()
    </script>
    <script type="text/javascript">
    if (!window.abtest) {
      window.abtest = {
        'b_ut': getCookie('b_ut'),
        'home_version': 'V8',
        'i-wanna-go-back': getCookie('i-wanna-go-back'),
        'in_new_ab': true,
        'ab_version': {"for_ai_home_version":"V8","tianma_banner_inline":"CONTROL","tianma_banner_live":"RENDER","in_theme_version":"CLOSE","enable_web_push":"DISABLE","enable_player_bar":"DISABLE","enable_ad_feedback":"DISABLE"},
        'ab_split_num': {"for_ai_home_version":160,"tianma_banner_inline":160,"tianma_banner_live":160,"in_theme_version":135,"enable_web_push":1,"enable_player_bar":160,"enable_ad_feedback":160},
      }
    }
~~~
b站的，一眼望不到头

## 添加标题
title元素用来添加文档的标题
h1为body添加顶级标题

title也称为你添加书签的时候，浏览器建议你使用的书签名

## 元数据：meta元素
元数据是描述数据的数据

比如：
~~~
<meta charset="utf-8" />
~~~
告诉你这个网页字符 是utf8

又比如：
~~~
<meta name="author" content="Chris Mills" />
<meta
  name="description"
  content="The MDN Web Docs Learning Area aims to provide
complete beginners to the Web with all they need to know to get
started with developing web sites and applications." />
~~~
许多meta元素包含了name和content属性
* name指定着该meta元素的类型 说明了该元素包含了什么类型的信息
* content指定了该meta元素的内容
比如上面的第一个meta元素
类型就是作者
内容就是克里斯米尔斯
这个作者类型的meta元素的内容就是克里斯米尔斯

很多网站有自己的元数据协议
那和我没关系

## 在站点里面加点自定义图标
这个我已经做到了
~~~
<link rel="shortcut icon" href="./static/img/favicon1.ico">
~~~~
这个没什么所谓

## 重中之重：在html当中应用css和js
css：让网页样式更好看
js：让网页能够交互

它们分别使用 <link 元素以及 <script 元素。

link 元素经常位于文档的头部，它有 2 个属性，rel="stylesheet" 表明这是文档的样式表，而 href 包含了样式表文件的路径：
~~~
<link rel="stylesheet" href="my-css-file.css" />
~~~
script 元素也应当放在文档的头部，并包含 src 属性来指向需要加载的 JavaScript 文件路径，同时最好加上 defer 以告诉浏览器在解析完成 HTML 后再加载 JavaScript。这样可以确保在加载脚本之前浏览器已经解析了所有的 HTML 内容。这样你就不会因为 JavaScript 试图访问页面上不存在的 HTML 元素而产生错误。
~~~
<script src="my-js-file.js" defer></script>
~~~

接下来有这样一个示例：
~~~javascript
const list = document.createElement('ul');
const info = document.createElement('p');
const html = document.querySelector('html');

info.textContent = 'Below is a dynamic list. Click anywhere on the page to add a new list item. Click an existing list item to change its text to something else.';

document.body.appendChild(info);
document.body.appendChild(list);

html.onclick = function() {
  const listItem = document.createElement('li');
  const listContent = prompt('What content do you want the list item to have?');
  listItem.textContent = listContent;
  list.appendChild(listItem);

  listItem.onclick = function(e) {
    e.stopPropagation();
    const listContent = prompt('Enter new content for your list item');
    this.textContent = listContent;
  }
}
~~~
~~~css
html {
  background-color: green;
  font-size: 20px;
}

ul {
  background: red;
  padding: 10px;
  border: 1px solid black;
}

li {
  margin-left: 20px;
}
~~~
~~~html
<!DOCTYPE html>
<html lang="en-US">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width">
    <title>Meta examples</title>

    <meta name="author" content="Chris Mills">
    <meta name="description" content="This is an example page to demonstrate usage of metadata on web pages.">

    <meta property="og:image" content="https://developer.mozilla.org/mdn-social-share.png">
    <meta property="og:description" content="This is an example page to demonstrate usage of metadata on web pages.">
    <meta property="og:title" content="Metadata; The HTML &lt;head&gt;, on MDN">

    <link rel="Shortcut Icon" href="favicon.ico" type="image/x-icon">

    <link rel="stylesheet" href="style.css">
    <script src="script.js" defer></script>
  </head>
  <body>
    <h1>Meta examples</h1>

    <p>Japanese example: ご飯が熱い。</p>

    
  </body>
</html>
~~~
### HTML文档结构
- `<!DOCTYPE html>`: 声明文档类型为HTML5。
- `<html lang="en-US">`: 设置页面语言为美式英语。
- `<meta charset="utf-8">`: 指定文档使用的字符编码为UTF-8，确保可以正确显示所有字符，包括非英文字符。
- `<meta name="viewport" content="width=device-width">`: 使页面在移动设备上能够自适应屏幕宽度。
- `<title>Meta examples</title>`: 设置浏览器标签页的标题。
- `<meta name="author" content="Chris Mills">`: 提供作者信息。
- `<meta name="description" content="...">`: 提供页面描述，常用于搜索引擎结果摘要。
- Open Graph (OG) 元数据：
  - `<meta property="og:image" content="...">`: 指定社交媒体分享时的图片。
  - `<meta property="og:description" content="...">`: 提供社交媒体分享时的描述。
  - `<meta property="og:title" content="...">`: 提供社交媒体分享时的标题。
- `<link rel="Shortcut Icon" href="favicon.ico" type="image/x-icon">`: 设置网站的快捷图标（通常出现在浏览器标签页旁边）。
- `<link rel="stylesheet" href="style.css">`: 链接到一个名为`style.css`的外部样式表。
- `<script src="script.js" defer></script>`: 引入一个名为`script.js`的外部JavaScript文件，并设置`defer`属性以延迟执行直到文档解析完成。


而对于css和js文件来说
在HTML中，`<ul>` 和 `<li>` 是用来创建无序列表的标签。

`<ul>` 代表“无序列表”（Unordered List）。它是一个容器标签，用于包含一系列的列表项。默认情况下，浏览器会在每个列表项前显示一个项目符号（通常是圆点），但这个样式可以通过CSS来改变。

`<li>` 代表“列表项”（List Item）。它是 `<ul>` 或者有序列表 `<ol>` 的子元素，用来表示列表中的每一个单独的条目。每个 `<li>` 元素都可以包含文本、图片或者其他嵌套的HTML元素。
~~~
<ul>
  <li>Apple</li>
  <li>Banana</li>
  <li>Cherry</li>
</ul>
~~~

## 没了
结束
2024年10月26日


## 头文件的结束了，文本处理基础的这部分开始了
HTML 的主要工作之一是赋予文本结构，使浏览器能够按照开发者的意图显示 HTML 文档。

## 标题
h123456标签
## 段落
p标签

## 三国演义来了

~~~html
<h1>三国演义</h1>

<p>罗贯中</p>

<h2>第一回 宴桃园豪杰三结义 斩黄巾英雄首立功</h2>

<p>
  话说天下大势，分久必合，合久必分。周末七国分争，并入于秦。及秦灭之后，楚、汉分争，又并入于汉……
</p>

<h2>第二回 张翼德怒鞭督邮 何国舅谋诛宦竖</h2>

<p>
  且说董卓字仲颖，陇西临洮人也，官拜河东太守，自来骄傲。当日怠慢了玄德，张飞性发，便欲杀之……
</p>

<h3>却说张飞</h3>

<p>
  却说张飞饮了数杯闷酒，乘马从馆驿前过，见五六十个老人，皆在门前痛哭。飞问其故，众老人答曰：“督邮逼勒县吏，欲害刘公；我等皆来苦告，不得放入，反遭把门人赶打！”……
</p>
~~~

显示出来这样：
***
<h1>三国演义</h1>

<p>罗贯中</p>

<h2>第一回 宴桃园豪杰三结义 斩黄巾英雄首立功</h2>

<p>
  话说天下大势，分久必合，合久必分。周末七国分争，并入于秦。及秦灭之后，楚、汉分争，又并入于汉……
</p>

<h2>第二回 张翼德怒鞭督邮 何国舅谋诛宦竖</h2>

<p>
  且说董卓字仲颖，陇西临洮人也，官拜河东太守，自来骄傲。当日怠慢了玄德，张飞性发，便欲杀之……
</p>

<h3>却说张飞</h3>

<p>
  却说张飞饮了数杯闷酒，乘马从馆驿前过，见五六十个老人，皆在门前痛哭。飞问其故，众老人答曰：“督邮逼勒县吏，欲害刘公；我等皆来苦告，不得放入，反遭把门人赶打！”……
</p>
***
## 为什么需要结构化
什么结构化不结构化的
结构化有点学术了
其实就是通过规定让大家更好的进行阅读
没了

## 为什么需要语义
没了

## 列表
上面两个问题，之后再来回答吧
这个比较重要
分三种
* 有序列表
* 无序列表
* 描述列表

### 无序列表：
~~~html
<ul>
  <li>豆浆</li>
  <li>油条</li>
  <li>豆汁</li>
  <li>焦圈</li>
</ul>

~~~
老北京吃的就是一个地道
`<li>` 代表“列表项”（List Item）。它是 `<ul>` 或者有序列表 `<ol>` 的子元素，用来表示列表中的每一个单独的条目。每个 `<li>` 元素都可以包含文本、图片或者其他嵌套的HTML元素。

### 有序列表：
~~~html
<ol>
  <li>沿这条路走到头</li>
  <li>右转</li>
  <li>直行穿过第一个十字路口</li>
  <li>在第三个十字路口处左转</li>
  <li>继续走 300 米，学校就在你的右手边</li>
</ol>
~~~
<ol>
  <li>沿这条路走到头</li>
  <li>右转</li>
  <li>直行穿过第一个十字路口</li>
  <li>在第三个十字路口处左转</li>
  <li>继续走 300 米，学校就在你的右手边</li>
</ol>
人类都能理解
他俩也能嵌套

## 重点强调
在 HTML 中我们用 `<em>`（emphasis）元素来标记这样的情况。这样做既可以让文档读起来更有趣，也可以被屏幕阅读器识别，并以不同的语调发出。浏览器默认样式为斜体，但你不应该纯粹为了获得斜体风格而使用这个标签。如果仅仅为了获得斜体样式而不增加语义辅助，你应该使用 `<span>` 元素和一些 CSS，或者是 `<i>` 元素（见下文）。

```html

<p><strong>2016 年 3 月 8 日</strong>到<strong>3 月 15 日</strong>，韩国职业棋士<strong>李世乭（이세돌）<em>九段</em></strong>与由 Google DeepMind 开发的计算机围棋软件 <strong>AlphaGo</strong> 对弈的五局三胜制围棋比赛在韩国<strong>首尔</strong>举行。结果为 AlphaGo 以<strong>四胜一负</strong>的战绩击败李世乭。赛后韩国棋院授予 AlphaGo <strong>荣誉九段</strong>的称号。</p>
```
<p><strong>2016 年 3 月 8 日</strong>到<strong>3 月 15 日</strong>，韩国职业棋士<strong>李世乭（이세돌）<em>九段</em></strong>与由 Google DeepMind 开发的计算机围棋软件 <strong>AlphaGo</strong> 对弈的五局三胜制围棋比赛在韩国<strong>首尔</strong>举行。结果为 AlphaGo 以<strong>四胜一负</strong>的战绩击败李世乭。赛后韩国棋院授予 AlphaGo <strong>荣誉九段</strong>的称号。</p>

## 斜体粗体下划线

只有在没有更合适的元素时，才适合使用 `<b>、<i> 或 <u>` 来表达传统上用粗体、斜体或下划线表达的意思；而通常情况下是有更合适的元素可供使用的。`<strong>、<em>、<mark> 或 <span>` 可能是更加合适的选择。

## 结束
2024年10月26日14:44:44
豹子

## 创建超链接
万物互联
~~~
<p>
  我创建了一个指向
  <a href="https://www.mozilla.org/zh-CN/">Mozilla 主页</a>的链接。
</p>
~~~
<p>
  我创建了一个指向
  <a href="https://www.mozilla.org/zh-CN/">Mozilla 主页</a>的链接。
</p>

## 块级链接

比如标题元素就是一个块级元素
让我们把标题元素变成链接
想让标题元素变为链接，就把它包裹在锚点元素（`<a>`）内，像这个代码段一样：
~~~
<a href="https://developer.mozilla.org/zh-CN/">
  <h1>MDN Web 文档</h1>
</a>
<p>自从 2005 年起，就开始记载包括 CSS、HTML、JavaScript 等网络技术。</p>
~~~

## 图片链接
把图片元素img包裹在链接元素内

## 这个比较重要：叫统一资源定位符（url）与路径（path）快速入门
统一资源定位符（Uniform Resource Locator，URL）是一个定义了在网络上的位置的一个文本字符串。
URL 使用路径查找文件。路径指定文件系统中你感兴趣的文件所在的位置。
### 指向当前目录
相同目录下进行url使用，比如同目录之下有a b两个文件我想在a当中包含一个指向b的超链接，我就只需要指定想要链接到的文件名
~~~
<p>
  要联系某位工作人员，请访问我们的<a href="contacts.html">联系人页面</a>。
</p>
~~~
### 指向子目录
如果有一个在文件夹当中的c文件，我们就要先找到他在哪个文件夹，假如就在文件夹这个文件夹当中吧
~~~
<p>请访问我的<a href="文件夹/c.html">项目主页</a>。</p>
~~~
### 指向上级目录
两个点
..

## 文档片段
超链接除了可以链接到文档外，也可以链接到 HTML 文档的特定部分（被称为文档片段）
要做到这一点，你必须首先给要链接到的元素分配一个 id 属性。通常情况下，链接到一个特定的标题是有意义的，这看起来就像下面这样：
~~~
<h2 id="Mailing_address">邮寄地址</h2>
~~~
这个标题元素有个id属性
