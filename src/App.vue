<template>
  <div class="todo-container">
    <div class="todo-wrap">
      <TodoHeader :addtodo="addtodo"/>
      <TodoMain :todos="todos" :deletetodo="deletetodo" />
      <TodoFooter :todos="todos" :selectAllTodos="selectAllTodos" :clearall="clearall"/>
    </div>
  </div>
</template>

<script>
  import Header from './components/Header.vue'
  import Main from './components/Main.vue'
  import Footer from './components/Footer.vue'
  import storageUtils from './utils/storageUtils'
  export default {

    data(){
      return {
        todos:storageUtils.readTodos()
      }
    },

    methods:{
      addtodo(todo){
        this.todos.unshift(todo)
      },
      deletetodo(index){
        this.todos.splice(index,1)
      },
      selectAllTodos(value){
        this.todos.forEach((todo,index)=>todo.complete=value)
      },
      clearall(){
        this.todos=this.todos.filter((todo)=>!todo.complete)
      }

    },
    watch:{
      todos:{
        deep:true,
        handler:storageUtils.saveTodos
      }
    },
    components: {
      TodoHeader: Header,
      TodoMain: Main,
      TodoFooter: Footer,
    },
  }
</script>


<style scoped>
  .todo-container {
    width: 600px;
    margin: 0 auto;
  }
  .todo-container .todo-wrap {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }
</style>
