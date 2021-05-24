<template>
  <div class="test">
    <h1>{{descriptionMsg}}</h1>
    <span>有个人的名字是{{name}}，今年{{age}}岁</span>
    <button @click="plusOne">再过了一年</button>
  </div>
  <div class="objectTest">
    有一本书的名字是{{book.name}},总共有{{book.page}}页
  </div>
  <div class="computeTest">
    <input type="text" v-model="inputMsg"/>
    <input type="text" v-model="reversedMessage"/>
  </div>
</template>


<script lang="ts">
// import { Options, Vue } from 'vue-class-component';
import { defineComponent, reactive,ref,computed } from 'vue'


/**
 * 定义一个结构体
 */
interface Book {
  name: string
  page: number
}



export default defineComponent({
  name: 'TestPage',
    //用于初始化属性值
    data() {
    return {
      descriptionMsg: "测试页，用于测试语法学习"
    };
  },

  //1、由于在执行 setup函数的时候，还没有执行 Created 生命周期方法，所以在 setup 函数中，无法使用 data 和 methods 的变量和方法
  //2、由于我们不能在 setup函数中使用 data 和 methods，所以 Vue 为了避免我们错误的使用，直接将 setup函数中的this修改成了 undefined
  //3、setup函数只能是同步的不能是异步的
  // 参考：https://blog.csdn.net/qq_41328247/article/details/109286022
 setup(){
    const name =ref('小李')    //名字
    const age=ref(18)    //年纪
    const inputMsg=ref("默认内容")    //默认内容

    // 方法
    function plusOne(){
      age.value++ //想改变值或获取值 必须.value
    }

   //初始化Book的各属性值
    const book:Book= reactive({ name: '小鸭子', page: 16 })
   
   //computed的使用，动态计算属性值
   const reversedMessage = computed(() => {
      return inputMsg.value.split('');
    })

    //必须返回 模板中才能使用
    return {
      name,age,plusOne,book,inputMsg,reversedMessage
    }
  }

})
</script>

