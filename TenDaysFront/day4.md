# 第四天

## 无语义元素
今天接着无语义元素来写
有时你会发现，对于一些要组织的项目或要包装的内容，现有的语义元素均不能很好对应。
有时候 我只想让一组元素作为一个单独的实体 来**修饰**或者**响应**css或者js
html提供div和span 这两个元素 以及配合这两个元素的class属性

## span
span是一个内联的无语义元素
在mdn文档当中 他说是最好用于无法找到更好的语义来包含内容或者不想增加特定的含义时
但事实上这样的span在这个博客的前端当中被大量使用
可能后面的vue学习会给我答案吧

span就是一个文本行一样的东西
~~~~html
<p>
  国王喝得酩酊大醉，在凌晨 1 点时才回到自己的房间，踉跄地走过门口。<span
    class="editor-note"
    >[编辑批注：此刻舞台灯光应变暗]</span
  >.
</p>
~~~~

## div
div是块级的无语义元素
~~~~html
<div class="shopping-cart">
  <h2>购物车</h2>
  <ul>
    <li>
      <p>
        <a href=""><strong>银耳环</strong></a
        >：$99.95.
      </p>
      <img src="../products/3333-0985/" alt="Silver earrings" />
    </li>
    <li>...</li>
  </ul>
  <p>售价：$237.89</p>
</div>
~~~~
这时，通过css可以定义购物车的样式


## br 换行元素
在段落当中换行
~~~~html
<p>
  从前有个人叫小高<br />
  他说写 HTML 感觉最好<br />
  但他写的代码结构语义一团糟<br />
  他写的标签谁也懂不了。
</p>
~~~~
<p>
  从前有个人叫小高<br />
  他说写 HTML 感觉最好<br />
  但他写的代码结构语义一团糟<br />
  他写的标签谁也懂不了。
</p>

没有 br 元素，这段会直接显示在长长的一行中

## 主题性终端元素
生成水平分割线

## 多媒体与嵌入
上图

## img元素
img元素是一个空元素
空元素无法包含子内容和结束标签
他需要两个属性才能起作用
*src alt*

src包含一个url 这个url指向要嵌入页面的图像
没有src属性 img元素就没有图像可以加载了

alt属性的值是图片的文本描述
用于在图片无法显示的情况下使用

## 宽度和高度
width 宽度
height 高度
他们的值是不带单位的整数
以像素为单位表示图像的宽度和高度
使用 HTML 属性来指定图片的实际大小是一个好的实践，但你不应该使用它们来调整图片的大小。
在将图片放到网页上之前，你应使用图像编辑器将其设置为正确的大小。
如果确实需要更改图片的大小，应该使用 CSS 来实现。

## 图像标题
title 类似于超链接
鼠标悬停在图片上 会有个提示

## figure 和 figcaption

可赋标题内容元素

~~~~html
<figure>
  <img src="/media/cc0-images/elephant-660-480.jpg" alt="Elephant at sunset" />
  <figcaption>An elephant at sunset</figcaption>
</figure>
~~~~
包含图像和图像的描述
他们一起是一个figure元素


## css背景图片
再说

# CSS 现在不用再说了
CSS（层叠样式表）用于设置和布置网页——例如，更改内容的字体、颜色、大小和间距，将其拆分为多个列，或添加动画和其他装饰功能。
css是指定html文档如何展示给用户的一门语言
css是一门基于规则的语言

能定义 用于你的网页中的 特定元素样式的 一组规则
好吧这玩意怎么这么长

比如说“我希望页面中的主标题是红色的大字”

下面这段css规则就能实现上面的效果
~~~~css
h1 {
  color: red;
  font-size: 5em;
}
~~~~
用html就不怎么行

上面这段css规则的语法
由一个选择器开头 **他选择了我们要用来添加样式的html元素**
在上面的例子当中 我们选择了h1

接着是一对大括号
大括号内部定义一个或者多个 *形式*为*属性*
每个*声明*都指定了我们所选择元素的一个属性
比如第一个声明指定了我们选择的h1的颜色

好了 这部分没了

## css模块
css由许多模块构成

现在不学

## css规范
不是给我们看的

## 开始吧

~~~~html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>开始学习 CSS</title>
  </head>

  <body>
    <h1>我是一级标题</h1>

    <p>
      这是一个段落文本。在文本中有一个 <span>span element</span> 并且还有一个
      <a href="http://example.com">链接</a>.
    </p>

    <p>这是第二段。包含了一个 <em>强调</em> 元素。</p>

    <ul>
      <li>项目 1</li>
      <li>项目 2</li>
      <li>项目 <em>三</em></li>
    </ul>
  </body>
