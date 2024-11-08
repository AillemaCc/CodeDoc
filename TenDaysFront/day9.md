# 第九天
前两天因为各种原因
断更了
今天开始事实上只剩下最后两天
当然 前端学习肯定不会止步在此
最后的两篇文章就入门一下js
## 什么是js
JavaScript 是一种脚本编程语言，它可以在网页上实现复杂的功能，网页展现给你的不再是简单的静态信息，而是实时的内容更新——交互式的地图、2D/3D 动画、滚动播放的视频等等——JavaScript 就在其中。它是标准 Web 技术蛋糕的第三层，其中 HTML 和 CSS 我们已经在学习区的其他部分进行了详细的讲解。

简单回顾一下这个web技术蛋糕
~~~~
    HTML 是一种标记语言，用来结构化我们的网页内容并赋予内容含义，例如定义段落、标题和数据表，或在页面中嵌入图片和视频。
    CSS 是一种样式规则语言，可将样式应用于 HTML 内容，例如设置背景颜色和字体，在多个列中布局内容。
    JavaScript 是一种脚本语言，可以用来创建动态更新的内容，控制多媒体，制作图像动画，还有很多。（好吧，虽然它不是万能的，但可以通过简短的代码来实现神奇的功能。）
~~~~
这三层依次建立，秩序井然。以简单文本标签作为示例。首先用 HTML 将文本标记起来，从而赋予它结构和目的：
~~~~
<button type="button">Player 1: Chris</button>
~~~~
然后我们可以为它加一点 CSS 让它更好看：
~~~~css
button {
  font-family: "helvetica neue", helvetica, sans-serif;
  letter-spacing: 1px;
  text-transform: uppercase;
  border: 2px solid rgb(200 200 0 / 60%);
  background-color: rgb(0 217 217 / 60%);
  color: rgb(100 0 0 / 100%);
  box-shadow: 1px 1px 2px rgb(0 0 200 / 40%);
  border-radius: 10px;
  padding: 3px 10px;
  cursor: pointer;
}
~~~~
实现的效果是这样的![图片](http://photos.swindle.icu/picture/typora%E5%9B%BE%E7%89%87%E5%AD%98%E5%82%A8/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202024-11-04%20134657.png)
之后呢 就可以加上一些js来实现动态行为
~~~~js
const button = document.querySelector("button");

button.addEventListener("click", updateName);

function updateName() {
  const name = prompt("请输入新的名字");
  button.textContent = `Player 1: ${name}`;
}
~~~~
至于js到底可以做什么
技术点如下
* 在变量当中储存有用的值 在上面的例子当中 我们请求客户输入一个新名字 然后将他存到name变量当中
* 操作一段文本：在上面的例子当中 我们操作字符串“player1”，然后把他和name拼接起来 创造出一个完整的文本标签
* 运行代码以响应网页当中发生的特定事件：我们用一个click时间来检测按钮什么时候被点击，然后运行代码 更新文本标签

** js一个非常常见的用途是通过文档对象模型API 动态修改html和css 以更新用户界面 **

## 让我们了解一下jss的运行次序
当浏览器执行到一段 JavaScript 代码时，通常会按从上往下的顺序执行这段代码。这意味着你需要注意代码书写的顺序。比如，我们回到第一个例子中的 JavaScript 代码：
~~~~js
const button = document.querySelector("button");

button.addEventListener("click", updateName);

function updateName() {
  const name = prompt("请输入新的名字");
  button.textContent = `Player 1: ${name}`;
}
~~~~
首先使用 document.querySelector 选定一个按钮，然后使用 addEventListener 给它附上一个事件监听器（第 3 行），使得在它被点击时，updateName() 代码块（5 – 8 行）便会运行。updateName() 代码块（这类可以重复使用的代码块称为“函数”）向用户请求一个新名字，然后把这个名字插入到段落中以更新显示。

如果互换了代码里最初两行的顺序，会导致问题。浏览器开发者控制台将返回一个错误：Uncaught ReferenceError: Cannot access 'button' before initialization。这意味着 button 对象还未初始化，所以我们不能为它增添事件监听器。
** 这是一个很常见的错误，在引用对象之前必须确保该对象已经存在。**


## 解释代码和编译代码
你或许听说过这两个术语：解释（interpret）和编译（compile）。在解释型语言中，代码自上而下运行，且实时返回运行结果。代码在由浏览器执行前，不需要将其转化为其他形式。代码将直接以文本格式被接收和处理。
相对的，编译型语言需要先将代码转化（编译）成另一种形式才能运行。比如 C/C++ 先被编译成机器码，然后才能由计算机运行。程序将以二进制的格式运行，这些二进制内容是由程序源代码产生的。
JavaScript 是轻量级解释型语言。浏览器接受到 JavaScript 代码，并以代码自身的文本格式运行它。技术上，几乎所有 JavaScript 转换器都运用了一种叫做即时编译（just-in-time compiling）的技术；当 JavaScript 源代码被执行时，它会被编译成二进制的格式，使代码运行速度更快。尽管如此，JavaScript 仍然是一门解释型语言，因为编译过程发生在代码运行中，而非之前。
至于他们孰优孰劣 这个不谈了

## 服务器端代码和客户端代码
你或许还听说过服务器端（server-side）和客户端（client-side）代码这两个术语，尤其是在 web 开发时。客户端代码是在用户的电脑上运行的代码，在浏览一个网页时，它的客户端代码就会被下载，然后由浏览器来运行并展示。在本模块中我们讨论的主要是客户端 JavaScript。
而服务器端代码在服务器上运行，然后运行结果才由浏览器下载并展示出来。流行的服务器端 web 语言包括：PHP、Python、Ruby、ASP.NET，甚至有 JavaScript！JavaScript 也可用作服务器端语言，比如现在流行的 Node.js 环境

## 怎么向页面添加js
	可以像添加 CSS 那样将 JavaScript 添加到 HTML 页面中。CSS 使用 <link> 元素链接外部样式表，使用 <style> 元素向 HTML 嵌入内部样式表，而 JavaScript 这里只需一个元素——<script>。我们来看看它是怎么工作的。
### 内嵌
直接在html文档当中的script元素当中添加js代码
body标签下面写就行了
### 外联
~~~~html
<script type="module" src="script.js"></script>
~~~~
## 使用addEventLinstener
与其在 HTML 中包含 JavaScript，不如使用纯 JavaScript 构造。通过 querySelectorAll() 函数，可以选择页面上的所有按钮。然后可以循环遍历这些按钮，使用 addEventListener() 为每个按钮分配一个处理器。代码如下所示：
~~~~js
const buttons = document.querySelectorAll("button");

for (let i = 0; i < buttons.length; i++) {
  buttons[i].addEventListener("click", createParagraph);
}
~~~~
这样写乍看去比 onclick 属性要长一些，但是这样写会对页面上所有按钮生效，无论多少个，或添加或删除，完全无需修改 JavaScript 代码。
大概的意思就是让这些按钮都能够被点击
## 脚本加载策略
页面上的所有 HTML 代码都按其出现的顺序加载。如果使用 JavaScript 去操作页面上的元素（更准确的说，是文档对象模型），那么如果 JavaScript 在 HTML 之前就被加载和解析了，代码将无法运行。
有几种不同的策略来确保 JavaScript 只在 HTML 解析之后运行：
* 在上面的js示例当中，脚本元素放在文档正文的底部。因此只能在html正文的其他部分被解析之后来运行
* 在上面的外部js示例当中，脚本元素放在文档的头部，在解析html正文之前解析。这样从原则上来说是错的。但是我们使用了但是由于我们使用了 `<script type="module">`，代码被视为一个模块，并且浏览器在执行 JavaScript 模块之前会等待所有的 HTML 代码都处理完毕
* 也可以把外部脚本放在正文的底部，但是如果 HTML 内容较多且网络较慢，在浏览器开始获取并加载脚本之前可能需要大量的时间，因此将外部脚本放在头部通常会更好一些

## 山茶初试js情
	我想让你开发一个猜数字游戏。游戏应随机选择一个 1 到 100 之间的自然数，然后邀请玩家在 10 轮以内猜出这个数字。每轮后都应告知玩家的答案正确与否，如果出错了，则告诉他数字是低了还是高了。并且应显示出玩家前一轮所猜的数字。一旦玩家猜对，或者用尽所有机会，游戏将结束。游戏结束后，可以让玩家选择重新开始
### 分解需求
1.随机生成一个1-100自然数
2.记录玩家当前的轮数
3.为玩家提供一种猜测数字的方法
4.一旦有结果提交，先把结果记录下来。以便用户可以看到他们先前的猜测。
5.然后检查它是否正确
6.如果正确：显示祝贺消息；阻止玩家继续猜测；显示控件允许玩家继续开始游戏
7.如果出错并且玩家有剩余轮次：告诉玩家出错；阻止玩家继续猜测；显示控件允许玩家继续开始游戏
8.如果出错，并且玩家没有剩余轮次：告诉玩家游戏结束。阻止玩家继续猜测（这会使游戏混乱）。显示控件允许玩家重新开始游戏。
9.一旦游戏重启，确保游戏的逻辑和 UI 完全重置，然后返回步骤 1。


html文档不做解释
着重对js部分讲解

### 规定变量以保存数据
~~~~js
let randomNumber = Math.floor(Math.random() * 100) + 1;

const guesses = document.querySelector(".guesses");
const lastResult = document.querySelector(".lastResult");
const lowOrHi = document.querySelector(".lowOrHi");

const guessSubmit = document.querySelector(".guessSubmit");
const guessField = document.querySelector(".guessField");

let guessCount = 1;
let resetButton;
~~~~
我草他们都是谁呢？
* randomNumber 随机数 我们用数学算法得出一个 1 到 100 之间的随机数，并赋值给第一个变量
* 接下来的三个常量均存储着一个引用，分别指向 HTML 结果段落中某个元素 在代码后面段落中插入值
* 接下来的两个常量存储对表单文本输入和提交按钮的引用，并用于控制以后提交猜测
* 倒数第二个变量存储一个计数器并初始化为 1（用于跟踪玩家猜测的次数），最后一个变量存储对重置按钮的引用，这个按钮尚不存在（但稍后就有了）。

### 函数
函数是可复用的代码块，可以一次编写，反复运行，从而节省了大量的重复代码。它们真的很有用。定义函数的方法很多，但现在我们先集中考虑当前这个简单的方式。这里我们使用关键字 function 、一个函数名、一对小括号定义了一个函数。随后是一对花括号（{ }）。花括号内部是调用函数时要运行的所有代码。

要运行一个函数代码时，可以输入函数名加一对小括号。
比如一个简单的函数定义如下
~~~~js
function checkGuess() {
  alert("I am a placeholder");
}
~~~~
在浏览器当中使用开发者工具
输入checkGuess()
就能得到浏览器弹出的提示
*I am a placeholder*
### 条件语句
下面是checkguess函数的完整版本
~~~~js
function checkGuess() {
  const userGuess = Number(guessField.value);
  if (guessCount === 1) {
    guesses.textContent = "Previous guesses: ";
  }
  guesses.textContent += `${userGuess} `;

  if (userGuess === randomNumber) {
    lastResult.textContent = "Congratulations! You got it right!";
    lastResult.style.backgroundColor = "green";
    lowOrHi.textContent = "";
    setGameOver();
  } else if (guessCount === 10) {
    lastResult.textContent = "!!!GAME OVER!!!";
    lowOrHi.textContent = "";
    setGameOver();
  } else {
    lastResult.textContent = "Wrong!";
    lastResult.style.backgroundColor = "red";
    if (userGuess < randomNumber) {
      lowOrHi.textContent = "Last guess was too low!";
    } else if (userGuess > randomNumber) {
      lowOrHi.textContent = "Last guess was too high!";
    }
  }

  guessCount++;
  guessField.value = "";
  guessField.focus();
}
~~~~
真有点多我草
* 第一行当中 声明了一个userGuess变量，将他设置为在文本字段中输入的值。我们还对这个值应用了内置的 Number() 方法，只是为了确保该值是一个数字。由于我们没有更改此变量，因此我们使用 const 声明。
* 接下来，我们遇到我们的第一个条件代码块。条件代码块让你能够根据某个条件的真假来选择性地运行代码。虽然看起来有点像一个函数，但它不是。条件块的最简单形式是从关键字 if 开始，然后是一些括号，然后是一些花括号。括号内包含一个比较。如果比较结果为 true，就会执行花括号内的代码。反之，花括号中的代码就会被跳过，从而执行下面的代码。本文的示例中，比较测试的是 guessCount 变量是否等于 1，即玩家是不是第一次猜数字
	guessCount === 1;
	如果是，我们让 guesses 段落的文本内容等于 Previous guesses:。如果不是就不用了。
* 第 6 行将当前 userGuess 值附加到 guesses 段落的末尾，并加上一个空格，以使每两个猜测值之间有一个空格。

在下一个代码块当中 有这么几个检查：
* 第一个 if(){ } 检查用户的猜测是否等于在代码顶端设置的 randomNumber 值。如果是，则玩家猜对了，游戏胜利，我们将向玩家显示一个漂亮的绿色的祝贺信息，并清除“高了 / 低了”信息框的内容，调用 setGameOver() 方法。
* 紧接着是一个 else if(){ } 结构。它会检查这个回合是否是玩家的最后一个回合。如果是，程序将做与前一个程序块相同的事情，只是这次它显示的是 Game Over 而不是祝贺消息。
* 最后的一个块是 else { }，前两个比较都不返回 true 时（也就是玩家尚未猜对，但是还有机会）才会执行这里的代码。在这个情况下，我们会告诉玩家他们猜错了，并执行另一个条件测试，判断并告诉玩家猜测的数字是高了还是低了。
* 函数最后三行（26 - 28 行）是为下次猜测值提交做准备的。我们把 guessCount 变量的值加 1，以使玩家消耗一次机会（++ 是自增操作符，为自身加 1），然后我们把表单中文本域的值清空，重新聚焦于此，准备下一轮游戏。

### 事件
现在，我们有一个实现比较不错的 checkGuess() 函数了，但它现在什么事情也做不了，因为我们还没有调用它。理想中，我们希望在点击“Submit guess”按钮时调用它，为此，我们需要使用事件。事件就是浏览器中发生的事儿，比如点击按钮、加载页面、播放视频，等等，我们可以通过调用代码来响应事件。侦听事件发生的结构称为事件监听器（Event Listener），响应事件触发而运行的代码块被称为事件处理器（Event Handler）。
在 checkGuess() 函数后添加以下代码：
~~~~js
guessSubmit.addEventListener("click", checkGuess);
~~~~
这里为 guessSubmit 按钮添加了一个事件监听器。addEventListener() 方法包含两个可输入值（称为“参数”（argument）），监听事件的类型（本例中为 click），和当事件发生时我们想要执行的代码（本例中为 checkGuess() 函数）。注意，addEventListener() 中作为参数的函数名不加括号。
现在，保存代码并刷新页面，示例应该能够工作了，但还不够完善。现在唯一的问题是，如果玩家猜对或游戏次数用完，游戏将出错，因为我们尚未定义游戏结束时应运行的 setGameOver() 函数。现在，让我们补全所缺代码，并完善示例功能。

### 补全游戏功能
在代码最后添加一个 setGameOver() 函数，然后我们一起来看看它：
~~~~js
function setGameOver() {
  guessField.disabled = true;
  guessSubmit.disabled = true;
  resetButton = document.createElement("button");
  resetButton.textContent = "Start new game";
  document.body.append(resetButton);
  resetButton.addEventListener("click", resetGame);
}
~~~~
* 前两行通过将 disable 属性设置为 true 来禁用表单文本输入和按钮。这样做是必须的，否则用户就可以在游戏结束后提交更多的猜测，游戏的规则将遭到破坏。
* 接下来的三行创建一个新的 `<button>` 元素，设置它的文本为“Start new game”，并把它添加到当前 HTML 的底部。
* 最后一行在新按钮上设置了一个事件监听器，当它被点击时，一个名为 resetGame() 的函数被将被调用。


现在我们需要定义 resetGame() 这个函数，依然放到代码底部：
~~~~js
function resetGame() {
  guessCount = 1;

  const resetParas = document.querySelectorAll(".resultParas p");
  for (const resetPara of resetParas) {
    resetPara.textContent = "";
  }

  resetButton.parentNode.removeChild(resetButton);

  guessField.disabled = false;
  guessSubmit.disabled = false;
  guessField.value = "";
  guessField.focus();

  lastResult.style.backgroundColor = "white";

  randomNumber = Math.floor(Math.random() * 100) + 1;
}
~~~~
这段较长的代码将游戏中的一切重置为初始状态，然后玩家就可以开始新一轮的游戏了。此段代码：
* guesscount设置为1
* 清除所有信息段落。这里，我们选择 `<div class="resultParas"></div>` 内的所有段落，然后通过循环迭代，将它们的 textContent 设置为 ''（一个空字符串)
* 删除重置按钮。
* 启用表单元素，清空文本域并聚焦于此，准备接受新猜测的数字。
* 删除 lastResult 段落的背景颜色。
* 生成一个新的随机数，这样就可以猜测新的数字了！

