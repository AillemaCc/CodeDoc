# 第十天
## 在js当中找bug
一般来说 当然也不止在js当中
代码错误主要分为两种：
* 语法错误：代码中存在拼写错误，将导致程序完全或部分不能运行，通常你会收到一些出错信息。只要熟悉语言并了解出错信息的含义，你就能够顺利修复它们。
* 逻辑错误：有些代码语法虽正确，但执行结果和预期相悖，这里便存在着逻辑错误。这意味着程序虽能运行，但会给出错误的结果。由于一般你不会收到来自这些错误的提示，它们通常比语法错误更难修复。
[这个会很有用](https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/First_steps/What_went_wrong)

## 如何存储你需要的信息：变量
在之前的一天零一小时的学习当中，你可能已经大概知道了js是什么，能用js来干什么。他是怎么和web蛋糕的其他几层通力合作，以及他的一部分主要特性。当然，这些都只是入门的内容
在这一段当中，我们将深入了解真正的基础知识，学习如何使用 JavaScript 最基础的构建单元——变量。
### 变量是什么
一个变量，就是一个用于存放数值的容器。这个数值可能是一个用于累加计算的数字，或者是一个句子中的字符串。变量的独特之处在于它存放的数值是可以改变的。让我们看一个简单的例子：
~~~~html
<button>Press me</button>
~~~~
~~~~js
const button = document.querySelector("button");

button.onclick = function () {
  let name = prompt("What is your name?");
  alert("Hello " + name + ", nice to see you!");
};
~~~~

在上面的例子中，点击按钮之后，第一行代码会在屏幕上弹出一个对话框，让你输入名字，然后存储输入的名字到一个变量。第二行代码将会显示包含你名字的欢迎信息，你的名字就是从之前的变量里面读取的。
变量的另一个特性就是它们能够存储任何的东西——不只是字符串和数字。变量可以存储更复杂的数据，甚至是函数
我们说，变量是用来存储数值的，那么有一个重要的概念需要区分。变量不是数值本身，它们仅仅是一个用于存储数值的容器。你可以把变量想象成一个个用来装东西的纸箱子。
### 声明变量
**使用变量的第一步**
声明一个变量的语法是在 var 或 let 关键字之后加上这个变量的名字：
### 初始化变量
在定义之后给他赋值

但一般我们都这样做
~~~~
let myName = "Chris";
~~~~
### “为什么有 var 和 let 呢？"
历史遗留问题
原因是有些历史性的。回到最初创建 JavaScript 时，是只有 var 的。在大多数情况下，这种方法可以接受，但有时在工作方式上会有一些问题——它的设计会令人困惑或令人讨厌。因此，let 是在现代版本中的 JavaScript 创建的一个新的关键字，用于创建与 var 工作方式有些不同的变量，解决了过程中的问题。
**简而言之，用let**
### 更新变量
一旦变量赋值，你可以通过简单地给它一个不同的值来更新它。就像赋值变量那样
### 命名规则
你可以给你的变量赋任何你喜欢的名字，但有一些限制。一般你应当坚持使用拉丁字符 (0-9,a-z,A-Z) 和下划线字符。
**小写驼峰命名法**
### 动态类型
JavaScript 是一种“动态类型语言”，这意味着不同于其他一些语言 (译者注：如 C、JAVA)，你不需要指定变量将包含什么数据类型（例如 number 或 string）
例如，如果你声明一个变量并给它一个带引号的值，浏览器就会知道它是一个字符串
即使它包含数字，但它仍然是一个字符串，所以要小心

## 条件语句
我几乎跳过了所有js当中的基础数据结构
例如，在游戏中，如果玩家的生命值变成了 0，那么游戏就结束了。在天气应用中，如果在早晨运行，就显示一张日出的图片；如果在晚上，就显示星星和月亮的图片。
在下面的内容当中，我们会探索一下js当中的条件语句如何工作
基础的部分和其他编程语言相差不大
~~~~html
<label for="weather">选择今天的天气：</label>
<select id="weather">
  <option value="">--作出选择--</option>
  <option value="sunny">晴天</option>
  <option value="rainy">雨天</option>
  <option value="snowing">雪天</option>
  <option value="overcast">阴天</option>
</select>

<p></p>
~~~~
~~~~js
const select = document.querySelector("select");
const para = document.querySelector("p");

select.addEventListener("change", setWeather);

function setWeather() {
  const choice = select.value;

  if (choice === "sunny") {
    para.textContent = "阳光明媚。穿上短裤吧！去海滩，或公园，吃个冰淇淋。";
  } else if (choice === "rainy") {
    para.textContent = "外面下着雨；带上雨衣和雨伞，不要在外面呆太久。";
  } else if (choice === "snowing") {
    para.textContent =
      "大雪纷飞，天寒地冻！最好呆在家里喝杯热巧克力，或者去堆个雪人。";
  } else if (choice === "overcast") {
    para.textContent =
      "虽然没有下雨，但天空灰蒙蒙的，随时都可能变天，所以要带一件雨衣以防万一。";
  } else {
    para.textContent = "";
  }
}
~~~~
~~~~
    这里我们有 HTML <select> 元素让我们选择不同的天气，以及一个简单的段落。
    在 JavaScript 中，我们同时存储了对 <select> 和 <p> 的引用，并对 <select> 添加了一个事件监听器，因此，当它的值改变时，setWeather() 函数被执行。
    当函数运行时，我们首先新建了一个 choice 变量去存储当前被选的 <select> 中的值。接着我们用条件判断语句根据 choice 的值选择性的展示段落中的文本。注意 else if () { } 块中的条件是怎么被判断的，除了第一个，它是在 if () { } 中被判断的。
    最后一个 else { } 中的选择通常被叫做“最后招数”——在所有的条件都不为 true 时其中的代码会被执行。在这个例子中，如果用户没有选择任何一个选项，它会将段落中的文本清空，例如当用户决定重新选择最开始出现的“--作出选择--”选项时，就会有这样的效果。
~~~~

### 简单介绍一下三目运算符
~~~~
condition ? 运行这段代码 : 否则，运行这段代码
~~~~
## 就先这样吧
