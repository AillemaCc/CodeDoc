# 第五天
今天继续css

## CSS如何运行
也就是说
浏览器如何获取css和html
并将他们加载成网页

首先 当浏览器或者你自己 展示一个页面或者描述一个文件的时候
他必须兼顾文件的内容或者文件的样式信息
下面我们将会描述处理文件的标准流程
当然了 只是相对的标准流程

1.浏览器载入html文件
2.将html文件转化为一个dom（document object model） dom是文件在计算机内存当中的表现形式
3.接下来，浏览器会拉取这个html文件的大部分资源 比如嵌入到页面的图片 视频 css样式。js则会稍后进行处理。在这部分当中我们不讲js的内容了
4.浏览器拉取到css会进行解析，根据选择器的不同类型，把他们分到不同的“桶”当中。浏览器根据他找到的不同的选择器，将不同的规则应用在对应的dom的节点当中。并且添加节点依赖的样式。**这个中间步骤称为渲染树。**
5.上述的规则应用于渲染树之后，渲染树会依照应该出现的结构进行布局
6.网页展示到屏幕上

## 关于dom
一个dom有一个树形结构 标记语言当中的每一个元素
任何东西都对应着结构树当中的一个节点
节点由节点本身和其他dom节点的关系定义
有些节点有父节点
有些节点有兄弟节点

事实上 一个dom示例比较有用：
现有一段html代码：
~~~~html
<p>
  Let's use:
  <span>Cascading</span>
  <span>Style</span>
  <span>Sheets</span>
</p>
~~~~
接下来是他的dom
~~~~
P
├─ "Let's use:"
├─ SPAN
|  └─ "Cascading"
├─ SPAN
|  └─ "Style"
└─ SPAN
    └─ "Sheets"
~~~~
`在这个 DOM 中，<p>元素对应了父节点，它的子节点是一个 text 节点和三个对应了<span>元素的节点，SPAN节点同时也是他们中的 Text 节点的父节点。`
上图就是浏览器怎么解析之前那个 HTML 片段——它生成上图的 DOM 树形结构并将它按照如下输出到浏览器：
<p>
  Let's use:
  <span>Cascading</span>
  <span>Style</span>
  <span>Sheets</span>
</p>

那我们将css添加到文件里加以渲染呢
浏览器会解析 HTML 并创造一个 DOM，然后解析 CSS。

## 浏览器遇到无法解析CSS代码的情况
在之前的文章中我们提到了浏览器并不会同时实现所有的新 CSS，此外很多人也不会使用最新版本的浏览器。鉴于 CSS 一直不断的开发，因此领先于浏览器可以识别的范围，那么你也许会好奇当浏览器遇到无法解析的 CSS 选择器或声明的时候会发生什么呢？

答案就是浏览器什么也不会做，继续解析下一个 CSS 样式！

如果一个浏览器在解析你所书写的 CSS 规则的过程中遇到了无法理解的属性或者值，它会忽略这些并继续解析下面的 CSS 声明。在你书写了错误的 CSS 代码（或者误拼写），又或者当浏览器遇到对于它来说很新的还没有支持的 CSS 代码的时候上述的情况同样会发生（直接忽略）。

相似的，当浏览器遇到无法解析的选择器的时候，他会直接忽略整个选择器规则，然后解析下一个 CSS 选择器。

换言之 错误的部分会被忽略

这样做好处多多，代表着你使用最新的 CSS 优化的过程中浏览器遇到无法解析的规则也不会报错。当你为一个元素指定多个 CSS 样式的时候，浏览器会加载样式表中的最后的 CSS 代码进行渲染（样式表，优先级等请读者自行了解），也正因为如此，你可以为同一个元素指定多个 CSS 样式来解决有些浏览器不兼容新特性的问题（比如指定两个width）。

这一特点在你想使用一个很新的 CSS 特性但是不是所有浏览器都支持的时候（浏览器兼容）非常有用，举例来说，一些老的浏览器不接收calc()(calculate 的缩写，CSS3 新增，为元素指定动态宽度、长度等，注意此处的动态是计算之后得一个值) 作为一个值。我可能使用它结合像素为一个元素设置了动态宽度（如下），老式的浏览器由于无法解析忽略这一行；新式的浏览器则会把这一行解析成像素值，并且覆盖第一行指定的宽度。

## CSS选择器
选择器是来指定网页上我们想要样式化的html元素的工具

## 选择器列表
如果你有多个使用相同样式的 CSS 选择器，那么这些单独的选择器可以被混编为一个“选择器列表”，这样，规则就可以应用到所有的单个选择器上了。
如果我的h1和.special类有相同的 CSS 那么就组合成一个选择器列表
~~~~css
h1, 
.special{
color:blue
}
~~~~
中间加上逗号 再换行

要注意的是 当使用选择器列表时 假如任何一个选择器无效了
*整条规则都会被忽略*

## 选择器的种类
### 类型 类 id选择器
~~~~css
#对类型：
h1 {
}
#对类：
.box {
}
#对id
#unique {
}
~~~~

