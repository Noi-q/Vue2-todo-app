<template>
  <ul class="ListTodo">
    <ItemTodo 
      v-for="itemTodo in DefaultTodo"
      :key="itemTodo.id"
      :item="itemTodo"
      />
  </ul>
</template>

<script>
import ItemTodo from './ItemTodo'

export default {
  name:'ListTodo',
  components:{
    ItemTodo,
  },
  props:['DefaultTodo']
}
</script>

<style scoped>

</style>
