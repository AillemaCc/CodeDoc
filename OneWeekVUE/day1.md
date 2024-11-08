# 一周vue第一天
怎么在idea当中创建一个vue工程呢
都集成环境了还说啥呢
正常安装一个nodejs
正常安装一个vuecli
记得nodejs在16版本以上就行了
**剩下的回来再写**
## 项目结构
* .vscode：没什么关系 他默认的推荐工具就是VScode
* .node_modules：vue项目依赖
* public：资源文件夹 比如浏览器图标等等
* src：源码文件夹
* gitignore：团队合作用的
* index.html：html入口文件
* package.json：项目描述文件
* readme：读我
* config：配置文件
目前需要关心的 就是src
## 模版语法
vue使用一种基于html的模版语法
使我们能够声明式地将其组件实例的数据 绑定到呈现的DOM上
所有的vue模版都是语法层面合法的html
可以被符合规范的浏览器和html解析器解析
### 文本插值
最基本的数据绑定形式是文本插值
它使用的是“Mustache”语法 (即双大括号)：
~~~~vue
<span>Message: {{ msg }}</span>
~~~~
双大括号标签会被替换为相应组件实例中 msg 属性的值。同时每次 msg 属性更改时它也会同步更新。
***
你也可以插入js表达式
~~~~vue
<script>
export default {
  data(){
    return{
      msg:"我操你妈",
      hello:"fuck",
      number:10,
    }
  }
}
</script>

<template>
  <h1>模版语法</h1>
  <p>{{msg}}</p>
  <p>{{hello}}</p>
  <p>{{number+1}}</p>
</template>
~~~~
就像这样
或者其他表达式
而且注意每个绑定仅支持单一表达式，也就是一段能够被求值的 JavaScript 代码。一个简单的判断方法是是否可以合法地写在 return 后面。

因此，下面的例子都是无效的：
~~~~
<!-- 这是一个语句，而非表达式 -->
{{ var a = 1 }}

<!-- 条件控制也不支持，请使用三元表达式 -->
{{ if (ok) { return message } }}
~~~~
### 原始html
双大括号会将数据解释为纯文本，而不是 HTML。若想插入 HTML，你需要使用 v-html 指令：
~~~~vue
<template>
  <div>
    <h1>模版语法</h1>
    <p>{{link}}</p>
  </div>

</template>


<script>
export default {
  data(){
    return{
      link:"<a href='www.baidu.com'>wocaonide</a>"
    }
  }
}
</script>
~~~~
会直接渲染出
~~~~
<a href='www.baidu.com'>wocaonide</a>
~~~~
没能识别a标签
那我们就需要v-html标签来让vue识别并且渲染这个原始html
~~~~vue
<p v-html="link"></p>
~~~~
### 属性绑定
什么是属性绑定呢
我们举一个例子
~~~~vue
<script>
export default {
  data(){
    return{
      msg:"active"
    }
  }
}
</script>

<template>
<p class="{{msg}}">test</p>
</template>
~~~~
对于这样一段vue代码来说，我们希望展示到界面上的测试文本 它的类型是active
那实际上是什么呢？
实际上他的属性变成了{{msg}}

在文档当中，有这样的描述

*双大括号不能在 HTML attributes 中使用。想要响应式地绑定一个 attribute，应该使用 v-bind 指令*
~~~~vue
<div v-bind:id="dynamicId"></div>
~~~~
v-bind 指令指示 Vue 将元素的 id attribute 与组件的 dynamicId 属性保持一致。如果绑定的值是 null 或者 undefined，那么该 attribute 将会从渲染的元素上移除。
让我们来试一下
~~~~vue
<script>
export default {
  data(){
    return{
      msg:"active"
    }
  }
}
</script>

<template>
  <p v-bind:class="msg">test</p>
</template>
~~~~
这样，test的属性就变成了active
文本的值的绑定用双括号
属性的值的绑定就用vbind

### 布尔型 Attribute 
布尔型 attribute 依据 true / false 值来决定 attribute 是否应该存在于该元素上。disabled 就是最常见的例子之一。
比如这样设置一个元素：
~~~~vue
<button :disabled="isButtonDisabled">Button</button>
~~~~
当isButtonDisabled 为真值或一个空字符串 `(即 <button disabled="">)` 时，元素会包含这个 disabled attribute。而当其为其他假值时 attribute 将被忽略。
### 动态绑定多个值
假如你有这样一套玩意：
~~~~js
const objectOfAttrs = {
  id: 'container',
  class: 'wrapper',
  style: 'background-color:green'
}
~~~~
你可以直接通过不带参数的 v-bind，将它们绑定到单个元素上：
~~~~vue
<script>
export default {
  data(){
    return{
      msg:"active",
      objectOfAttrs:{
        id: 'container',
        class: 'wrapper',
        style: 'background-color:green'
      }
    }

  }
}
</script>

<template>
  <div v-bind="objectOfAttrs">fuck</div>
</template>
~~~~
