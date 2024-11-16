# 第七天

## 依赖注入

### props逐级透传问题

通常情况下，当我们需要从父组件向子组件传递数据时，会使用 [props](https://cn.vuejs.org/guide/components/props.html)。想象一下这样的结构：有一些多层级嵌套的组件，形成了一棵巨大的组件树，而某个深层的子组件需要一个较远的祖先组件中的部分数据。在这种情况下，如果仅使用 props 则必须将其沿着组件链逐级传递下去，这会非常麻烦

比如一个root组件，向footer组件传递数据，footer组件再通过props向更深层的组件传递，这只是一个比较短的例子，之后肯定还会有更长的

`provide` 和 `inject` 可以帮助我们解决这一问题。一个父组件相对于其所有的后代组件，会作为**依赖提供者**。任何后代的组件树，无论层级有多深，都可以**注入**由父组件提供给整条链路的依赖。

### provide 提供

要为组件后代提供数据，需要使用到 [`provide`](https://cn.vuejs.org/api/options-composition.html#provide) 选项：

~~~~vue
export default {
  provide: {
    message: 'hello!'
  }
}
~~~~

对于 `provide` 对象上的每一个属性，后代组件会用其 key 为注入名查找期望注入的值，属性的值就是要提供的数据。

如果我们需要提供依赖当前组件实例的状态 (比如那些由 `data()` 定义的数据属性)，那么可以以函数形式使用 `provide`：

~~~~js
export default {
  data() {
    return {
      message: 'hello!'
    }
  },
  provide() {
    // 使用函数的形式，可以访问到 `this`
    return {
      message: this.message
    }
  }
}
~~~~

但是这样的操作不会使得注入保持响应性，我们会在后面的内容中（假如我真的写的话）讨论怎么让这种注入变成响应式

### 在应用层当中provide

两三句话 不多写了



### inject 注入

要注入上层组件当中提供的数据，需要使用inject选项来声明

~~~~js
export default{
    inject:['message'],
    created(){
        console.log(this.message)
    }
}
~~~~

这样声明之后，注入会在组件自身的状态之前被解析，因此就可以在data当中访问到注入的属性。

### 注入别名

当我们以数组形式使用inject，就像上面那样的时候，注入的属性会以同名的key暴露到组件实例上。

在上面的例子中，提供的属性名为 `"message"`，注入后以 `this.message` 的形式暴露。访问的本地属性名和注入名是相同的。

如果我们想要用一个不同的本地属性名注入该属性，我们需要在 `inject` 选项的属性上使用对象的形式：

~~~~js
export default{
    inject:{
        localMessage{
        from:"message"
    }
    }
}
~~~~

通过from声明注入来源的名称。这里，组件本地化了原注入名 `"message"` 所提供的属性，并将其暴露为 `this.localMessage`

### 注入默认值

默认情况下，`inject` 假设传入的注入名会被某个祖先链上的组件提供。如果该注入名的确没有任何组件提供，则会抛出一个运行时警告。

如果在注入一个值时不要求必须有提供者，那么我们应该声明一个默认值，和 props 类似：

~~~~js
export default {
  // 当声明注入的默认值时
  // 必须使用对象形式
  inject: {
    message: {
      from: 'message', // 当与原注入名同名时，这个属性是可选的
      default: 'default value'
    },
    user: {
      // 对于非基础类型数据，如果创建开销比较大，或是需要确保每个组件实例
      // 需要独立数据的，请使用工厂函数
      default: () => ({ name: 'John' })
    }
  }
}
~~~~

### 使用symbol作为注入名

至此，我们已经了解了如何使用字符串作为注入名。但如果你正在构建大型的应用，包含非常多的依赖提供，或者你正在编写提供给其他开发者使用的组件库，建议最好使用 Symbol 来作为注入名以避免潜在的冲突。

我们通常推荐在一个单独的文件中导出这些注入名 Symbol：

~~~~js
//key.js
export const myInjectionKey=Symbol()
~~~~

~~~~js

// 在供给方组件中
import { myInjectionKey } from './keys.js'

export default {
  provide() {
    return {
      [myInjectionKey]: {
        /* 要提供的数据 */
      }
    }
  }
}
~~~~

~~~~js

// 注入方组件
import { myInjectionKey } from './keys.js'

export default {
  inject: {
    injected: { from: myInjectionKey }
  }
}
~~~~

## 异步组件

### 基本用法

在大型项目当中，我们可能需要拆分应用为更小的块，并且我们可能会在需要的时候，才从服务器加载相关组件。这样的传输，vue提供了[`defineAsyncComponent`](https://cn.vuejs.org/api/general.html#defineasynccomponent) 方法来实现此功能：

~~~~js
import { defineAsyncComponent } from 'vue'

const AsyncComp = defineAsyncComponent(() => {
  return new Promise((resolve, reject) => {
    // ...从服务器获取组件
    resolve(/* 获取到的组件 */)
  })
})
// ... 像使用其他一般组件一样使用 `AsyncComp`
~~~~

这一部分剩下的内容我建议直接去原文阅读

[原文链接](https://cn.vuejs.org/guide/components/async.html)

## 组件生命周期

每个vue组件实例在创建时期，都需要经过一定的初始化步骤。比如设置好数据侦听，编译模板，挂载实例到dom，以及在数据改变的时候更新dom。在此过程当中，他也会运行被称为生命周期钩子的函数。让开发者有机会在特定阶段运行自己的代码

**从创建的那一刻开始，到卸载的那一刻结束**

* 创建期
* 挂载期
* 更新期
* 销毁期

每个生命周期都有一个对应的before函数和本名的函数，一共八个生命周期函数

before create--组件即将创建

create--组件创建

before mount--挂载之前

mounted--挂载

......

八个函数运行下来

就是一个生命周期函数

每个生命周期函数都是自动执行的

懂概念就可以



## 结束

这是最后的一部分了。没了

