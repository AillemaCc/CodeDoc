# 第八天
我说白了今天学一会
## 盒模型能够显示的例子
下面的示例当中有三个不同的html元素
他们的外部显示类型 都是block
* 在css当中添加了边框的段落 浏览器会将其渲染为一个盒子框 段落从新的行开始，并且能够扩展整个可用宽度
* 使用 display: flex 布局的列表。这就为容器的子项（即弹性项）建立了弹性布局。列表本身是一个区块盒子，与段落一样，会扩展到整个容器的宽度，然后换行
* 一个块级段落 内含两个span段落 这些元素通常是inline，但是其中一个元素的类是 block，令其被设置为 display: block。

效果和代码如下：

![图1](http://photos.swindle.icu/picture/typora%E5%9B%BE%E7%89%87%E5%AD%98%E5%82%A8/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202024-11-03%20150456.png)

第一个规则 
	border: 2px solid rebeccapurple;：设置段落 (<p>) 和无序列表 (<ul>) 的边框为2像素宽的 rebeccapurple 色实线。
    padding: .5em;：设置内边距为0.5em。

第二个规则 
    border: 2px solid blue;：设置所有带有 class="block" 的元素和所有列表项 (<li>) 的边框为2像素宽的蓝色实线。
    padding: .5em;：设置内边距为0.5em。
第三个规则
    display: flex;：将无序列表 (<ul>) 显示为一个弹性容器，使其子元素（通常是 <li>）可以水平排列。
    list-style: none;：移除无序列表的默认项目符号。
第四个规则
	display: block;：将所有带有 class="block" 的元素显示为块级元素，这意味着它们会独占一行。
	