</html>
~~~~
我们要让这个html文档能够遵循我们给他的css规则
有三种方式可以实现
现在我么你倾向于用普遍并且有用的方式

**在文档的开头连接CSS**

在head元素当中添加如下代码：
~~~~html
<link rel="stylesheet" href="styles.css" />
~~~~
前提是真的有一个styles.css
他们俩在同一级文件目录之下
语句块里面，我们用属性 rel，让浏览器知道有 CSS 文档存在（所以需要遵守 CSS 样式的规定），并利用属性 href 指定，寻找 CSS 文件的位置。


## 样式化html元素
我们之前把h1变红了
是通过用选择器选择h1
我们也可以用元素选择器选择其他元素
~~~~css
p,
li {
  color: green;
}
~~~~
选择了所有段落 所有列表

## 改变元素的默认行为
浏览器有自己的一套css规则
就拿我们的无序列表 ul 举个例子，它自带项目符号，不过要是你跟它有仇，你就可以这样移除它们：
~~~~css
li {
  list-style-type: none;
}
~~~~
## 使用类名
你可以给html元素加一个类名
这样能实现这样的效果：

*“我知道你想干啥，你想用这种方式样式化这一片元素，又想用那种方式样式化那一片元素，真贪心。不过没关系，你可以给 HTML 元素加个类名（class），再选中那个类名，这样就可以了，大家基本上都这么用。”*

举个例子：
~~~~html
<ul>
  <li>项目一</li>
  <li class="special">项目二</li>
  <li>项目 <em>三</em></li>
</ul>
~~~~
项目二就这么特殊上了
在css当中 要选中这个special类 只需要在选择器的开头 加上一个点

~~~~CSS
.special {
  color: orange;
  font-weight: bold;
}
~~~~
举个例子，你可能也想让段落里边的 span 一起又橙又粗起来。试试把special 类属性加上去，保存，刷新，哇，生活就是这么美好。


有时候你发现 选择器当中 元素和类一起出现
这是说选中每一个 special的li元素
但这样不好用
因为这样special就不对其他元素起作用了

~~~~css
li.special {
  color: orange;
  font-weight: bold;
}
~~~~

## 根据元素在文档中的位置确定样式

有时候，你希望某些内容根据它在文档中的位置而有所不同。这里有很多选择器可以为你提供帮助，但现在我们只介绍几个选择器。在我们的文档中有两个 `<em>`元素——一个在段落内，另一个在列表项内。仅选择嵌套在`<li>` 元素内的`<em>`我们可以使用一个称为包含选择符的选择器，它只是单纯地在两个选择器之间加上一个空格。
将以下规则添加到样式表。
~~~~css
li em{
color:rebeccapurple;
}
~~~~
该选择器将选择`<li>`内部的任何`<em>`元素（`<li>`的后代）

## 也可以根据状态确定样式

一个直观的例子就是当我们修改链接的样式时。当我们修改一个链接的样式时我们需要定位（针对） `<a>` （锚）标签。取决于是否是未访问的、访问过的、被鼠标悬停的、被键盘定位的，亦或是正在被点击当中的状态，这个标签有着不同的状态。你可以使用 CSS 去定位或者说针对这些不同的状态进行修饰——下面的 CSS 代码使得没有被访问的链接颜色变为粉色、访问过的链接变为绿色。

~~~~css
a:link {
  color: pink;
}

a:visited {
  color: green;
}
~~~~
你可以改变链接被鼠标悬停的时候的样式，例如移除下划线，下面的代码就实现了这个功能。
~~~~css
a:hover {
  text-decoration: none;
}
~~~~
我们对鼠标悬停于链接上的情况删除了下划线。你当然可以让超链接在任何情况下都没有下划线。但需要注意的是，对一个实际的站点，需要让浏览者知道“链接是链接”。为了让浏览者注意到一段文字中的某些部分是可点击的，最好保留 link 状态下的下划线。— 这是下划线的本来作用。不管你用 CSS 来做什么，都应当使得变化后的文档看上去更加清晰明了。


## 选择器和选择符
我忘了什么是选择符了

## 在html当中应用css
有三种方法 外部样式表 内部样式表 内联样式

