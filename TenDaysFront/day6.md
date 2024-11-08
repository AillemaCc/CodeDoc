# 今天是第六天了

## 最后一种选择器 关系选择器
这是因为他们在其他选择器之间和其他选择器与文档内容之间
建立了一种有用的关系

### 后代选择器
后代选择器——典型用单个空格（" "）字符——组合两个选择器，比如，第二个选择器匹配的元素被选择，如果他们有一个祖先（父亲，父亲的父亲，父亲的父亲的父亲，等等）元素匹配第一个选择器。选择器利用后代组合符被称作后代选择器。

现在这个mdndoc不说人话了

我们看一个例子

~~~~css
.box p {
  color: red;
}
~~~~

~~~~html
<div class="box"><p>Text in .box</p></div>
<p>Text not in .box</p>
~~~~
这个后代选择器就选择了box当中的p
让他变红
同样是p但是不在box当中
不变红

### 子代关系选择器
是一个大鱼号
	只会在选择器选中直接子元素的时候匹配。继承关系上更远的后代则不会匹配。例如，只选中作为<article>的直接子元素的<p>元素：
	下个示例中，我们弄了个有序列表，内嵌于另一个无序列表里面。我用子代关系选择器，只选中为<ul>的直接子元素的<li>元素，给了它们一个顶端边框。
	如果你移去指定子代选择器的>的话，你最后得到的是后代选择器，所有的<li>会有个红色的边框。

效果就是 只有ul里面的li会有红色的边框
ol里面的li不会有边框
因为ol继承关系更远了

~~~~html
<ul>
  <li>Unordered item</li>
  <li>Unordered item
    <ol>
      <li>Item 1</li>
      <li>Item 2</li>
    </ol>
  </li>
</ul>
~~~~
~~~~css
ul > li {
  border-top: 5px solid red;
}
~~~~

### 邻接兄弟

让我想起战场兄弟了我说白了

邻接兄弟选择器
一个加号

用来选中恰好处于另一个在继承关系上的 同级的 元素旁边的物件

例如
	例如，选中所有紧随<p>元素之后的<img>元素：
	p + img
	常见的使用场景是，改变紧跟着一个标题的段的某些表现方面，就像是我下面的示例那样。这里我们寻找一个紧挨<h1>的段，然后样式化它。
	如果你往<h1>和<p>之间插入其他的某个元素，例如<h2>，你将会发现，段落不再与选择器匹配，因而不会应用元素邻接时的前景和背景色
在这就不展示了 总而言之
*同级+紧邻*
条件两个不能缺少一个


### 通用兄弟

	如果你想选中一个元素的兄弟元素，即使它们不直接相邻，你还是可以使用通用兄弟关系选择器（~）。要选中所有的<p>元素后任何地方的<img>元素，我们会这样做
后面只要有，就直接选中出来了


## 层级 优先级 继承
这些概念决定着如何将 CSS 应用到 HTML 中，以及如何解决冲突。


## 冲突规则：
CSS 代表层叠样式表（Cascading Style Sheets），理解第一个词层叠（cascade）很重要——层叠的表现方式是理解 CSS 的关键。

在某些时候，在做一个项目过程中你会发现一些应该产生效果的样式没有生效。
通常的原因是你创建了两个应用于同一个元素的规则。
与层叠密切相关的概念是优先级（specificity），决定在发生冲突的时候应该使用哪条规则。
设计元素样式的规则可能不是期望的规则


这里也有继承的概念，也就是在默认情况下，一些 css 属性继承 当前元素的 父元素上设置的值，有些则不继承。这也可能导致一些恶心的东西

## 层叠
样式表层叠：简单地说 就是css规则的顺序决定了当冲突发生的时候，哪一条规则会被实际使用
	下面的示例中，我们有两个关于 <h1> 的规则。<h1> 最后显示蓝色——这两个规则来自同一个源，且具有相同的元素选择器，有相同的优先级，所以顺序在最后的生效。
~~~~CSS
h1 {
  color: red;
}
h1 {
  color: blue;
}
~~~~
H1最后会是蓝色


## 优先级
这是浏览器决定当多个规则有不同选择器对应相同元素的时候 需要使用哪个规则
这基本上是一个尺度
一个衡量选择器具体选择哪些区域的尺度

* 一个元素选择器不是很具体，则会选择页面上该类型的所有元素，所以它的优先级就会低一些。
* 一个类选择器稍微具体点，则会选择该页面中有特定 class 属性值的元素，所以它的优先级就要高一点。


## 继承
一些设置在父元素上的 CSS 属性是可以被子元素继承的，有些则不能。
那他妈哪些能哪些不能啊
举一个例子，如果你设置一个元素的 color 和 font-family，每个在里面的元素也都会有相同的属性，除非你直接在元素上设置属性。
说的有点垃圾

## 优先级算法
你会发现在一些情况下，有些规则在最后出现，但是却应用了前面的具有冲突的规则。这是因为前面的有更高的优先级——它范围更小，因此浏览器就把它选择为元素的样式。

就像前面看到的，类选择器的权重大于元素选择器，因此类上定义的属性将覆盖应用于元素上的属性。

这里需要注意虽然我们考虑的是选择器，以及应用在选中对象上的规则，但不会覆盖所有规则，只覆盖相同的属性。

这样可以避免重复的 CSS。一种常见的做法是给基本元素定义通用样式，然后给不同的元素创建对应的类。举个例子，在下面的样式中我给 2 级标题定义了通用样式，然后创建了一些类只修改部分属性的值。最初定义的值应用于所有标题，然后更具体的值通过对应类来实现。

~~~~html
<h2>Heading with no class</h2>
<h2 class="small">Heading with class of small</h2>
<h2 class="bright">Heading with class of bright</h2>
~~~~
~~~~css
h2 {
  font-size: 2em;
  color: #000;
  font-family: Georgia, 'Times New Roman', Times, serif;
}

.small {
  font-size: 1em;
}

.bright {
  color: rebeccapurple;
}
~~~~
出现了这样的效果
![效果图](http://photos.swindle.icu/picture/typora%E5%9B%BE%E7%89%87%E5%AD%98%E5%82%A8/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202024-10-30%20154652.png)

一个选择器的优先级可以说是由三个不同的值（或分量）相加，可以认为是百（ID）十（类）个（元素）——三位数的三个位数：

    ID：选择器中包含 ID 选择器则百位得一分。
    类：选择器中包含类选择器、属性选择器或者伪类则十位得一分。
    元素：选择器中包含元素、伪元素选择器则个位得一分。

## 内联样式
内联样式，即 style 属性内的样式声明，优先于所有普通的样式，无论其优先级如何。这样的声明没有选择器，但它们的优先级可以理解为 1-0-0-0；即无论选择器中有多少个 ID，它总是比其他任何优先级的权重都要高。

## 层叠层
这一部分可能很重要吧

*如果你是 CSS 的新手，刚开始可能会觉得这部分的内容与本课程的其他部分相比不太相关，而且有些学术化。然而，了解层叠层的基本知识对于你在项目中遇到它们时会非常有帮助。随着你对 CSS 的不断使用，理解层叠层以及如何充分利用它们的功能将能够避免在处理来自不同团队、插件和开发人员的 CSS 代码库时遇到的很多问题。当你使用来自多个源的 CSS，或当存在冲突的 CSS 选择器和竞争优先级时，又或者当你考虑使用 !important 时，层叠层最为相关。*

首先，应用于元素的每个css属性，只能有一个值
可以通过开发者工具中检查元素来查看应用于元素的所有属性值
工具的样式面板 显示了应用在被检查元素上的所有属性值
以及匹配的选择器和css源文件