### 标签属性选择器
根据一个元素上的某个标签属性的存在以选择元素的不同方式
或者根据一个有特定值的标签属性是否存在来选择

### 伪类与伪元素
这组选择器包含了伪类，用来样式化一个元素的特定状态。例如:hover伪类会在鼠标指针悬浮到一个元素上的时候选择这个元素：
它还可以包含了伪元素，选择一个元素的某个部分而不是元素自己。例如，::first-line是会选择一个元素（下面的情况中是`<p>`）中的第一行，类似`<span>`包在了第一个被格式化的行外面，然后选择这个`<span>`。
~~~~css
p::first-line {
}
~~~~


**下面我们详细的学习各种选择器**
***
## 类型，类和ID选择器

这可能是最常用到的
### 类型选择器
标签名选择器或者元素选择器
因为他选择了一个标签或者说元素
大小写不敏感

### 全局选择器
一个型号
选中所有内容
它能让选择器更加易读
假如我想选中article元素的第一子元素
（好吧我还不知道什么是第一子元素）
不管是什么元素，都给他加粗
我可以将:first-child选择器用作article元素选择器的一个后代选择器：
~~~~
article :first-child {
}
~~~~
但是这会和article:first-child混淆，而后者选择了作为其他元素的第一子元素的article元素。
为了避免这种混淆，我们可以向:first-child选择器加入全局选择器，这样选择器所做的事情很容易就能看懂。
选择器正选中article元素的任何第一子元素：

*锇，这在说什么呢*

### 类选择器
一个点开头
会选择文档中应用了这个类的所有物件

### 指向特定元素的类
建立一个指向应用一个类的特定元素。
这个网站又开始垃圾了
李子加载不出来
好了加载出来了

比如说有如下例子：
~~~~html
<h1 class="highlight">Class selectors</h1>
<p>Veggies es bonus vobis, proinde vos postulo essum magis <span class="highlight">kohlrabi welsh onion</span> daikon amaranth tatsoi tomatillo
    melon azuki bean garlic.</p>

<p class="highlight">Gumbo beet greens corn soko <strong>endive</strong> gumbo gourd. Parsley shallot courgette tatsoi pea sprouts fava bean collard
    greens dandelion okra wakame tomato. Dandelion cucumber earthnut pea peanut soko zucchini.</p>
~~~~
你能看到的是，h1 span p都被标记上了highlight类
假如在css当中像这样
~~~~css
.highlight {
  background-color: yellow;
}
~~~~
那么大家都被会打上高亮的黄色
假如像这样
~~~~css
span.highlight {
  background-color: yellow;
}

h1.highlight {
  background-color: pink;
}
~~~~
在css规定出两个指向特定元素的类，第一个指向的特定元素是span
第二个指向的特定元素是h1

这种方式使 CSS 没那么可复用，因为类现在只会应用到那个特定元素，在认为规则也该应用到其他元素的时候，你会需要另外加上一个选择器。

### 多个类被应用的时候 指向一个元素
对一个元素应用许多个类
然后分别指向他们
或者仅仅在选择器中存在所有这些类的时候选择这一元素

*上面这个是人能理解的话吗我请问了*

在下面的示例中，有一个包含了一条笔记的`<div>`。灰色的边框在盒子带有notebox类的时候应用。如果它还有一个warning或是danger类，我们改变border-color。

~~~~html
<div class="notebox">
    This is an informational note.
</div>

<div class="notebox warning">
    This note shows a warning.
</div>

<div class="notebox danger">
    This note shows danger!
</div>

<div class="danger">
    This won't get styled — it also needs to have the notebox class
</div>
~~~~

~~~~css
.notebox {
  border: 4px solid #666;
  padding: .5em;
}

.notebox.warning {
  border-color: orange;
  font-weight: bold;
}

.notebox.danger {
  border-color: red;
  font-weight: bold;
}
~~~~
他会展示这样一个结果：<img src="http://photos.swindle.icu/picture/typora%E5%9B%BE%E7%89%87%E5%AD%98%E5%82%A8/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202024-10-29%20145049.png" style="zoom:80%;" />

第一个 仅仅应用了notbox
第二个 在notbox的基础上 warning了
第三个 在notbox的基础上 danger了
第四个 没有notbox

### id选择器
以#开头 基本上和类选择器一样用
在一篇文章当中 一个id只会用到一次
他能选中设定了id的元素
你可以在id前面加上类型选择器
这是个很垃圾的方式
算了
不想写了

## 属性选择器
从 HTML 的学习中，你已经知道，元素可以带有属性，它提供了关于如何标记的更详细信息。CSS 中，你能用属性选择器来选中带有特定属性的元素。

### 存否和值选择器
这些选择器允许：基于一个元素自身是否存在（例如herf）
或者
基于各式不同的按属性值的匹配，来选取元素

就是所谓的存在吗？这里面有吗？