### 外部样式表：
单独扩展名为.css的文件里面
可以将一个css文件连接到多个网页上
用同一个css样式表为所有网页确定样式
link元素在此处很重要
当然，herf引用的路径可能相当的不同
~~~~html
<!-- 在当前目录中，引用子文件夹 styles 中的样式表文件 -->
<link rel="stylesheet" href="styles/style.css" />

<!-- 在当前目录中，引用子文件夹 styles 中的子文件夹 general 中的样式表文件 -->
<link rel="stylesheet" href="styles/general/style.css" />

<!-- 在当前目录的父级目录中，引用子文件夹 styles 中的样式表文件 -->
<link rel="stylesheet" href="../styles/style.css" />
~~~~

### 内部样式表：
一个内部样式表驻留在html文档内部 要创建一个内部样式表
要把css放置在包含在head元素当中的style元素内
长这样
~~~~html
<!doctype html>
<html lang="zh-CN">
  <head>
    <meta charset="utf-8" />
    <title>我的 CSS 测试</title>
    <style>
      h1 {
        color: blue;
        background-color: yellow;
        border: 1px solid black;
      }
      p {
        color: red;
      }
    </style>
  </head>
  <body>
    <h1>Hello World!</h1>
    <p>这是我的第一个 CSS 示例</p>
  </body>
</html>
~~~~

可维护性太差

### 内联样式 
shit 别用


## 优先级
假如冲突了 比如有一个 p 选择器，将段落文本设置为蓝色。然而，也有一个类将所选元素的文本设置为红色。
一个在前面 一个在后面
在后面的会覆盖在前面的样式
这是**层叠**规则

## 属性和值
在最基本的层面上 css由两个组成部分组成
属性和值
* 属性是人类可读的标识符 指示想要更改的样式特征
* 值是每个特定的属性拥有的值 这个值表示如何对属性施加样式。

单个属性和值。属性名为 color，值为 blue。

当一个属性与一个值配对时，这种配对被称为 CSS 声明。CSS 声明可以在 CSS 声明块中找到。

最后，CSS 声明块与选择器配对，以生成 CSS 规则集（或称 CSS 规则）。


## 函数
大多数值是相对简单的关键字或者数值
但是也有一些值以函数的形式出现
### calc函数
简单的计算
### transform的不同取值
rotate（） 旋转
### 我相信还有非常多 不写了

## @规则
css当中的@rules是一些特殊的规则
提供了关于css应该执行什么或者如何表现的指令
有些艾特规则比较简单
只有一个关键词和一个值
例如@import
将一个样式表导入另一个css样式表

另外一个常见的规则可能是@media，它被用来创建媒体查询。媒体查询使用条件逻辑来应用 CSS 样式。

在下面的例子中，样式表为 body 元素定义了一个默认的粉红色背景。然而，如果浏览器的视口宽于 30em，接下来的媒体查询则定义了蓝色背景。


## 简写属性

一些属性：如 font、background、padding、border 和 margin 等属性称为简写属性。它们允许在一行中设置多个属性值，从而节省时间并使代码更整洁。
但是降低可读性我说白了
~~~~css
/* 在像 padding 和 margin 这样的 4 值简写语法中，
   数值的应用顺序是上、右、下、左（从顶部顺时针方向）。
   也有其他的简写类型，例如 2 值简写，
   它为顶部/底部设置 padding/margin，然后是左侧/右侧 */
padding: 10px 15px 15px 5px;
~~~~
上面的规则设置与下面的等价：
~~~~css
padding-top: 10px;
padding-right: 15px;
padding-bottom: 15px;
padding-left: 5px;
~~~~

## 注释
CSS 中的注释以 /* 开头，以 */ 结尾。

## 空白
空白是指实际的空格 制表符 换行符
就像浏览器忽略了 HTML 中的空白一样，浏览器也忽略了 CSS 中的空白。空白的价值在于它可以提高可读性。
在下面的例子中，每个声明（和规则的开始/结束）都有自己的行。这可以说是一种编写 CSS 的好方法。它使人们更容易维护和理解 CSS。

难道正常人不这么编程吗

真有不正常的人我说白了
~~~~css
body {font: 1em/150% Helvetica, Arial, sans-serif; padding: 1em; margin: 0 auto; max-width: 33em;}
@media (min-width: 70em) { body { font-size: 130%;}}

h1 {font-size: 1.5em;}

div p, #id:first-line {background-color: red; border-radius: 3px;}
div p {margin: 0; padding: 1em;}
div p + p {padding-top: 0;}
~~~~
