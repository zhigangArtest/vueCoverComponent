<template>
  <div id="app">
    <button class="alert" @click="showPop">点击弹出</button>
    <Pop v-if="show" :father="[this,'show']" @myway="handle">
      确认要取消吗？
      <!-- <form action="">
        用户名：<input type="text" >
        密码：<input type="text">
      </form> -->
    </Pop>
  </div>
</template>

<script>
import Pop from './components/Pop'

export default {
  name: 'App',
  data(){
    return {
      show: false
    }
  },
  methods:{
    showPop(){
      this.show = true;
    },
    handle(){
      console.log('返回true')
    }
  },
  components: {
    Pop
  }
}
</script>

<style>
.alert{
  display: block;
   margin : 200px auto;
}

</style>
