# 第七天
昨天基本没写什么东西
今天也差点不想写什么东西了
我刚才还以为今天是周五来着

## 接着昨天的层叠层开始写
CSS 中的 C 代表“层叠”。这是样式层叠在一起的方法。用户代理经过几个非常明确定义的步骤来确定每个元素的每个属性的值。我们将在这里简要列出这些步骤，然后深入研究第 4 步——层叠层，就是你来到这里学习的内容：

    相关声明：找到所有具有匹配每个元素的选择器的声明代码块。
    重要性：根据规则是普通还是重要对规则进行排序。重要的样式是指设置了 !important 标志的样式。
    来源：在两个按重要性划分的分组内，按作者、用户或用户代理这几个来源对规则进行排序。
    层：在六个按重要性和来源划分的分组内，按层叠层进行排序。普通声明的层顺序是从创建的第一个到最后一个，然后是未分层的普通样式。对于重要的样式，这个顺序是反转的，但保持未分层的重要样式优先权最低。
    优先级：对于来源层中优先权相同的竞争样式，按优先级对声明进行排序。
    出现顺序：当两个来源层的优先权相同的选择器具有相同的优先级时，最后声明的具有最高优先级的选择器的属性值获胜。

对于每一步，只有“仍在运行”的声明才会进入下一轮“竞争”。如果只有一个声明在运行，那么它就“赢了”，后续的步骤就没有意义了


## 来源和层叠
有三种层叠来源类型
用户代理样式表
用户样式表
作者样式表

浏览器根据来源和重要性 将每个声明分为六个来源分组 有八个优先权级别
（怎么能这么多的）
下面是优先权顺序：

    用户代理普通样式
    用户普通样式
    作者普通样式
    正在动画的样式
    作者重要样式
    用户重要样式
    用户代理重要样式
    正在过渡的样式


	“用户代理”指的是浏览器。“用户”指的是是网站访问者。“作者”指的是你，开发者。用 <style> 元素直接在元素上声明的样式是作者样式。不包括动画和过渡样式，用户代理普通样式具有最低优先权；用户代理重要样式具有最高优先权。

## 来源和优先级
对于每个属性 
在优先级当中获胜的声明是来自基于权重具有优先权的来源的声明
暂时忽略层的情况下 来自具有最高优先权的来源的值将被应用
如果获胜的来源对于一个元素有多个属性的声明
那么将比较这些竞争属性值的选择器的优先级
但是对于不同来源之间的选择器 不比较优先级
	在下面的例子中，有两个链接。第一个没有应用作者样式，所以只有用户代理样式被应用（以及你个人的用户样式，如果有的话）。第二个被作者样式设置了 text-decoration 和 color，即使作者样式表中的选择器具有 0-0-0 的优先级。作者样式“获胜”的原因是，当来自不同来源的样式发生冲突时，具有优先权的来源的规则被应用，而不管没有优先权的来源中的优先级如何。
~~~~css
:where(a.author) {
  text-decoration: overline;
  color: red;
}
~~~~
~~~~html
<p><a href="https://example.org">User agent styles</a></p>
<p><a href="https://example.org" class="author">Author styles</a></p>
~~~~
	在撰写本文时，用户代理样式表中“竞争”的选择器是 a:any-link，它具有 0-1-1 的优先级权重。虽然这大于作者样式表中 0-0-0 的选择器，但即使你当前的用户代理中的选择器不同，也没关系：作者和用户代理来源之间从不比较优先级权重。


# 我决定跳过层叠层这部分

# 盒！
好吧 这事实上是包裹css元素的一个东西
就像收纳元素的盒子

## 区块盒子与行内盒子
在 CSS 中，我们有几种类型的盒子，一般分为区块盒子（block boxes）和行内盒子（inline boxes）。类型指的是盒子在页面流中的行为方式以及与页面上其他盒子的关系。盒子有内部显示（inner display type）和外部显示（outer display type）两种类型。
一般来说，可以使用 display 属性为显示类型设置各种值，该属性可以有多种值。

## 外部显示类型
一个拥有 block 外部显示类型的盒子会表现出以下行为：
* 盒子会产生换行
* 宽度和高度属性
* 内边距外边距 边框 会把其他元素从当前盒子周围推开
* 如果没有指定宽度，方框将会沿着行的方向扩展以填充容器当中的可用空间 大多数情况下 盒子会变得和容器一样的宽 占据可用空间的100%


某些html元素 如h1 p 默认使用block作为外部显示类型
一个拥有inline外部显示类型的盒子会表现出如下行为：
* 盒子不会产生换行
* 宽度和高度属性不起作用
* 垂直方向的内边距 外边距 以及边框会被应用 但是不会把其他处于inline状态的盒子推开
* 水平方向的内边距、外边距以及边框会被应用且会把其他处于 inline 状态的盒子推开。
	某些 HTML 元素，如 <a>、 <span>、 <em> 以及 <strong>，默认使用 inline 作为外部显示类型。

## 内部显示类型
盒子有内部显示类型 他决定了盒子内部元素的布局方式
例如，可以通过设置 display: flex; 来更改内部显示类型。该元素仍将使用外部显示类型 block 但内部显示类型将变为 flex。该方框的任何直接子代都将成为弹性（flex）项，并按照弹性盒子规范执行。