<template>
  <div class="FooterTodo-css" v-show="DefaultTodo.length">
      <label class="FooterTodo-label">
          <input 
            type="checkbox"
            :checked="isAll"
            @change="checkAll"
          >
          <a onselectstart='return false'>Select All {{doneTotal}} / Share {{DefaultTodo.length}}</a>
      </label>
      <button class="btn btn-css" @click="clearAll">Delete Selected</button>
  </div>
</template>

<script>
export default {
    name:'FooterTodo',
    // props:['DefaultTodo','checkAllTodo','clearAllTodo'],
    props:['DefaultTodo'],
    computed: {
        // 监视勾选
        doneTotal(){
          let i = 0;
          this.DefaultTodo.forEach((todo)=>{
            if(todo.done){
              return i++
            }
          })
          return i;
        },
        isAll(){
          return this.doneTotal === this.DefaultTodo.length && this.DefaultTodo.length > 0;
        }
    },
    methods:{
        // 全选
        checkAll(event){
          // this.checkAllTodo(event.target.checked)
          this.$emit('checkAllTodo',event.target.checked)
        },
        // 删除已选
        clearAll(){
          /*
          for(let i=0;i<this.DefaultTodo.length;i++){
            if(this.DefaultTodo[i].done === true){
              if(confirm('确定删除吗？')){
                this.$emit('clearAllTodo')
              }
              // this.$emit('clearAllTodo')
            }else{
              return alert('????')
            }
            /*
            else if(this.DefaultTodo[i].done === false){
              return alert('????')
            }
          }*/
          
          if(confirm('确定删除吗？')){
            // this.clearAllTodo()
            this.$emit('clearAllTodo')
          }
          
        }
    }
}
</script>

<style scoped>
a{
    font-size:20px;
}
input{
    zoom:150%;
}

.FooterTodo-label{
    margin-left: -540px;
}

.btn{
  margin-bottom: 10px;
  position:relative;
  left: 540px;
}
.btn-css{
    padding:15px;
    background-color:red;
    font-size: 20px;
    border:solid white;
}

.btn:hover{
    background-color:#A52A2A;
    color:white;
}
</style>
