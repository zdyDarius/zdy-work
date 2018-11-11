<template>
  <div class="todo-footer">
    <label>
      <input type="checkbox"   v-model="isCheckall" />
    </label>
    <span>
       <span>已完成{{comsize}}</span>/全部{{todos.length}}
        </span>
    <button class="btn btn-danger" v-show="comsize" @click="deleteall">清除已完成任务</button>
  </div>
</template>

<script>
  export default {
    props:['todos','selectAllTodos','clearall'],
    data () {
      return {}
    },
    methods:{
      deleteall(){
        console.log(this.claerall)
        this.clearall()
      }
    },
    computed:{
      comsize:{
        get(){
          return this.todos.reduce((pre,todo)=>pre+(todo.complete?1:0) ,0)
        },
      },
      isCheckall:{
        get(){
          return this.todos.length===this.comsize && this.comsize!==0
        },
        set(value){
          this.selectAllTodos(value)
        }

      }
    }
  }
</script>


<style scoped>
  .todo-footer {
    height: 40px;
    line-height: 40px;
    padding-left: 6px;
    margin-top: 5px;
  }

  .todo-footer label {
    display: inline-block;
    margin-right: 20px;
    cursor: pointer;
  }

  .todo-footer label input {
    position: relative;
    top: -1px;
    vertical-align: middle;
    margin-right: 5px;
  }

  .todo-footer button {
    float: right;
    margin-top: 5px;
  }

</style>