for...of 循环为你提供了一种获取数组中的每一个元素的方法，并在元素的基础上运行 JavaScript 代码
例如：
~~~~js
const fruits = ["apples", "bananas", "cherries"];
for (const fruit of fruits) {
  console.log(fruit);
}
~~~~
他就会输出三种水果
那么我们这段代码当中的循环做了什么事情呢
~~~~js
const resetParas = document.querySelectorAll(".resultParas p");
for (const resetPara of resetParas) {
  resetPara.textContent = "";
}
~~~~
`这段代码通过 querySelectorAll() 方法创建了一个包含 <div class="resultParas"> 内所有段落的变量，然后通过循环迭代，删除每个段落的文本内容。`

请注意，即使 resetParas 是一个常量，我们也可以更改其内部属性，例如 textContent。

### 对象
在 let resetButton;（脚本顶端部分）下方添加下面一行内容，然后保存文件：
~~~~
guessField.focus();
~~~~
这一行通过 focus() 方法让光标在页面加载完毕时自动放置于 input 输入框内，这意味着玩家可以马上开始第一次猜测，而无需点击输入框。这只是一个小的改进，却提高了可用性——为使用户能投入游戏提供一个良好的视觉线索。
深入分析一下。JavaScript 中一切都是对象。对象是存储在单个分组中的相关功能的集合。可以创建自己的对象，但这是较高阶的知识，我们今后才会谈及。现在，仅需简要讨论浏览器内置的对象，它们已经能够做许多有用的事情。