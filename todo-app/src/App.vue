<template>
  <div id="root">
  <!-- 接收LoginName参数传给getName -->
   <!-- <Login @LoginName="getName"/> -->
    <div class="container">
      <br/><br/>
      <transition 
        appear
        name="animate__animated animate__bounce" 
        enter-active-class="animate__rotateInDownLeft"
      >
        <h1 class="Hl" onselectstart='return false'>Hello Todo!</h1>
      </transition>
      <!--<p>插播一个小广告：Telegram公益机场推荐频道：http://t.me/PublicGoodVPN</p> --> 
      <br/><br/>
      <!-- Add Todo -->
      <AddTodo @AppAddTodo="AppAddTodo" :DefaultTodo="DefaultTodo"/>
      <br/><br/>
      <ListTodo 
        :DefaultTodo="DefaultTodo"
      />
      <FooterTodo 
        :DefaultTodo="DefaultTodo"
        @checkAllTodo="checkAllTodo"
        @clearAllTodo="clearAllTodo"
      />
    </div>
  </div>
</template>


<script>
import 'animate.css'

// import Login from './components/Login/Login'

import AddTodo from './components/Todo/AddTodo'
import ListTodo from './components/Todo/ListTodo'
import FooterTodo from './components/Todo/FooterTodo'

export default {
  name: 'App',
  components:{
    AddTodo,
    ListTodo,
    FooterTodo,
    // Login
  },
  data(){
    return {
      /*
      DefaultTodo: [
        {id:'001',name:'Eat',done:false},
        {id:'002',name:'Sleep',done:false},
        {id:'003',name:'Play',done:false},
        {id:'004',name:'Fuck',done:false},
      ]
      */
      DefaultTodo: JSON.parse(localStorage.getItem('DefaultTodo')) || []
    }
  },
  methods:{
    // 自定义事件,将LoginName传给getName
    /*
    getName(name){
      console.log(name)
    },
    */
    // AddTodo组件
    // 添加Todo
    AppAddTodo(event){
      this.DefaultTodo.unshift(event);
    },
    // ItemTodo组件
    // 勾选Todo
    checkTodo(id){
      // todo参数为遍历出来的元素体
      this.DefaultTodo.forEach((todo)=>{
        if(todo.id === id){
          return todo.done = !todo.done;
        }
      })
    },

    // 更新Todo
    updateTodo(id,name){
      this.DefaultTodo.forEach((todo)=>{
        if(todo.id === id){
          return todo.name = name
        }
      })
    },

    // 删除Todo
    deleteTodo(id){
      // todo参数为过滤出来的元素体
      this.DefaultTodo = this.DefaultTodo.filter((todo)=>{
        return todo.id !== id
      })
    },
    // FooterTodo组件
    // 全选Todo
    checkAllTodo(done){
      // todo参数为遍历出来的元素体
      this.DefaultTodo.forEach((todo)=>{
        todo.done = done
      })
    },

    // 删除已选Todo
    clearAllTodo(){
      this.DefaultTodo = this.DefaultTodo.filter((todo)=>{
        return !todo.done
      })
    }
  },
  // 本地存储
  watch:{
    DefaultTodo:{
      deep:true,
      handler(value){
        localStorage.setItem('DefaultTodo',JSON.stringify(value))
      }
    }
    /*
    DefaultTodo(value){
      localStorage.setItem('DefaultTodo',JSON.stringify(value))
    },
    */
  },
  mounted(){
    this.$bus.$on('checkTodo',this.checkTodo)
    this.$bus.$on('deleteTodo',this.deleteTodo)
    this.$bus.$on('updateTodo',this.updateTodo)
  },
  beforeDestroy(){
    this.$bus.$off(['checkTodo','deleteTodo','updateTodo'])
  }
}
</script>

<style>
body{
  margin:0;
}
#root{
  text-align:center;
}
.container{
  border:10px solid whitesmoke;
  position:relative;
  margin:auto;
  width:1000px;
}

.Hl{
  font-size:60px;
}
</style>
