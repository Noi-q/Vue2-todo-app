<template>
  <div class="AddTodo">
    <div class="AddTodo-css">
      <input type="text" placeholder="Add to a Todo" @keyup.enter="addTodo">
    </div>
  </div>
</template>

<script>
// 导入nanoid包
import {nanoid} from "nanoid"

export default {
  name:'AddTodo',
  props:['DefaultTodo'],
  methods:{
    // 添加Todo
    addTodo(event){
      // 校验数据
      if(!event.target.value){
        return alert('输入内容不能为空！')
      } else if(event.target.value.length >= 32){
        return alert('输入内容字数太大！')
      }else {
        // console.log(this.DefaultTodo)
        for(let i=0;i<this.DefaultTodo.length;i++){
          if(this.DefaultTodo[i].name === event.target.value){
            return alert('已经含有该Todo！')
          }
        }
      }
      /*
      this.$nextTick(function(){
        if(event.target.value === this.DefaultTodo.name){
          // return alert('已经含有该Todo！')
          return console.log(this)
        }
      })*/
      // 用户输入包装为对象
      const todoObj = {
        id:nanoid(),
        // event.target 是标签体
        name:event.target.value,
        done:false,
      }
      // 通过自定义事件把对象传给App组件
      this.$emit('AppAddTodo',todoObj)
      // 清空输入内容
      event.target.value = ''
    }
  }
}
</script>

<style scoped>
.AddTodo-css{
  background-color:whitesmoke;
  /* height:50px; */
  padding-top: 20px;
  padding-bottom: 20px;
  margin-left:150px;
  margin-right:150px;
  border-radius:10px 10px 10px 10px;
}

input {
  width:300px;
  height:30px;
  padding:8px;
  border-radius:18px 18px 18px 18px;
  font-size:20px;
  border:solid white;
  /* 取消点击默认样式 */
  outline:none;
}

input:hover {
  border:solid #C0C0C0;
}

</style>
