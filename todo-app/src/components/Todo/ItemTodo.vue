<template>
  <!-- ListTodo子组件 -->
  <transition
    appear
    name="animate__animated animate__bounce"
    enter-active-class="animate__fadeInDown"
    leave-active-class="animate__bounceOutDown"
  >
    <li class="ItemTodo-css">
      <label class="ItemTodo-label">
        <!-- @change 当元素的值发生改变时触发事件 -->
        <input 
          class="inputCheckbox"
          type="checkbox"
          :checked="item.done"
          @change="handleCheck(item.id)"
        >
        <span>{{item.name}}</span>
        <input
          type="text"
          class="input-edit"
          v-show="item.Edit"
          :value="item.name"
          @blur="handleBlur(item,$event)"
          @keyup.enter="handleBlur(item,$event)"
          ref="inputName"
        >
      </label>
      <button 
        class="btn-edit" 
        v-show="!item.Edit" 
        @click="handleEdit(item)">Edit</button>
      <button 
        class="btn btn-css" 
        @click="handleDelete(item.id)">Delete</button>
    </li>
  </transition>
</template>

<script>
import 'animate.css'  // 导入动画库
export default {
  name:'ItemTodo',
  props:['item'],
  methods:{
    // 勾选
    handleCheck(id){
      // 将对应的Todo对象的done值取反
      //this.checkTodo(id)
      this.$bus.$emit('checkTodo',id)
    },
    // 删除
    handleDelete(id){
      if(confirm('确定删除吗？')){
        // this.deleteTodo(id)
        this.$bus.$emit('deleteTodo',id)
      }
    },
    // 编辑
    handleEdit(item){
      // console.log(item)
      if(item.hasOwnProperty('Edit')){
        item.Edit = true;
      }else{
        this.$set(item,'Edit',true)
      }
      this.$nextTick(function(){
        this.$refs.inputName.focus()
      })
    },
    // 失去焦点编辑成功
    handleBlur(item,$event){
      item.Edit = false;
      if(!$event.target.value.trim()){
        return alert('内容不能为空！')
      }
      this.$bus.$emit('updateTodo',item.id,$event.target.value)
    },
    
  }
}
</script>

<style scoped>

li{
  list-style: none;
  margin-left: -20px;
  margin-right: 20px;
}

input{
  /* 放大复选框 */
  zoom: 150%;
  vertical-align: middle;
  position:absolute;
  left:24px;
  /* right: 0; */
}

.ItemTodo-css{
  background-color:whitesmoke;
  margin-top: 1px;
  margin-bottom: 1px;
  padding-top: 20px;
  padding-bottom: 20px;
  border: 5px solid white;
  border-radius: 3px 3px 3px 3px;
}

.ItemTodo-css:hover{
  background-color: #C0C0C0;
}


/* .ItemTodo-label{
  /* position:relative; */
  /* margin-left: -840px; */
  /* text-align: center; 
}
*/

/* span */

span{
  font-size: 23px;
  /* margin-left:-150px; */
  /* vertical-align: middle; */
  position:relative;
  /* left:100px; */
  right: 0;
}
.ItemTodo-css:hover span{
  color: white;
}

/* button */
.btn{
  /* float:right; */
  display: none;
  position:absolute;
  left: 900px;
}
.btn-edit{
  padding: 10px;
  background-color: skyblue;
  font-size: 20px;
  border: none;
  display: none;
  position: absolute;
  left:835px;
}
.btn-edit:hover {
  background-color: #00BFFF;
  color: white;
}
.ItemTodo-css:hover .btn-edit{
  display: block;
  margin-top: -34px;
  margin-left: -12px;
  border-radius: 3px 3px 3px 3px;
}
.btn-css{
  /* margin-top: -13px; */
  padding:10px;
  background-color:red;
  border:none;
  font-size: 20px;
}
.ItemTodo-css:hover .btn{
  display: block;
  margin-top: -34px;
  margin-left: -12px;
  border-radius: 3px 3px 3px 3px;
}
.btn:hover{
  background-color:#A52A2A;
  color:white;
}

.input-edit{
  width: 400px;
  outline: none;
  border: solid white;
  border-radius: 4px 4px 4px 4px;
  position: absolute;
  left:100px;
}

.input-edit:hover{
  border: solid gray;
}

/*
.inputCheckbox input[type=checkbox]:checked {
  background: red;
  border: 11px solid white;
}*/
</style>
