<template>
  <div>
    <h1>UserName:{{UserName}}</h1>
    <button @click="getUserName">自定义事件</button>
  </div>
</template>

<script>
export default {
  name:'Login',
  data(){
    return {
      UserName:'Ecioboy'
    }
  },
  methods:{
    getUserName(){
      // $emit绑定自定义事件，传参给UserName
      this.$emit('LoginName',this.UserName)
    }
  }
}
</script>

<style>

</style>