下面这些例子可以看到这些选择器怎么使用：
* 使用 li[class] 我们就能匹配任何有class属性的选择器 这匹配了除了第一项之外的所有项
* li[class=“a”]匹配一个带有a类的选择器，不过不会选中一部分值为a而另一部分是另一个用空格隔开的值的类，它选中了第二项。
* li[class~="a"]会匹配一个a类，不过也可以匹配一列用空格分开、包含a类的值，它选中了第二和第三项。

下面是这个的具体示例：
~~~~html
<h1>Attribute presence and value selectors</h1>
<ul>
  <li>Item 1</li>
    <li class="a">Item 2</li>
    <li class="a b">Item 3</li>
    <li class="ab">Item 4</li>
</ul>
~~~~

~~~~css
li[class] {
  font-size: 200%;
}

li[class="a"] {
  background-color: yellow;
}

li[class~="a"] {
  color: red;
}
~~~~
这么说吧 2 3 4都是li元素 都被放大了
严格带有a的 没有其他东西的会变成黄色 那就是2
相对带有a的 除了严格带有a的包含在内之外 有空格分割的字符串 也就是把a独立出来的形如”a b“，也可以被第三个所匹配
但是第四个不行 ab是一个整体了

### 子字符串匹配选择器
这些选择器让更高级的属性的值的子字符串的匹配变得可行。例如，如果你有box-warning和box-error类，想把开头为“box-”字符串的每个物件都匹配上的话，你可以用[class^="box-"]来把它们两个都选中。

* [attr^=value] 	li[class^="box-"] 	匹配带有一个名为attr的属性的元素，其值开头为value子字符串。
* [attr$=value] 	li[class$="-box"] 	匹配带有一个名为attr的属性的元素，其值结尾为value子字符串
* [attr*=value] 	li[class*="box"] 	匹配带有一个名为attr的属性的元素，其值的字符串中的任何地方，至少出现了一次value子字符串。

### 大小写敏感
如果你想在大小写不敏感的情况下，匹配属性值的话，你可以在闭合括号之前，使用i值。这个标记告诉浏览器，要以大小写不敏感的方式匹配 ASCII 字符。没有了这个标记的话，值会按照文档语言对大小写的处理方式，进行匹配——HTML 中是大小写敏感的。
~~~~css
li[class^="a" i] {
  color: red;
}
~~~~


## 伪类和伪元素
光看名字可能并不好理解什么是伪类和伪元素

那么
### 什么是伪类
伪类是一种选择器
选择处于特定状态的元素
一种状态当然可以是一种类
比如
当他们是这一类型的第一个元素/当鼠标指针悬浮在元素上面
他们就出现了某种不同
这能够在html当中减少多余的类

在格式上 伪类就是开头为冒号的关键字：
:pseudo-class-name

简单的伪类示例：
如果我们想要让一篇文章中的第一段变大加粗，可为此段加上一个类，然后为那个类添加 CSS。但这背叛了我们使用伪类的初衷
假如我们不加类，我们可以使用:first-child伪类选择器——这将一直选中文章中的第一个子元素
也就是说 假如我们新增加了一个段落，就不需要再把之前的类挪到新的段落里面了

### 用户行为伪类
一些伪类只会在用户以某种方式和文档交互的时候应用。这些用户行为伪类，有时叫做动态伪类，表现得就像是一个类在用户和元素交互的时候加到了元素上一样

    :hover——上面提到过，只会在用户将指针挪到元素上的时候才会激活，一般就是链接元素。
    :focus——只会在用户使用键盘控制，选定元素的时候激活。

当然了 还有许多其他的

### 伪元素是啥
伪元素以类似方式表现，不过表现得是像你往标记文本中加入全新的 HTML 元素一样，而不是向现有的元素上应用类。伪元素开头为双冒号::。
例如，如果你想选中一段的第一行，你可以把它用一个span元素包起来，然后使用元素选择器；不过，如果包起来的单词/字符数目长于或者短于父元素的宽度，这样做会失败。由于我们一般不会知道一行能放下多少单词/字符——因为屏幕宽度或者字体大小改变的时候这也会变——通过改变 HTML 的方式来可预测地这么做是不可能的
::first-line伪元素选择器会值得信赖地做到这件事——即使单词/字符的数目改变，它也只会选中第一行。

### 伪类和伪元素结合起来
如果你想让第一段的第一行加粗，你需要把:first-child和::first-line选择器放到一起。试着编辑前面的实时示例，让它使用下面的 CSS。这里的意思是，我们想选择一个article元素里面的第一个p元素的第一行。
~~~~css
article p:first-child::first-line {
  font-size: 120%;
  font-weight: bold;
}
~~~~

### 生成带有：：before和：：after的内容
这两个是一组特别的伪元素，他们和content属性一起使用。
更推荐的用法是插入一个图标，例如下面的示例加入的一个小箭头，作为一个视觉性的提示
~~~~css
.box::after {
  content: " ➥";
}
~~~~
他就会在box这个类标记的元素后面，插入一个小箭头

## 更多的伪类和伪元素的参考见：
https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Building_blocks/Selectors/Pseudo-classes_and_pseudo-elements