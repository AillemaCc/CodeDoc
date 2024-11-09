# 第三天

## 生命周期钩子

每个 Vue 组件实例在创建时都需要经历一系列的初始化步骤，比如设置好数据侦听，编译模板，挂载实例到 DOM，以及在数据改变时更新 DOM。在此过程中，它也会运行被称为生命周期钩子的函数，让开发者有机会在特定阶段运行自己的代码。

### 注册周期钩子

这段竟然他妈的不重要

## 侦听器

### 基本示例

计算属性允许我们声明性地计算衍生值。然而在有些情况下，我们需要在状态变化时执行一些“副作用”：例如更改 DOM，或是根据异步操作的结果去修改另一处的状态。

在选项式 API 中，我们可以使用 [`watch` 选项](https://cn.vuejs.org/api/options-state.html#watch)在每次响应式属性发生变化时触发一个函数。

~~~~js
export default {
  data() {
    return {
      question: '',
      answer: 'Questions usually contain a question mark. ;-)',
      loading: false
    }
  },
  watch: {
    // 每当 question 改变时，这个函数就会执行
    question(newQuestion, oldQuestion) {
      if (newQuestion.includes('?')) {
        this.getAnswer()
      }
    }
  },
  methods: {
    async getAnswer() {
      this.loading = true
      this.answer = 'Thinking...'
      try {
        const res = await fetch('https://yesno.wtf/api')
        this.answer = (await res.json()).answer
      } catch (error) {
        this.answer = 'Error! Could not reach the API. ' + error
      } finally {
        this.loading = false
      }
    }
  }
}
~~~~

上面这段代码，就能实现在：

`question` 数据属性中输入包含问号（?）的问题时，组件会调用 `getAnswer` 方法来获取一个答案。`getAnswer` 方法通过向 `https://yesno.wtf/api` 发送请求来异步获取答案，并将响应中的答案更新到 `answer` 数据属性中。

这他妈怎么一步上天了

或者说**侦听器是来监测、侦听页面当中具有响应式的数据变化的工具**

这是一个比较容易理解的例子：

~~~~vue
<template>
  <div style="text-align: center;">
  <h3>监听器</h3>
    <p>{{msg}}</p>
    <button @click="updatedata">修改数据</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      msg:"fuck"
    }
  },
  methods:{
    updatedata(){
      this.msg="fucku"
    }
  },
  watch:{
    msg(newValue,oldValue){
      //数据发生变化的时候，自动执行的函数；函数名必须与侦听的数据对象的名字保持一致
      console.log(newValue,oldValue)
    }
  }
}
</script>
~~~~



上面的就是watch的作用







