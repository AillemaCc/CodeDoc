# 第四天

## 组件

组件最大的优势就是能够复用

~~~~vue
<script>
export default {
  
}
</script>

<template>
<div>承载标签</div>
</template>

<style>

</style>
~~~~

上面就是一个什么都没有的组件

~~~~vue
<script>
export default {

}
</script>

<template>
<div style="text-align: center">
  <p class="container">组件基础组成</p>
</div>
</template>

<style>
.container {
  text-align: center;
  font-size: 30px;
  color: red;
}
</style>
~~~~

随便写点什么

在app.vue当中这样声明

~~~~vue
<script>
//第一步：引入组件
import fuck from "./components/fuck.vue"
//第二步：注入组件
export default {
  components:{
    fuck
  }
}
</script>

<template>
  <!--第三步：显示组件-->
  <fuck />
</template>
~~~~

对于一个组件来说，必须存在模版代码

剩下的style和script都无所谓了

可以都随便选

### scoped属性

他就干一件事：让当前样式只在当前组件当中生效

如果不加scoped，这个组件就会变成全局组件，在所有页面当中都生效

所以最好都添加上scoped，让代码更加规范

### 组件嵌套关系

组件允许我们将ui划分为独立的，可用的部分，并且可以对每个部分进行单独的思考

在实际应用当中，组件常常被组织成层层嵌套的树状结构

至于具体嵌套能实现到什么方式

这个视频给了一个从无到有的一个非常简单的示例

[链接](https://www.bilibili.com/video/BV1Rs4y127j8?spm_id_from=333.788.videopod.episodes&vd_source=6f5674ac2382927bd50461ce4c6ce2ed&p=22)

### 组件注册方式

一个vue使用之前就需要先被注册

注册组件有两种方式

全局注册和局部注册

在我们之前做的，都是局部注册。

而全局注册，在最外层注册一次，在所有组件当中都可以引用

全局注册在main.js当中操作，在main当中注册之后，就不需要局部注册

~~~~js


import { createApp } from 'vue'
import App from './APP.vue'
const app = createApp(App)
//只能在这中间写组件的注册语句
createApp(App).mount('#app')

~~~~

比如我们想全局引用一个header

~~~~js


import { createApp } from 'vue'
import App from './APP.vue'
import Header from "@/pages/header.vue";
const app = createApp(App)
//只能在这中间写组件的注册语句
app.component('Header', Header)
createApp(App).mount('#app')

~~~~



这样，就可以全局注册header组件

但是在真正的应用场景当中

还是**推荐选择局部注册**

因为全局注册有这么两个问题

1. 全局注册，但并没有被使用的组件无法在生产打包时被自动移除 (也叫“tree-shaking”)。如果你全局注册了一个组件，即使它并没有被实际使用，它仍然会出现在打包后的 JS 文件中。
2. 全局注册在大型项目中使项目的依赖关系变得不那么明确。在父组件中使用子组件时，不太容易定位子组件的实现。和使用过多的全局变量一样，这可能会影响应用长期的可维护性。

相比之下，局部注册的组件需要在使用它的父组件中显式导入，并且只能在该父组件中使用。它的优点是使组件之间的依赖关系更加明确，并且对 tree-shaking 更加友好。

局部注册的模板就像这样：

~~~~vue
<script>
import ComponentA from './ComponentA.vue'

export default {
  components: {
    ComponentA
  }
}
</script>

<template>
  <ComponentA />
</template>
~~~~

### 组件传递数据

组件和组件之间，并不是完全独立的，是存在数据之间的传递的

比如我们现在有父子两个组件：

在父组件当中：

~~~~vue
<script>
import Children from "./child.vue";
export default {
  data(){
    return{

    }
  },
  components: {
    Children
  }
}
</script>

<template>
<h3>PARENT</h3>
  <Children title="fuckyou" />
</template>

<style scoped>

</style>
~~~~

我们注册了children组件，同时直接在children当中传入一个title

而在children组件当中

~~~~vue
<script>
export default {
  data(){
    return{

    }
  },
  props:["title"]
}
</script>

<template>
  <h3>children</h3>
  <p>{{ title }}</p>
</template>

<style scoped>

</style>
~~~~

我们通过props接收title参数（以字符串形式）

同时在前端展示出来

**父传子 props**

### 动态传递数据

我们可以在父亲组件当中，声明一个msg:"fucku"，用这个`<Children :title="msg" />`进行传递

因为这个没有写死在html当中

~~~~vue
<!-- 根据一个变量的值动态传入 -->
<BlogPost :title="post.title" />

<!-- 根据一个更复杂表达式的值动态传入 -->
<BlogPost :title="post.title + ' by ' + post.author.name" />
~~~~





**注意**

props传递数据，只能从父级传递到子级，不能反其道而行

### 组件传递多种数据类型

还可以传递数字类型。。。。

反正任何东西都能作为props的值被传递

~~~~vue
<script>
import Children from "./child.vue";
export default {
  data(){
    return{
      msg:"fucku",
      age:20
    }
  },
  components: {
    Children
  }
}
</script>

<template>
<h3>PARENT</h3>
  <Children :title="msg" :age="age" />
</template>

<style scoped>

</style>
~~~~

像这样就又传递了一个age 数字类型

### 组件传递校验

vue组件可以更细致的声明对传入的props的要求

比如我们上面已经看到过的类型声明，如果传入的值不满足类型要求，Vue 会在浏览器控制台中抛出警告来提醒使用者。这在开发给其他开发者使用的组件时非常有用。

要声明对 props 的校验，你可以向 `props` 选项提供一个带有 props 校验选项的对象，例如：

~~~~js
export default {
  props: {
    // 基础类型检查
    //（给出 `null` 和 `undefined` 值则会跳过任何类型检查）
    propA: Number,
    // 多种可能的类型
    propB: [String, Number],
    // 必传，且为 String 类型
    propC: {
      type: String,
      required: true
    },
    // 必传但可为 null 的字符串
    propD: {
      type: [String, null],
      required: true
    },
    // Number 类型的默认值
    propE: {
      type: Number,
      default: 100
    },
    // 对象类型的默认值
    propF: {
      type: Object,
      // 对象或者数组应当用工厂函数返回。
      // 工厂函数会收到组件所接收的原始 props
      // 作为参数
      default(rawProps) {
        return { message: 'hello' }
      }
    },
    // 自定义类型校验函数
    // 在 3.4+ 中完整的 props 作为第二个参数传入
    propG: {
      validator(value, props) {
        // The value must match one of these strings
        return ['success', 'warning', 'danger'].includes(value)
      }
    },
    // 函数类型的默认值
    propH: {
      type: Function,
      // 不像对象或数组的默认，这不是一个
      // 工厂函数。这会是一个用来作为默认值的函数
      default() {
        return 'Default function'
      }
    }
  }
}
~~~~

