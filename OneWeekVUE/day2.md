# 第二天
## 条件渲染
根据条件渲染不同的视图
类似于js当中的条件语句
v-if 指令用于条件性地渲染一块内容。这块内容只会在指令的表达式返回真值时才被渲染。
~~~~vue
<h1 v-if="awesome">Vue is awesome!</h1>
~~~~
你也可以使用 v-else 为 v-if 添加一个“else 区块”。
一个 v-else 元素必须跟在一个 v-if 或者 v-else-if 元素后面，否则它将不会被识别。
v-else-if 提供的是相应于 v-if 的“else if 区块”。它可以连续多次重复使用：
~~~~vue
<div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  Not A/B/C
</div>
~~~~
和 v-else 类似，一个使用 v-else-if 的元素必须紧跟在一个 v-if 或一个 v-else-if 元素后面。

因为 v-if 是一个指令，他必须依附于某个元素。但如果我们想要切换不止一个元素呢？在这种情况下我们可以在一个 `<template>` 元素上使用 v-if，这只是一个不可见的包装器元素，最后渲染的结果并不会包含这个 `<template>` 元素。
另一个可以用来按条件显示一个元素的指令是 v-show。其用法基本一样：
不同之处在于 v-show 会在 DOM 渲染中保留该元素；v-show 仅切换了该元素上名为 display 的 CSS 属性。

v-show 不支持在 `<template>` 元素上使用，也不能和 v-else 搭配使用。

### if和show
v-if 是“真实的”按条件渲染，因为它确保了在切换时，条件区块内的事件监听器和子组件都会被销毁与重建。

v-if 也是惰性的：如果在初次渲染时条件值为 false，则不会做任何事。条件区块只有当条件首次变为 true 时才被渲染。

相比之下，v-show 简单许多，元素无论初始条件如何，始终会被渲染，只有 CSS display 属性会被切换。

总的来说，v-if 有更高的切换开销，而 v-show 有更高的初始渲染开销。因此，如果需要频繁切换，则使用 v-show 较好；如果在运行时绑定条件很少改变，则 v-if 会更合适。

## 列表渲染
### vfor
我们可以使用 v-for 指令基于一个数组来渲染一个列表。v-for 指令的值需要使用 item in items 形式的特殊语法，其中 items 是源数据的数组，而 item 是迭代项的别名：
~~~~js
const items = ref([{ message: 'Foo' }, { message: 'Bar' }])
~~~~
~~~~vue
<li v-for="item in items">
  {{ item.message }}
</li>
~~~~
v-for 也支持使用可选的第二个参数表示当前项的位置索引。
~~~~js
const parentMessage = ref('Parent')
const items = ref([{ message: 'Foo' }, { message: 'Bar' }])
~~~~
index可以理解为数组下标
~~~~vue
<li v-for="(item, index) in items">
  {{ parentMessage }} - {{ index }} - {{ item.message }}
</li>
~~~~
输出如下：
Parent - 0 - Foo
Parent - 1 - Bar
### vfor与对象
你也可以使用 v-for 来遍历一个对象的所有属性。遍历的顺序会基于对该对象调用 Object.values() 的返回值来决定。
~~~~vue
<template>
  <div style="text-align: center;">
    <h1>wpcap</h1>
      <p v-for="name in names" :key="name">{{ name }}</p>
    <div v-for="user in userinfo">{{user}}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      names: ["wocaonide", "wocaotade"],
      userinfo:{
        name:"wocaonima",
        age:"20",
        sex:"male"
      }
    };
  }
};
</script>
~~~~

### 通过key管理状态
Vue 默认按照“就地更新”的策略来更新通过 v-for 渲染的元素列表。当数据项的顺序改变时，Vue 不会随之移动 DOM 元素的顺序，而是就地更新每个元素，确保它们在原本指定的索引位置上渲染。

默认模式是高效的，但只适用于列表渲染输出的结果不依赖子组件状态或者临时 DOM 状态 (例如表单输入值) 的情况。

为了给 Vue 一个提示，以便它可以跟踪每个节点的标识，从而重用和重新排序现有的元素，你需要为每个元素对应的块提供一个唯一的 key attribute：
~~~~vue
<div v-for="item in items" :key="item.id">
  <!-- 内容 -->
</div>
~~~~
推荐在任何可行的时候为 v-for 提供一个 key attribute，除非所迭代的 DOM 内容非常简单 (例如：不包含组件或有状态的 DOM 元素)，或者你想有意采用默认行为来提高性能。

key 绑定的值期望是一个基础类型的值，例如字符串或 number 类型。不要用对象作为 v-for 的 key。

**往往可以用json的id来作为key**

## 事件处理
### 监听事件
我们可以使用 v-on 指令 (简写为 @) 来监听 DOM 事件，并在事件触发时执行对应的 JavaScript。用法：v-on:click="handler" 或 @click="handler"。
事件处理器 (handler) 的值可以是：

* 内联事件处理器：事件被触发时执行的内联 JavaScript 语句 (与 onclick 类似)。
内联事件处理器通常用于简单场景，例如：
~~~~vue
  <div style="text-align: center;">
    <button @click="count++">Add 1</button>
    <p>Count is: {{ count }}</p>
  </div>
