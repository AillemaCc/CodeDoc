# 第五天

## 组件事件

在组件的模版表达式当中，可以直接使用$emit方法触发自定义事件

props可以父亲传子代

而$emit就可以子代传父亲

首先我们展示一个例子，这个例子当中有两个组件，分别是子组件和父组件。我们在子组件当中，设置一个按钮，点击它，能够使用$emit，触发一个自定义事件clickEvent。这个事件名称在父组件当中，可以通过<ComponentsB @clickEvent="getHandle" />被触发。在触发这个由下至上的事件是，父组件当中，我们定义的getHandle方法也被触发了。我们可以让他输出一个声明，告诉我们结果

~~~~vue
<script>
import ComponentsB from './ComponentsB.vue'
export default {
  components: {
    ComponentsB
  },
  methods:{
    getHandle(){
      alert("触发父级事件")
    }
  }

}
</script>

<template>
<h3>组件事件</h3>
  <ComponentsB @clickEvent="getHandle" />
</template>

<style scoped>

</style>
~~~~



~~~~vue
<script>
export default {
  methods:{
    clickEventHandle(){
      //自定义事件
        this.$emit('clickEvent')
    }
  }
}
</script>

<template>
<h3>子事件</h3>
  <button @click="clickEventHandle">点击按钮</button>
  </template>

<style scoped>

</style>
~~~~

这样，点击页面当中的按钮，就能实现功能

------

emit的第二个参数可以是一个数据，比如一个字符串

在父组件当中，被子组件触发的方法就可以传入一个参数

所以，组件之间传递数据有两个方案：

* 父传子：props

* 子传父：自定义事件

  

## 组件事件配合vmodel使用

双向绑定，同时显示

![流程图](http://photos.swindle.icu/picture/typora%E5%9B%BE%E7%89%87%E5%AD%98%E5%82%A8/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202024-11-12%20165530.png)

~~~~vue
<script>
export default {
  data(){
    return{
      search:""
    }
  },
  watch:{
    search(newvalue,oldvalue){
      this.$emit("putsearch",newvalue)
    }
  }
}
</script>

<template>
搜索：<input type="text" v-model="search" />

</template>

<style scoped>

</style>
~~~~

~~~~vue
<script>

import ComponentsB from "@/components/ComponentsB.vue";
export default {
  components: {
    ComponentsB
  },
  data(){
    return{
      search:""
    }
  },
  methods:{
    getsearch(data){
      this.search = data;
    }
  }
}
</script>

<template>
<h3>主页面</h3>
  <ComponentsB @putsearch="getsearch"/>
  <p>{{search}}</p>
</template>

<style scoped>

</style>
~~~~

除了上述的方案 props也可以实现子传父

但是需要一点额外的方式

通过函数的加入，能够实现子传父

父亲先传一个函数给孩子，孩子再使用这个函数给父亲传递数据。父亲就能从孩子那里接收到数据。而且无需触发。

~~~~vue
<script>
import ComponentsB from './ComponentsB.vue'
export default {
  data(){
    return{
      msg:""
    }
  },
  components:{
    ComponentsB
  },
  methods:{
    dataFn(data){
      console.log(data)
    }
  }
}
</script>

<template>
  <h3>A</h3>
  <ComponentsB :onEvent="dataFn"/>
</template>

<style scoped>

</style>
~~~~



~~~~vue
<script>
export default {
  data(){
    return{

    }
  },
  props:{
    onEvent:Function,


  }
}
</script>

<template>
<h3>B</h3>
  <p>{{onEvent("传递了子组件的数据进入到父组件当中")}}</p>
</template>

<style scoped>

</style>
~~~~

## 透传属性

使用率太低了

瞎他妈看看得了

## 插槽slots

组件怎么接受模版内容呢？

在某些场景当中，我们可能想要给子组件传递一些模版片段，让子组件在他们的组件中渲染这些片段