~~~~
* 方法事件处理器：一个指向组件上定义的方法的属性名或是路径。
随着事件处理器的逻辑变得愈发复杂，内联代码方式变得不够灵活。因此 v-on 也可以接受一个方法名或对某个方法的调用。

~~~~js
data() {
  return {
    name: 'Vue.js'
  }
},
methods: {
  greet(event) {
    // 方法中的 `this` 指向当前活跃的组件实例
    alert(`Hello ${this.name}!`)
    // `event` 是 DOM 原生事件
    if (event) {
      alert(event.target.tagName)
    }
  }
}
~~~~
方法事件处理器会自动接收原生 DOM 事件并触发执行。在上面的例子中，我们能够通过被触发事件的 event.target 访问到该 DOM 元素----button

也可以在内联处理器当中调用方法
这允许我们向方法传入自定义参数以代替原生事件：
~~~~js
methods: {
  say(message) {
    alert(message)
  }
}
~~~~
~~~~vue
<button @click="say('hello')">Say hello</button>
<button @click="say('bye')">Say bye</button>
~~~~
### 事件修饰符
在处理事件时调用 event.preventDefault() 或 event.stopPropagation() 是很常见的。尽管我们可以直接在方法内调用，但如果方法能更专注于数据逻辑而不用去处理 DOM 事件的细节会更好。

为解决这一问题，Vue 为 v-on 提供了事件修饰符。修饰符是用 . 表示的指令后缀，包含以下这些：
.stop
.prevent
.self
.capture
.once
.passive
~~~~vue
<!-- 单击事件将停止传递 -->
<a @click.stop="doThis"></a>

<!-- 提交事件将不再重新加载页面 -->
<form @submit.prevent="onSubmit"></form>

<!-- 修饰语可以使用链式书写 -->
<a @click.stop.prevent="doThat"></a>

<!-- 也可以只有修饰符 -->
<form @submit.prevent></form>

<!-- 仅当 event.target 是元素本身时才会触发事件处理器 -->
<!-- 例如：事件处理器不来自子元素 -->
<div @click.self="doThat">...</div>
~~~~
**.capture、.once 和 .passive 修饰符与原生 addEventListener 事件相对应：**

## 表单输入绑定
在前端处理表单时，我们常常需要将表单输入框的内容同步给 JavaScript 中相应的变量。手动连接值绑定和更改事件监听器可能会很麻烦：
~~~~vue
<input
  :value="text"
  @input="event => text = event.target.value">
~~~~
看着都恶心
v-model 指令帮我们简化了这一步骤：
~~~~vue
<input v-model="text">
~~~~
比如说这样：
~~~~vue
<p>Message is: {{ message }}</p>
<input v-model="message" placeholder="edit me" />
~~~~
或者这样
~~~~vue
<span>Multiline message is:</span>
<p style="white-space: pre-line;">{{ message }}</p>
<textarea v-model="message" placeholder="add multiple lines"></textarea>
~~~~
单行文本和多行文本

注意在 textarea 中是不支持插值表达式的。请使用 v-model 来替代：
~~~~vue
<!-- 错误 -->
<textarea>{{ text }}</textarea>

<!-- 正确 -->
<textarea v-model="text"></textarea>
~~~~

### 复选框
~~~~vue
<input type="checkbox" id="checkbox" v-model="checked" />
<label for="checkbox">{{ checked }}</label>
~~~~
意思是先有某种输入 比如我们规定为v-model="checked"

然后在这个lable 属性为checkbox的元素当中

checked这个元素就出现了

我们也可以将多个复选框绑定到同一个数组或[集合](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set)的值：

~~~~vue
export default {
  data() {
    return {
      checkedNames: []
    }
  }
}
~~~~

~~~~vue
<div>Checked names: {{ checkedNames }}</div>

<input type="checkbox" id="jack" value="Jack" v-model="checkedNames" />
<label for="jack">Jack</label>

<input type="checkbox" id="john" value="John" v-model="checkedNames" />
<label for="john">John</label>

<input type="checkbox" id="mike" value="Mike" v-model="checkedNames" />
<label for="mike">Mike</label>
~~~~

在这个例子中，`checkedNames` 数组将始终包含所有当前被选中的框的值。

### 单选按钮

~~~~vue
<div>Picked: {{ picked }}</div>

<input type="radio" id="one" value="One" v-model="picked" />
<label for="one">One</label>

<input type="radio" id="two" value="Two" v-model="picked" />
<label for="two">Two</label>
~~~~

### 选择器

单选

~~~~vue
<div>Selected: {{ selected }}</div>

<select v-model="selected">
  <option disabled value="">Please select one</option>
  <option>A</option>
  <option>B</option>
  <option>C</option>
</select>
~~~~

多选

~~~~vue
<div>Selected: {{ selected }}</div>

<select v-model="selected" multiple>
  <option>A</option>
  <option>B</option>
  <option>C</option>
</select>
~~~~

选择器的选项可以使用 `v-for` 动态渲染：

~~~~vue
export default {
  data() {
    return {
      selected: 'A',
      options: [
        { text: 'One', value: 'A' },
        { text: 'Two', value: 'B' },
        { text: 'Three', value: 'C' }
      ]
    }
  }
}
<select v-model="selected">
  <option v-for="option in options" :value="option.value">
    {{ option.text }}
  </option>
</select>

<div>Selected: {{ selected }}</div>
~~~~

### 

